# MikroTik HAP Series: VLAN Setup with Inter-VLAN Routing

**Target Device:** HAP ac², HAP ac³, HAP (any 5-port model)  
**RouterOS:** v6.48+  
**Scope:** Physical VLAN configuration → IP addressing → DHCP → Firewall rules → Inter-VLAN routing  
**Difficulty:** Beginner-friendly with step-by-step breakdown

---

## 🔍 Prerequisites & Setup Checklist

Before touching the CLI, verify:

- [ ] HAP router accessible via Winbox or SSH
- [ ] All cables labeled or documented (which physical port = which VLAN intent)
- [ ] Device inventory: how many devices per VLAN?
- [ ] IP ranges decided (don't overlap)
- [ ] VLAN IDs chosen (avoid 1 for management, use 10, 20, 30... for clarity)
- [ ] Decision: How do you access the router post-VLAN setup? (dedicated mgmt VLAN or one LAN VLAN?)

---

## 📋 Example Setup (Adapt to Your Needs)

| VLAN ID | Name | Purpose | IP Subnet | Ports |
|---------|------|---------|-----------|-------|
| 10 | Management | Router access + admin devices | 192.168.10.0/24 | ether2 |
| 20 | Workstations | User PCs/Laptops | 192.168.20.0/24 | ether3, ether4 |
| 30 | Guests | Guest network (isolated) | 192.168.30.0/24 | ether5 |
| —  | WAN | Upstream ISP | DHCP/Static | ether1 |

**Key rule:** Each VLAN = one IP subnet = one router interface = one DHCP scope (optional)

---

## ⚡ Step 1: Plan Your VLAN Layout on Paper

Create a simple diagram showing which devices go where:

```
┌─────────────────────────────────────┐
│         MikroTik HAP ac²            │
├─────────────────────────────────────┤
│ ether1: WAN (ether1 → ISP)          │
│ ether2: Access port, VLAN 10 (Mgmt) │
│ ether3: Access port, VLAN 20 (Work) │
│ ether4: Access port, VLAN 20 (Work) │
│ ether5: Access port, VLAN 30 (Guest)│
└─────────────────────────────────────┘
         ↓
    📊 Router IPs (one per VLAN):
    - VLAN 10: 192.168.10.1/24  (gateway)
    - VLAN 20: 192.168.20.1/24  (gateway)
    - VLAN 30: 192.168.30.1/24  (gateway)
```

**Why:** If you skip this, you'll get lost configuring interfaces.

---

## 🔧 Step 2: Create VLAN Interfaces (CLI)

Log into the HAP via Winbox → New Terminal, or SSH, then paste commands one at a time.

### 2.1 Create virtual VLAN interfaces

```bash
# VLAN 10 - Management
/interface vlan
add name=vlan10 vlan-id=10 interface=bridge

# VLAN 20 - Workstations
add name=vlan20 vlan-id=20 interface=bridge

# VLAN 30 - Guests
add name=vlan30 vlan-id=30 interface=bridge
```

**What this does:**
- Creates three virtual interfaces (vlan10, vlan20, vlan30)
- Each is tagged with its VLAN ID on the **bridge** (explained below)

### 2.2 Create a bridge to tag/untag traffic

```bash
/interface bridge
add name=bridge protocol-mode=rstp
```

**Why a bridge?**
- MikroTik uses a bridge to manage VLAN membership
- Physical ports connect to the bridge, not directly to VLANs
- VLAN tagging happens at the bridge level

### 2.3 Connect physical ports to the bridge

```bash
/interface bridge port
# Add ether2, ether3, ether4, ether5 to the bridge
add interface=ether2 bridge=bridge
add interface=ether3 bridge=bridge
add interface=ether4 bridge=bridge
add interface=ether5 bridge=bridge
```

**Note:** ether1 stays untagged (WAN), do NOT add it to the bridge.

---

## 🏷️ Step 3: Assign Ports to VLANs (Tagging Rules)

**Two modes:**
- **Access port:** Belongs to ONE VLAN, untagged (device doesn't know about VLAN)
- **Trunk port:** Carries multiple VLANs, tagged (switch-to-switch)

For a HAP with end devices (PCs, phones), use **access ports**.

### 3.1 Configure access ports and VLAN membership

```bash
/interface bridge vlan
# VLAN 10 on ether2 (untagged = access port)
add bridge=bridge vlan-ids=10 untagged=ether2 tagged=bridge

# VLAN 20 on ether3, ether4 (untagged = access ports)
add bridge=bridge vlan-ids=20 untagged=ether3,ether4 tagged=bridge

# VLAN 30 on ether5 (untagged = access port)
add bridge=bridge vlan-ids=30 untagged=ether5 tagged=bridge
```

**Key concept:**
- `untagged=ether2` → Traffic on ether2 is automatically tagged as VLAN 10 (invisible to device)
- `tagged=bridge` → The bridge itself knows how to handle VLAN 10 traffic
- Multiple ports can share a VLAN (ether3 + ether4 both VLAN 20)

### 3.2 Verify VLAN membership

```bash
/interface bridge vlan print
```

You should see:
```
Flags: X - disabled; 
 #   BRIDGE  VLAN-ID  TAGGED                  UNTAGGED         
 0   bridge  10                               ether2,bridge    
 1   bridge  20                               ether3,ether4,b…
 2   bridge  30                               ether5,bridge    
```

**✅ If this looks right, continue. If not, delete entries and retry.**

---

## 🌐 Step 4: Assign IP Addresses to Each VLAN Interface

Each VLAN interface needs an IP—this is the **gateway** for that VLAN.

```bash
/ip address
# VLAN 10 gateway (Management)
add address=192.168.10.1/24 interface=vlan10

# VLAN 20 gateway (Workstations)
add address=192.168.20.1/24 interface=vlan20

# VLAN 30 gateway (Guests)
add address=192.168.30.1/24 interface=vlan30
```

### Verify IPs are assigned:

```bash
/ip address print
```

You should see all three VLAN interfaces with their IPs.

---

## 📡 Step 5: Configure DHCP Server (One per VLAN)

Devices on each VLAN will request IPs from the router. Set up DHCP pools.

### 5.1 Create DHCP pools (one per VLAN)

```bash
/ip pool
# Pool for VLAN 10
add name=dhcp-vlan10 ranges=192.168.10.100-192.168.10.254

# Pool for VLAN 20
add name=dhcp-vlan20 ranges=192.168.20.100-192.168.20.254

# Pool for VLAN 30
add name=dhcp-vlan30 ranges=192.168.30.100-192.168.30.254
```

**Range rationale:**
- .1 = router (gateway)
- .2-.99 = reserved for static IPs (servers, network devices)
- .100-.254 = DHCP pool for clients

### 5.2 Create DHCP servers

```bash
/ip dhcp-server
# VLAN 10 DHCP
add name=dhcp-vlan10 interface=vlan10 address-pool=dhcp-vlan10 disabled=no

# VLAN 20 DHCP
add name=dhcp-vlan20 interface=vlan20 address-pool=dhcp-vlan20 disabled=no

# VLAN 30 DHCP
add name=dhcp-vlan30 interface=vlan30 address-pool=dhcp-vlan30 disabled=no
```

### 5.3 Create DHCP networks (tell server what subnet to serve)

```bash
/ip dhcp-server network
# VLAN 10
add address=192.168.10.0/24 gateway=192.168.10.1 dns-server=8.8.8.8

# VLAN 20
add address=192.168.20.0/24 gateway=192.168.20.1 dns-server=8.8.8.8

# VLAN 30
add address=192.168.30.0/24 gateway=192.168.30.1 dns-server=8.8.8.8
```

**Optional:** Replace `8.8.8.8` with your ISP's DNS or local DNS server.

---

## 🔥 Step 6: Configure Firewall Rules (Inter-VLAN Routing)

By default, MikroTik allows all inter-VLAN traffic. To control it, add firewall rules.

### 6.1 Default policy: Allow inter-VLAN routing

If you want ALL VLANs to reach ALL VLANs (permissive), skip this. Otherwise:

```bash
/ip firewall filter
# Allow traffic from VLAN 20 → VLAN 30 (optional rule example)
add chain=forward in-interface=vlan20 out-interface=vlan30 action=accept

# Allow traffic from VLAN 30 → VLAN 20
add chain=forward in-interface=vlan30 out-interface=vlan20 action=accept
```

### 6.2 Isolate guests (VLAN 30 cannot reach others)

```bash
# Drop traffic FROM guests TO workstations
/ip firewall filter
add chain=forward in-interface=vlan30 out-interface=vlan20 action=drop

# Drop traffic FROM guests TO management
add chain=forward in-interface=vlan30 out-interface=vlan10 action=drop

# Allow guests to talk TO WAN (internet)
add chain=forward in-interface=vlan30 out-interface=ether1 action=accept
```

**Important:** Order matters. Rules are processed top-to-bottom. Add drop rules BEFORE accept rules.

### Verify firewall rules:

```bash
/ip firewall filter print
```

---

## 🛡️ Step 7: Enable Masquerading for Internet Access

If your HAP has a WAN connection, enable NAT so VLANs can reach the internet.

```bash
/ip firewall nat
add chain=srcnat out-interface=ether1 action=masquerade
```

**What this does:** VLANs going to the internet (ether1) are translated to the router's WAN IP.

---

## 👤 Step 8: Management Access (Winbox/SSH to Router)

You need a way to access the router AFTER VLANs are active. Two options:

### Option A: Add router IP to VLAN 10 (Management VLAN only)

```bash
/interface list
add name=management

/interface list member
add interface=vlan10 list=management

/ip firewall filter
add chain=input in-interface-list=management action=accept
```

Connect admin devices to ether2 (VLAN 10), then access router at 192.168.10.1

### Option B: Keep WAN management enabled (risky but easy)

```bash
/ip firewall filter
add chain=input in-interface=ether1 protocol=tcp dst-port=8291 action=accept
add chain=input in-interface=ether1 protocol=tcp dst-port=22 action=accept
```

Allows Winbox (8291) and SSH (22) from WAN. Consider limiting to your ISP's /24.

**⚠️ Gotcha:** After VLAN config, if you can't access the router, you may need a hard reset (factory reset button). Plan this carefully.

---

## ✅ Step 9: Verification & Testing

### 9.1 Test from a device on VLAN 20 (Workstations)

1. Connect a PC to ether3 or ether4
2. Restart or renew DHCP lease
3. Open terminal:

```bash
ipconfig /all        # Windows
ip addr show         # Linux
```

You should see IP from 192.168.20.100-254 range.

### 9.2 Test inter-VLAN routing

From VLAN 20 device, ping VLAN 10 router:

```bash
ping 192.168.10.1
```

Should **succeed** (if firewall rules allow it).

From VLAN 30 device, ping VLAN 20:

```bash
ping 192.168.20.1
```

Should **fail** (if you applied the guest isolation rules).

### 9.3 Test internet access

```bash
ping 8.8.8.8
```

Should succeed (assumes ether1 has internet).

### 9.4 Check router-side statistics

```bash
/interface print stats
```

Look for byte counts on vlan10, vlan20, vlan30—confirms traffic flowing.

---

## 🚨 Common Gotchas & Fixes

| Problem | Cause | Fix |
|---------|-------|-----|
| Devices can't get IP | DHCP server disabled or pool exhausted | Check `/ip dhcp-server print` and `/ip pool print` |
| Can't reach router after VLAN | Firewall blocked management traffic | Re-enable input chain or use recovery via reset button |
| Inter-VLAN works but no internet | NAT not enabled | Add masquerade rule: `/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade` |
| One VLAN works, others don't | VLAN not added to bridge or wrong untagged port | Check `/interface bridge vlan print` for all VLANs |
| Port forwarding doesn't work | Masquerading rule catches it first | Reorder NAT rules—DST rule BEFORE srcnat |

---

## 📝 Quick Reference: Complete Configuration Dump

To export your config for backup or documentation:

```bash
/export compact
```

Paste output into a text file. To restore:

```bash
/import file-name=backup.rsc
```

---

## 🎯 Next Steps (When Confident)

1. **VLAN tagging on upstream:** If you have a managed switch upstream, configure trunk ports with the same VLAN IDs
2. **Dynamic routing (OSPF/BGP):** If you have multiple routers, learn OSPF on RouterOS
3. **QoS per VLAN:** Queue trees to limit bandwidth per VLAN
4. **RADIUS authentication:** 802.1X for access control (enterprise setup)

---

## 📖 CLI Command Summary (Copy-Paste Order)

```bash
# 1. Bridge
/interface bridge add name=bridge protocol-mode=rstp
/interface bridge port add interface=ether2 bridge=bridge
/interface bridge port add interface=ether3 bridge=bridge
/interface bridge port add interface=ether4 bridge=bridge
/interface bridge port add interface=ether5 bridge=bridge

# 2. VLAN interfaces
/interface vlan add name=vlan10 vlan-id=10 interface=bridge
/interface vlan add name=vlan20 vlan-id=20 interface=bridge
/interface vlan add name=vlan30 vlan-id=30 interface=bridge

# 3. VLAN membership
/interface bridge vlan add bridge=bridge vlan-ids=10 untagged=ether2 tagged=bridge
/interface bridge vlan add bridge=bridge vlan-ids=20 untagged=ether3,ether4 tagged=bridge
/interface bridge vlan add bridge=bridge vlan-ids=30 untagged=ether5 tagged=bridge

# 4. IP addresses
/ip address add address=192.168.10.1/24 interface=vlan10
/ip address add address=192.168.20.1/24 interface=vlan20
/ip address add address=192.168.30.1/24 interface=vlan30

# 5. DHCP pools
/ip pool add name=dhcp-vlan10 ranges=192.168.10.100-192.168.10.254
/ip pool add name=dhcp-vlan20 ranges=192.168.20.100-192.168.20.254
/ip pool add name=dhcp-vlan30 ranges=192.168.30.100-192.168.30.254

# 6. DHCP servers
/ip dhcp-server add name=dhcp-vlan10 interface=vlan10 address-pool=dhcp-vlan10 disabled=no
/ip dhcp-server add name=dhcp-vlan20 interface=vlan20 address-pool=dhcp-vlan20 disabled=no
/ip dhcp-server add name=dhcp-vlan30 interface=vlan30 address-pool=dhcp-vlan30 disabled=no

# 7. DHCP networks
/ip dhcp-server network add address=192.168.10.0/24 gateway=192.168.10.1 dns-server=8.8.8.8
/ip dhcp-server network add address=192.168.20.0/24 gateway=192.168.20.1 dns-server=8.8.8.8
/ip dhcp-server network add address=192.168.30.0/24 gateway=192.168.30.1 dns-server=8.8.8.8

# 8. NAT (internet access)
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade

# 9. Optional: Guest isolation
/ip firewall filter add chain=forward in-interface=vlan30 out-interface=vlan20 action=drop
/ip firewall filter add chain=forward in-interface=vlan30 out-interface=vlan10 action=drop
/ip firewall filter add chain=forward in-interface=vlan30 out-interface=ether1 action=accept
```

Paste this entire block into SSH terminal at once, or line-by-line via Winbox terminal.

---

**Last Updated:** 2025  
**Author Notes:** Written for HAP ac² but applies to all HAP variants. Test in lab first.
