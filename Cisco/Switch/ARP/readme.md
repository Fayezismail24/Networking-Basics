# 🔍 ARP Protocol

## 📌 What is ARP?

**ARP (Address Resolution Protocol)** is a **Layer 2/3 hybrid protocol** that maps **IP addresses to MAC addresses** on the same local network (LAN).

> **Core Function:** "I know the IP address. What's the MAC address?"

Without ARP, devices couldn't find each other on the LAN because switches forward frames based on **MAC addresses**, not IP addresses.

---

## 🔗 Why ARP is Critical:

### The Problem:
```
Host A: "I need to send data to 192.168.1.50"
         But I only know the IP — I don't know its MAC address
         I can't send a frame without a destination MAC!
         
Switch: "I need a destination MAC to forward this frame"
```

### The Solution:
```
Host A broadcasts: "Who has IP 192.168.1.50? Send me your MAC!"
Host B replies: "I have 192.168.1.50. My MAC is AA:BB:CC:DD:EE:FF"
Host A: "Perfect! Now I can send the frame to AA:BB:CC:DD:EE:FF"
```

---

## 📊 ARP in the Network Stack:

```
┌─────────────────────────────────┐
│   Layer 7: Application (HTTP)   │
├─────────────────────────────────┤
│   Layer 4: Transport (TCP/UDP)  │
├─────────────────────────────────┤
│   Layer 3: Network (IP) ◄────┐  │
├─────────────────────────────┤  │
│   ★ ARP (Layer 3 protocol)  ◄─┘ │  ← Sits here!
├─────────────────────────────────┤
│   Layer 2: Data Link (MAC)      │  ← Uses MAC addresses
├─────────────────────────────────┤
│   Layer 1: Physical             │
└─────────────────────────────────┘
```

**ARP is NOT a Layer 2 or Layer 3 protocol exclusively** — it's a **hybrid that uses Layer 2 and 3 information**.

---

## 📦 ARP Packet Structure

### Full ARP Header (28 bytes)

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
┌───────────────────────────────────────────────────────────────┐
│          Hardware Type (HTYPE)                                │  (2 bytes)
├───────────────────────────────────────────────────────────────┤
│          Protocol Type (PTYPE)                                │  (2 bytes)
├───────┬───────────────────────────────────────────────────────┤
│ HLEN  │ PLEN                      │ Operation (OPER)           │  (1+1+2 bytes)
├───────┴───────────────────────────┴───────────────────────────┤
│                Sender Hardware Address (SHA)                  │  (6 bytes for Ethernet)
├───────────────────────────────────────────────────────────────┤
│                 Sender Protocol Address (SPA)                 │  (4 bytes for IPv4)
├───────────────────────────────────────────────────────────────┤
│              Target Hardware Address (THA)                    │  (6 bytes for Ethernet)
├───────────────────────────────────────────────────────────────┤
│                Target Protocol Address (TPA)                  │  (4 bytes for IPv4)
└───────────────────────────────────────────────────────────────┘
```

### ARP Header Fields:

| Field | Size | Purpose | Values |
|-------|------|---------|--------|
| **Hardware Type (HTYPE)** | 2 bytes | Network type | `1` = Ethernet, `6` = Token Ring, `7` = ARCNET |
| **Protocol Type (PTYPE)** | 2 bytes | Protocol type | `0x0800` = IPv4, `0x86DD` = IPv6 |
| **Hardware Address Length (HLEN)** | 1 byte | MAC address length | `6` for Ethernet |
| **Protocol Address Length (PLEN)** | 1 byte | IP address length | `4` for IPv4, `16` for IPv6 |
| **Operation (OPER)** | 2 bytes | ARP action | `1` = Request, `2` = Reply, `3` = RARP Request, `4` = RARP Reply |
| **Sender Hardware Address (SHA)** | Variable | Sender's MAC | `AA:BB:CC:DD:EE:FF` |
| **Sender Protocol Address (SPA)** | Variable | Sender's IP | `192.168.1.100` |
| **Target Hardware Address (THA)** | Variable | Target's MAC | `00:00:00:00:00:00` (ARP Request), or real MAC (ARP Reply) |
| **Target Protocol Address (TPA)** | Variable | Target's IP | `192.168.1.50` |

### Real ARP Request Example:

```
Hardware Type: 1 (Ethernet)
Protocol Type: 0x0800 (IPv4)
HLEN: 6 (Ethernet MAC = 6 bytes)
PLEN: 4 (IPv4 = 4 bytes)
Operation: 1 (Request)
Sender Hardware Address (SHA): AA:BB:CC:DD:EE:FF (Host A's MAC)
Sender Protocol Address (SPA): 192.168.1.100 (Host A's IP)
Target Hardware Address (THA): 00:00:00:00:00:00 (Unknown — looking for this)
Target Protocol Address (TPA): 192.168.1.50 (Looking for this IP)

Message: "I'm 192.168.1.100 (AA:BB:CC:DD:EE:FF). 
          Who has 192.168.1.50? Please tell me your MAC!"
```

### Real ARP Reply Example:

```
Hardware Type: 1 (Ethernet)
Protocol Type: 0x0800 (IPv4)
HLEN: 6
PLEN: 4
Operation: 2 (Reply)
Sender Hardware Address (SHA): 11:22:33:44:55:66 (Host B's MAC)
Sender Protocol Address (SPA): 192.168.1.50 (Host B's IP)
Target Hardware Address (THA): AA:BB:CC:DD:EE:FF (Host A's MAC — now filled in)
Target Protocol Address (TPA): 192.168.1.100 (Host A's IP)

Message: "I'm 192.168.1.50. My MAC is 11:22:33:44:55:66!"
```

---

## 🔄 ARP Request/Reply Process (Detailed)

### Scenario: Host A (192.168.1.100) wants to send data to Host B (192.168.1.50)

#### Step 1: Host A checks its ARP cache
```
Host A's ARP Cache:
  192.168.1.50 → ? (Not found)

Action: Host A needs to broadcast an ARP Request
```

#### Step 2: Host A broadcasts ARP Request
```
Layer 2 Ethernet Frame:
┌─────────────────────────────────────────┐
│ Dest MAC: FF:FF:FF:FF:FF:FF (broadcast) │  ← BROADCAST!
│ Src MAC:  AA:BB:CC:DD:EE:FF (Host A)    │
│ EtherType: 0x0806 (ARP)                 │
├─────────────────────────────────────────┤
│ ARP Request:                            │
│  SHA: AA:BB:CC:DD:EE:FF                 │
│  SPA: 192.168.1.100                     │
│  THA: 00:00:00:00:00:00 (unknown)       │
│  TPA: 192.168.1.50                      │
└─────────────────────────────────────────┘

Transmission: Sent on ALL ports on the switch (broadcast)
```

#### Step 3: All hosts on the LAN receive the ARP Request
```
Host B: "Is this asking for 192.168.1.50? YES, that's me!"
Host C: "Is this asking for 192.168.1.60? No, not me. Ignore."
Host D: "Is this asking for 192.168.1.70? No, not me. Ignore."
```

#### Step 4: Host B sends ARP Reply (unicast)
```
Layer 2 Ethernet Frame:
┌─────────────────────────────────────────┐
│ Dest MAC: AA:BB:CC:DD:EE:FF (Host A)    │  ← UNICAST (only to Host A)
│ Src MAC:  11:22:33:44:55:66 (Host B)    │
│ EtherType: 0x0806 (ARP)                 │
├─────────────────────────────────────────┤
│ ARP Reply:                              │
│  SHA: 11:22:33:44:55:66 (Host B)        │
│  SPA: 192.168.1.50                      │
│  THA: AA:BB:CC:DD:EE:FF (Host A)        │
│  TPA: 192.168.1.100                     │
└─────────────────────────────────────────┘

Message: "I'm 192.168.1.50. My MAC is 11:22:33:44:55:66!"
```

#### Step 5: Host A receives ARP Reply
```
Host A updates ARP cache:
  192.168.1.50 → 11:22:33:44:55:66

Now Host A can send frames to 192.168.1.50 using MAC 11:22:33:44:55:66
```

---

## 💾 ARP Cache (ARP Table)

### What is the ARP Cache?

Each host maintains a **table of IP ↔ MAC mappings** it has recently learned.

### Example ARP Cache on Host A:

```
192.168.1.1    → AA:AA:AA:AA:AA:AA (gateway/router)
192.168.1.50   → 11:22:33:44:55:66 (Host B) [Just learned]
192.168.1.100  → AA:BB:CC:DD:EE:FF (self)
192.168.1.255  → FF:FF:FF:FF:FF:FF (broadcast)

TTL (Time to Live):
  - Dynamic entries: 120–300 seconds (varies by OS)
  - Static entries: Permanent
  - When TTL expires: Entry is removed
```

### Viewing ARP Cache:

**Windows:**
```bash
arp -a
```

**Output:**
```
Interface: 192.168.1.100 --- 0xa
  Internet Address      Physical Address      Type
  192.168.1.1           aa-aa-aa-aa-aa-aa     dynamic
  192.168.1.50          11-22-33-44-55-66     dynamic
  192.168.1.255         ff-ff-ff-ff-ff-ff     static
  224.0.0.1             01-00-5e-00-00-01     static
```

**Linux:**
```bash
arp -a
ip neighbor show
```

**Output:**
```
? (192.168.1.1) at aa:aa:aa:aa:aa:aa [ether] on eth0
? (192.168.1.50) at 11:22:33:44:55:66 [ether] on eth0
```

### ARP Cache Timeout Behavior:

```
Time 0:       ARP Request sent for 192.168.1.50
Time 1s:      ARP Reply received
              Cache entry created: 192.168.1.50 → 11:22:33:44:55:66
              TTL = 300 seconds

Time 30s:     Data sent to 192.168.1.50 (cached, no new ARP request)

Time 120s:    Entry still in cache (180 sec remaining)

Time 301s:    TTL expired, entry removed
              Next packet to 192.168.1.50 triggers new ARP Request
```

---

## 🎭 ARP Packet Types

### 1️⃣ ARP Request (OPER = 1)

**Sender asks:** "Who has this IP?"

```
Operation: 1 (Request)
THA: 00:00:00:00:00:00 (don't know yet)

Example:
  "Who has 192.168.1.50?"
  (TPA field = 192.168.1.50)
```

**Transmission:** Broadcast (FF:FF:FF:FF:FF:FF)

---

### 2️⃣ ARP Reply (OPER = 2)

**Sender responds:** "That's me! Here's my MAC!"

```
Operation: 2 (Reply)
THA: <actual MAC of the requester>

Example:
  "I have 192.168.1.50! My MAC is 11:22:33:44:55:66"
```

**Transmission:** Unicast (only to requester)

---

### 3️⃣ Gratuitous ARP (Request or Reply)

**A device announces itself without being asked.**

```
Host sends ARP Request or Reply for ITSELF:
  SPA = TPA (sender IP = target IP)
  
Example:
  "I'm 192.168.1.100 with MAC AA:BB:CC:DD:EE:FF"
  (both SPA and TPA = 192.168.1.100)
```

**Use Cases:**
- **Announce presence** — newly booted device
- **Update ARP caches** — "I have a new MAC address"
- **Detect IP conflicts** — if reply received, someone else has your IP
- **VRRP/HSRP** — virtual router announces itself

**Example Wireshark Output:**
```
ARP request
  Sender IP: 192.168.1.100
  Target IP: 192.168.1.100 (SAME!)
  Message: "I'm 192.168.1.100, MAC AA:BB:CC:DD:EE:FF"
```

---

### 4️⃣ Proxy ARP

**A router responds to ARP requests on behalf of a remote host.**

```
Host A: "Who has 10.0.0.50?"
        (target is on different network)

Router (Proxy): "I have 10.0.0.50! Use my MAC!" (or I'll forward for you)
        (even though it's on the other side of the router)

Original purpose: Connect hosts to different subnets without routing knowledge
Modern use: Load balancing, failover
```

---

### 5️⃣ Reverse ARP (RARP) — Obsolete

**Maps MAC addresses to IP addresses** (opposite of ARP).

```
OPER = 3 (RARP Request)
OPER = 4 (RARP Reply)

Example: A diskless workstation booting up:
  "I have MAC 11:22:33:44:55:66. What's my IP address?"
```

**Status:** Replaced by DHCP in modern networks.

---

## 🌐 ARP Across Subnets

### Scenario 1: Local Network (Same Subnet) ✅

```
Host A: 192.168.1.100
Host B: 192.168.1.50
Gateway: 192.168.1.1

Same subnet: 192.168.1.0/24

Host A → Host B:
  1. Check ARP cache for 192.168.1.50
  2. If not found, broadcast ARP Request
  3. Host B replies with MAC
  4. Data sent directly to Host B ✓
```

### Scenario 2: Different Networks (Cross-Subnet) ❌

```
Host A: 192.168.1.100 (subnet 192.168.1.0/24)
Host B: 10.0.0.50 (subnet 10.0.0.0/24)
Gateway: 192.168.1.1

Different subnets!

Host A → Host B:
  1. Check routing table: 10.0.0.50 is not local
  2. Send to gateway: 192.168.1.1
  3. ARP for gateway's MAC: 192.168.1.1
  4. Get gateway MAC
  5. Send frame to gateway MAC
  6. Gateway forwards to Host B (new ARP request on other side)
  
✓ Host B receives data via gateway
```

**Key Point:** ARP only works on the **same physical segment (LAN)**.

---

## 📊 ARP vs IP Routing Comparison

| Aspect | ARP | IP Routing |
|--------|-----|-----------|
| **Purpose** | Find MAC from IP (locally) | Find path to IP (globally) |
| **Scope** | Local network (LAN) | Any network (Internet) |
| **Question** | "What's the MAC?" | "Which interface/gateway?" |
| **Protocol** | Layer 2/3 | Layer 3 |
| **Cache** | ARP Cache (120–300s) | Routing Table (static/dynamic) |
| **Broadcast** | Yes (floods to all ports) | No (consulted locally) |
| **Example** | 192.168.1.50 → AA:BB:CC:DD:EE:FF | 10.0.0.0/24 → via 192.168.1.1 |

---

## 🔴 Common ARP Issues & Troubleshooting

### Issue 1: "No Route to Host" Error

**Symptoms:**
```
ping 192.168.1.50
No route to host
```

**Possible Causes:**
1. Host is not on the local network (wrong subnet)
2. ARP request broadcast but no reply received
3. Host is powered off or disconnected

**Troubleshooting:**
```bash
# Check if target is in same subnet
ipconfig /all (Windows)
ip addr show (Linux)

# Check ARP cache
arp -a

# Try to get ARP reply
arp -d 192.168.1.50  (delete entry)
ping 192.168.1.50    (sends new ARP request)

# Check switch connectivity
  - Cable plugged in?
  - Port enabled on switch?
  - VLAN correct?
```

---

### Issue 2: "Incomplete" ARP Entry

**Symptoms:**
```
arp -a
  192.168.1.50    incomplete   (MAC unknown)
```

**Cause:** ARP request sent but no reply received.

**Why:**
- Host 192.168.1.50 powered off
- Host on different VLAN (even though IP looks local)
- Firewall blocking ARP reply
- Proxy ARP misconfigured
- Network cable disconnected

**Fix:**
```bash
# Delete and retry
arp -d 192.168.1.50
ping 192.168.1.50

# If still incomplete after retry:
  - Verify host is actually on this network
  - Check switch port status
  - Check for VLAN issues
  - Disable any proxy ARP if enabled
```

---

### Issue 3: Duplicate ARP Reply (ARP Conflict)

**Symptoms:**
```
Duplicate IP address detected: 192.168.1.100 is using 11:22:33:44:55:66
```

**Cause:** Two devices have the same IP address!

**Scenario:**
```
Host A: 192.168.1.100 → MAC: AA:BB:CC:DD:EE:FF
Host B: 192.168.1.100 → MAC: 11:22:33:44:55:66 (WRONG!)

When Host C pings 192.168.1.100:
  - Gets reply from Host A with MAC AA:BB:CC:DD:EE:FF
  - Gets reply from Host B with MAC 11:22:33:44:55:66
  
Result: ARP conflict detected!
```

**Fix:**
```bash
# Find the duplicate IP
# Windows:
arp -a | find "192.168.1.100"

# Linux:
arp | grep 192.168.1.100
ip neighbor | grep 192.168.1.100

# Check MAC addresses:
  - If two different MACs appear → IP conflict!
  - Fix: Change one device's IP address
  - Or: Check DHCP server (assigning same IP twice)
```

---

### Issue 4: Proxy ARP Problems

**Symptoms:**
```
Router replies to ARP requests for hosts on other subnets
Unexpected network behavior
```

**Example:**
```
Host A (192.168.1.0/24) ARP for Host B (10.0.0.0/24)
Router: "I'll handle 10.0.0.0 — use my MAC!"

Expected: Only gateway's MAC
Actual: Gateway claims to have remote hosts (Proxy ARP enabled)
```

**Check if Proxy ARP is enabled:**
```bash
# Cisco Router
show ip arp proxy

# Linux
cat /proc/sys/net/ipv4/conf/eth0/proxy_arp

# Windows (rare, but possible)
netsh interface ipv4 show interface
```

---

### Issue 5: Slow Network / High ARP Traffic

**Symptoms:**
```
- Network performance degraded
- Wireshark shows excessive ARP requests
- CPU utilization on gateway high
```

**Causes:**
- Device with wrong subnet mask flooding ARP
- Broadcast storm
- Multiple devices with same IP (ARP conflict)
- Malware causing ARP spoofing

**Diagnosis:**
```bash
# Linux - check ARP traffic
tcpdump -i eth0 arp | head -20

# Count ARP packets
tcpdump -i eth0 arp | wc -l

# Wireshark filter
arp.opcode == 1  (requests only)
arp.dst.proto_ipv4 == 192.168.1.0  (specific subnet)
```

---

## 🔒 ARP Security Issues

### 1️⃣ ARP Spoofing (ARP Cache Poisoning)

**Attack:** Attacker sends fake ARP replies to redirect traffic.

```
Real Network:
  Host A: 192.168.1.100 → MAC AA:BB:CC:DD:EE:FF
  Gateway: 192.168.1.1 → MAC AA:AA:AA:AA:AA:AA

Attacker sends:
  "I'm 192.168.1.1! Use my MAC: 66:66:66:66:66:66"

Host A's ARP Cache becomes:
  192.168.1.1 → 66:66:66:66:66:66 (WRONG!)

Result: Host A's traffic now goes to attacker instead of gateway!
```

**Attack Tools:**
- arpspoof
- Cain & Abel
- ettercap

**Detection:**
```bash
# Linux - watch for duplicate MACs
arp -a | grep <ip>  # If multiple MACs, it's poisoned!

# Wireshark - look for unusual ARP activity
arp.src.hw_mac == arp.dst.hw_mac  (sender and target have same MAC)
```

**Mitigation:**
- **Static ARP entries** (non-dynamic)
- **Dynamic ARP Inspection (DAI)** — Cisco switches validate ARP
- **Gratuitous ARP** — hosts re-announce themselves periodically
- **VLAN separation** — limit ARP broadcast scope
- **ARP tables on routers** — use static entries for critical devices
- **Encryption** — use TLS/SSL for sensitive traffic (defeats ARP spoofing for content)

---

### 2️⃣ ARP Broadcast Storm

**Attack:** Attacker floods network with thousands of ARP requests.

```
Attacker: 50,000 ARP requests per second
  "Who has 192.168.1.1?"
  "Who has 192.168.1.2?"
  "Who has 192.168.1.3?"
  ...

Result: 
  - Switch CPU overwhelmed
  - Network devices bogged down
  - Legitimate traffic delayed
```

**Detection:**
```bash
# Monitor ARP traffic
tcpdump -i eth0 'arp' -c 1000 | wc -l

# If > 1000 ARP packets in a few seconds → attack
```

**Mitigation:**
- Rate-limit ARP on switch ports
- Configure ARP inspection thresholds
- Deploy IPS/IDS

---

### 3️⃣ Gratuitous ARP Abuse

**Attack:** Attacker sends gratuitous ARP to claim ownership of IPs or MACs.

```
Attacker: "I'm 192.168.1.100 with MAC AA:BB:CC:DD:EE:FF"
          (updates everyone's ARP cache to attacker's MAC)

Or worse: "I'm the default gateway with my MAC!"
          (redirects all traffic to attacker)
```

**Mitigation:**
- Monitor gratuitous ARP frequency
- Validate gratuitous ARP against known devices
- Disable if not needed

---

## 🧪 Hands-On Labs

### Lab 1: Basic ARP Learning

**Objective:** Observe ARP request/reply in real-time

**Tools Needed:**
- Wireshark
- ping command
- arp utility

**Steps:**

1. **Clear ARP cache:**
   ```bash
   # Windows
   arp -d *
   
   # Linux
   ip neigh flush all  (requires root)
   ```

2. **Start Wireshark:**
   ```
   - Select your network interface
   - Start capture
   - Filter: arp (shows only ARP packets)
   ```

3. **Ping a host:**
   ```bash
   ping 192.168.1.50
   ```

4. **Observe in Wireshark:**
   ```
   Frame 1: ARP Request (broadcast)
     Who has 192.168.1.50?
     Sender: 192.168.1.100 → AA:BB:CC:DD:EE:FF
     
   Frame 2: ARP Reply (unicast)
     I have 192.168.1.50
     Sender: 192.168.1.50 → 11:22:33:44:55:66
     
   Frame 3-N: ICMP Echo Request/Reply
     (ping data, now that MAC is known)
   ```

5. **Check ARP cache:**
   ```bash
   arp -a
   # Shows: 192.168.1.50 → 11:22:33:44:55:66
   ```

---

### Lab 2: ARP Cache Timeout

**Objective:** Observe ARP cache entries expire

**Steps:**

1. **Ping a host:**
   ```bash
   ping 192.168.1.50
   ```

2. **Check ARP cache immediately:**
   ```bash
   arp -a
   # Shows: 192.168.1.50 [Active]
   ```

3. **Wait 5 minutes (no communication with host):**
   ```
   (Wait...)
   ```

4. **Check ARP cache again:**
   ```bash
   arp -a
   # Depending on OS:
   #   - Entry might still exist (TTL=120-300s)
   #   - Or entry removed (if TTL expired)
   ```

5. **Ping again:**
   ```bash
   ping 192.168.1.50
   # New ARP request sent (not in cache anymore)
   ```

---

### Lab 3: Gratuitous ARP Detection

**Objective:** Generate and observe gratuitous ARP

**Requirements:** Linux (arping tool)

**Steps:**

1. **Start Wireshark with ARP filter:**
   ```
   Filter: arp
   ```

2. **Send gratuitous ARP:**
   ```bash
   # Linux (requires root)
   arping -c 1 -A -I eth0 192.168.1.100
   # -c 1 = send 1 packet
   # -A = gratuitous ARP (both request and reply)
   # -I eth0 = use this interface
   # 192.168.1.100 = my own IP
   ```

3. **Observe in Wireshark:**
   ```
   ARP Request
     Sender IP: 192.168.1.100
     Target IP: 192.168.1.100 (SAME!)
     Sender MAC: AA:BB:CC:DD:EE:FF
     Target MAC: 00:00:00:00:00:00
     
   Message: "I'm 192.168.1.100 with MAC AA:BB:CC:DD:EE:FF"
   ```

4. **Check all devices' ARP cache:**
   ```bash
   arp -a
   # All hosts now have: 192.168.1.100 → AA:BB:CC:DD:EE:FF
   ```

---

### Lab 4: ARP Spoofing (Educational)

⚠️ **Legal Warning:** Only perform on YOUR OWN lab network!

**Objective:** Demonstrate ARP spoofing vulnerability

**Tools:** arpspoof (Linux) or similar

**Attack Scenario:**
```
Normal Traffic:
  Host A (192.168.1.100) ←→ Host B (192.168.1.50)

With Spoofing:
  Attacker sends: "I'm 192.168.1.50! Use my MAC!"
  Result: Host A's traffic redirected to attacker
```

**Lab Setup:**

1. **Three hosts on same LAN:**
   - Host A: 192.168.1.100
   - Host B: 192.168.1.50 (victim)
   - Attacker: 192.168.1.200

2. **Start attack (on Attacker):**
   ```bash
   arpspoof -i eth0 -t 192.168.1.100 192.168.1.50
   # Tell Host A that "I'm 192.168.1.50"
   ```

3. **Monitor with Wireshark (on Host A):**
   ```
   Before:
     192.168.1.50 → 11:22:33:44:55:66 (Host B's real MAC)
   
   After spoofing:
     192.168.1.50 → 66:77:88:99:AA:BB (Attacker's MAC!)
   ```

4. **Observe traffic redirect:**
   ```bash
   # On Attacker, capture traffic
   tcpdump -i eth0 -n src 192.168.1.100
   # Shows all of Host A's traffic!
   ```

5. **Stop attack:**
   ```bash
   Ctrl+C (to stop arpspoof)
   ```

---

### Lab 5: Dynamic ARP Inspection (DAI) on Cisco Switch

**Objective:** Prevent ARP spoofing with DAI

**Scenario:**
```
Switch with 3 hosts:
  Port 1: Host A (192.168.1.100, MAC AA:BB:CC:DD:EE:FF)
  Port 2: Host B (192.168.1.50, MAC 11:22:33:44:55:66)
  Port 3: Attacker (trying to spoof)
```

**Configuration:**

1. **Enable DHCP Snooping (prerequisite for DAI):**
   ```
   Switch(config)# ip dhcp snooping
   Switch(config)# ip dhcp snooping vlan 10
   Switch(config)# no ip dhcp snooping information option
   ```

2. **Enable DAI on VLAN:**
   ```
   Switch(config)# ip arp inspection vlan 10
   ```

3. **Set ports as trusted/untrusted:**
   ```
   Switch(config-if)# ip arp inspection trust        (gateway port)
   Switch(config-if)# no ip arp inspection trust     (access ports)
   ```

4. **Configure valid ARP entries (optional):**
   ```
   Switch(config)# arp access-list AUTHORIZED
   Switch(config-acl)# permit ip host 192.168.1.100 mac host aa.bb.cc.dd.ee.ff
   Switch(config-acl)# permit ip host 192.168.1.50 mac host 11.22.33.44.55.66
   ```

5. **Apply ACL to DAI:**
   ```
   Switch(config)# ip arp inspection filter AUTHORIZED vlan 10
   ```

6. **Test attack:**
   ```
   Attacker tries to spoof ARP
   
   Result: Switch drops malicious ARP
   Log: "%DAI-3-PACKET_RATE_EXCEEDED: Excessive ARP packets (5 packets in 200 ms)"
   ```

---

## 📋 CCNA Exam Focus Areas

### ✅ Must Know:

| Concept | Key Points |
|---------|-----------|
| **ARP Purpose** | Resolves IP → MAC on same LAN |
| **ARP Request** | Broadcast with OPER=1, THA=00:00:00:00:00:00 |
| **ARP Reply** | Unicast with OPER=2, filled THA |
| **ARP Packet Size** | 28 bytes for IPv4/Ethernet |
| **ARP Cache** | Dynamically learns, TTL ~120-300 seconds |
| **ARP Scope** | Local network only (same subnet) |
| **Gratuitous ARP** | SPA = TPA, used for announcements |
| **Proxy ARP** | Router responds for remote hosts |
| **No ARP on routers** | Routers use routing tables (consulted locally) |
| **ARP vs ICMP** | ARP for local MAC, ICMP (ping) for reachability |

---

### 📝 Sample CCNA Questions:

**Q1:** Which layer does ARP operate at?
**A:** Layer 2/3 hybrid (uses both MAC and IP)

**Q2:** What is the destination MAC in an ARP Request?
**A:** FF:FF:FF:FF:FF:FF (broadcast)

**Q3:** What OPER value indicates an ARP Reply?
**A:** 2

**Q4:** A device has an "incomplete" ARP entry for 192.168.1.50. What does this mean?
**A:** ARP request was sent but no reply received; MAC is unknown.

**Q5:** Which scenario requires ARP?
**A:** Two hosts on the same LAN communicating locally (need MAC addresses)

**Q6:** Do routers use ARP for forwarding?
**A:** Only to resolve the next-hop gateway's MAC. Final destination resolution uses routing tables on intermediate routers.

**Q7:** What is a Gratuitous ARP?
**A:** Device announces itself without being asked (SPA = TPA). Used for conflict detection.

**Q8:** How does a device behave if it receives an ARP Request for its own IP?
**A:** It sends an ARP Reply with its MAC address.

**Q9:** Can ARP work across different subnets?
**A:** No, ARP is broadcast-based and doesn't cross router boundaries.

**Q10:** What's the main vulnerability with ARP?
**A:** No authentication; anyone can claim any IP/MAC (ARP spoofing).

---

## 🔧 ARP Commands Reference

### Windows:

```bash
arp -a                  # Display ARP cache
arp -d 192.168.1.50     # Delete specific entry
arp -d *                # Clear entire ARP cache
arp -s 192.168.1.1 AA:BB:CC:DD:EE:FF  # Static entry
getmac /all             # Show MAC addresses
```

### Linux:

```bash
arp -a                  # Display ARP cache
arp -d 192.168.1.50     # Delete entry (needs root)
ip neighbor show        # Modern alternative to arp
ip neigh flush all      # Clear all entries (needs root)
arping -c 1 192.168.1.50  # Send ARP request manually
```

### Cisco Router:

```bash
show arp                # Display ARP table
clear arp-cache         # Clear ARP cache
show arp summary        # ARP statistics
debug arp               # Real-time ARP activity
show ip arp proxy       # Check proxy ARP status
```

### Wireshark Filters:

```
arp                          # All ARP packets
arp.opcode == 1              # ARP Requests only
arp.opcode == 2              # ARP Replies only
arp.src.proto_ipv4 == 192.168.1.0/24  # Specific subnet
arp.src.hw_mac == arp.dst.hw_mac      # Suspicious (same MAC)
arp.duplicate-address-frame  # Duplicate IP detected
```

---

## 🎯 Key Takeaways

✅ **ARP = IP to MAC translation on the same LAN**  
✅ **ARP Request = broadcast (to everyone)**  
✅ **ARP Reply = unicast (to requester only)**  
✅ **ARP Cache = learned entries expire in ~2-5 minutes**  
✅ **ARP only works locally** — doesn't cross routers  
✅ **Gratuitous ARP** = device announces itself  
✅ **Proxy ARP** = router replies for remote hosts  
✅ **ARP spoofing is a real security threat** — use DAI/static entries to mitigate  
✅ **ARP is stateless** — no authentication, no security  
✅ **Modern networks use DHCP + gratuitous ARP for efficiency**

---

**For your GitHub repo:** Save this as `3.ARP-Protocol.md` in your Networking-Basics folder.
