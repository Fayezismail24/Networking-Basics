# VLAN Best Practices & Design Patterns

---

## VLAN Design Philosophy

### Principle 1: Segment by Function, Not by Location

❌ **Bad VLAN Design**
```
Building A VLANs:
├─ VLAN 10: Building A (all devices)
│  ├─ Workstations
│  ├─ Servers
│  ├─ Printers
│  └─ Phones
└─ VLAN 20: Building B (all devices)
```

When a printer fails in Building A, you re-IP every device in VLAN 10.

✅ **Good VLAN Design**
```
Function-based VLANs (location-independent):
├─ VLAN 10: Management (IT, SNMP, SSH)
├─ VLAN 20: Workstations (user PCs, data)
├─ VLAN 30: Servers (databases, apps)
├─ VLAN 40: Printers (managed print network)
└─ VLAN 50: Phones (VoIP)
```

If a printer fails, only VLAN 40 is affected. Users in other VLANs unaffected.

---

## VLAN ID Allocation Strategy

### Recommended VLAN ID Ranges

```
1          Default VLAN (reserved, do NOT use for devices)
10–49      Management & Infrastructure
│  ├─ 10: Mgmt (switches, routers, firewalls)
│  ├─ 20: IT support / helpdesk PCs
│  └─ 30: SNMP, monitoring, logging
50–99      Workstations & Clients
│  ├─ 50: Engineering workstations
│  ├─ 60: HR / Finance workstations
│  └─ 70: General office workstations
100–149    Servers & Infrastructure
│  ├─ 100: Database servers
│  ├─ 110: Web servers
│  ├─ 120: Application servers
│  └─ 130: File servers
150–199    Voice (VoIP) & Collaboration
│  ├─ 150: IP phones
│  ├─ 160: Video conferencing
│  └─ 170: Unified communications
200–249    IoT & Specialized
│  ├─ 200: IoT devices (cameras, sensors)
│  ├─ 210: Building management systems
│  └─ 220: Guest WiFi / BYOD
250–999    Reserved for future expansion
1000–1005  Extended VLANs (if needed, rare in CCNA)
```

### Why This Matters
- Easy to remember (e.g., "workstations are in the 50s")
- Room for growth (each segment has 50 VLAN IDs)
- Logical organization aids troubleshooting
- Follows industry conventions

---

## VLAN Naming Convention

### Standard Naming Pattern

```
<FUNCTION>_<LOCATION>_<TIER>

Examples:
├─ MGMT_HQ_INFRA       (Management, Headquarters, Infrastructure)
├─ USER_FLOOR3_OFFICE  (User workstations, Floor 3, Office area)
├─ SRV_DATACENTER_PROD (Servers, Datacenter, Production)
├─ VOIP_HQ_PRIMARY     (VoIP, HQ, Primary system)
└─ GUEST_ALL_OPEN      (Guest network, All locations, Open access)
```

### Simpler Pattern (Small Networks)

```
<FUNCTION>-<NUMBER>

Examples:
├─ MGMT-10
├─ USER-50
├─ PHONE-150
├─ GUEST-220
└─ IOT-200
```

### Switch Configuration

```
vlan 10
  name MGMT-10
  exit

vlan 50
  name USER-WORKSTATIONS
  exit

vlan 100
  name SRV-DATACENTER-PROD
  exit
```

---

## VLAN Security Best Practices

### 1. Disable VLAN 1

VLAN 1 is used by many legacy systems and unmanaged devices. Avoid using it.

```
configure terminal

! Create a separate VLAN for management
vlan 10
  name Management
  exit

! Set all access ports to a non-1 VLAN
interface range GigabitEthernet0/0/1-47
  switchport access vlan 10  ← NOT VLAN 1
  exit

exit
```

---

### 2. Disable DTP and Manual Trunk Configuration

DTP introduces security risks (VLAN hopping). Disable globally.

```
configure terminal

! Disable DTP on all access ports
interface range GigabitEthernet0/0/1-47
  switchport mode access
  switchport nonegotiate
  exit

! Manually configure trunks (not dynamic)
interface GigabitEthernet0/0/48
  switchport mode trunk
  switchport nonegotiate  ← Explicit = secure
  switchport trunk native vlan 999  ← Unused VLAN
  switchport trunk allowed vlan 1,10,20,30
  exit

exit
```

---

### 3. Change Native VLAN to Unused VLAN

Default native VLAN 1 is an attack vector for native VLAN hopping.

```
configure terminal

interface GigabitEthernet0/0/48
  switchport trunk native vlan 999
  exit

! VLAN 999 must NOT be used on any access port
! (No devices should be in VLAN 999)

exit
```

**Why?** Untagged frames on the trunk default to native VLAN. If attacker sends untagged frame, it lands in VLAN 999 (unused) = isolated.

---

### 4. Enable Port Security (Per-VLAN)

Restrict MAC addresses per access port to prevent rogue device connection.

```
configure terminal

interface range GigabitEthernet0/0/1-47
  switchport port-security
  switchport port-security maximum 2  ← Allow 2 MACs (PC + phone)
  switchport port-security mac-address sticky  ← Learn dynamically
  switchport port-security violation shutdown  ← Disable on violation
  exit

exit
```

---

### 5. Isolate User VLANs from IT Infrastructure

Use separate IP address ranges.

```
VLAN 10 (MGMT): 192.168.1.0/24    ← Infrastructure only
VLAN 20 (USER): 10.1.0.0/16       ← Users only (different class)
VLAN 30 (SRV): 172.16.0.0/16      ← Servers only
```

**Rationale**: If user VLAN is compromised, attacker must change IP class to reach infrastructure.

---

### 6. Use VACLs (VLAN Access Control Lists) for Micro-Segmentation

Block traffic between VLANs at Layer 2 (more restrictive than Layer 3 routing).

```
configure terminal

! Create VACL: Block user VLAN ↔ server VLAN
ip access-list extended BLOCK-USER-SRV
  deny ip 10.1.0.0 0.0.255.255 172.16.0.0 0.0.255.255
  permit ip any any
  exit

vlan access-map ISOLATE 10
  match ip address BLOCK-USER-SRV
  action drop
  exit

vlan filter ISOLATE vlan-list 20,100  ← Apply to VLAN 20 & 100

exit
```

⚠️ **Advanced**: VACL is complex; use for high-security networks only.

---

### 7. Configure VLAN Management IP on Unused VLAN

Never manage switch via user-accessible VLAN (e.g., VLAN 20).

```
configure terminal

! ✓ Good: Mgmt interface on dedicated VLAN 10
interface Vlan10
  ip address 192.168.1.1 255.255.255.0
  exit

! ✗ Bad: DO NOT do this:
! interface Vlan20
!   ip address 10.1.0.1 255.255.255.0  ← Users can SSH here!

exit
```

---

## VLAN Design for Multi-Site Networks

### Site-to-Site VLAN Consistency

Maintain same VLAN IDs across all sites for operational simplicity.

```
Site A (HQ)              Site B (Branch)
├─ VLAN 10: MGMT        ├─ VLAN 10: MGMT
├─ VLAN 20: USER        ├─ VLAN 20: USER
├─ VLAN 30: SRV         ├─ VLAN 30: SRV
└─ Trunk 192.168.1.0/24 └─ Trunk 10.1.0.0/24

All sites use VLAN 10 for management (same ID, different subnets)
→ Easier troubleshooting, consistent naming
```

### Subnet Allocation (Multi-Site)

```
VLAN 10 (MGMT):
├─ Site A: 192.168.10.0/24
├─ Site B: 192.168.20.0/24
└─ Site C: 192.168.30.0/24
→ Same VLAN ID, unique subnets

VLAN 20 (USER):
├─ Site A: 10.1.0.0/24
├─ Site B: 10.2.0.0/24
└─ Site C: 10.3.0.0/24
```

---

## VLAN Configuration Backup & Documentation

### Backup Running-Config

```
copy running-config startup-config
copy running-config tftp://192.168.1.10/C3560-backup.txt
```

### Extract VLAN Config

```
show running-config | include vlan
show running-config interface | include vlan
```

### Document Template

```markdown
# VLAN Configuration - Site A

## VLAN Summary
| ID  | Name            | Subnet         | Ports        | Purpose      |
|-----|-----------------|----------------|--------------|--------------|
| 1   | default         | N/A            | Disabled     | Reserved     |
| 10  | MGMT-10         | 192.168.10.0/24| Gi0/0/1-4   | Management   |
| 20  | USER-WORKSTNS   | 10.1.0.0/24    | Gi0/0/11-40 | Workstations |
| 30  | SRV-PROD        | 172.16.0.0/24  | Gi0/0/41-45 | Servers      |
| 150 | PHONE-VOIP      | 10.150.0.0/24  | Gi0/0/46-47 | IP Phones    |

## Trunk Configuration
| Port    | Native VLAN | Allowed VLANs | Destination   |
|---------|-------------|---------------|---------------|
| Gi0/0/48| 999         | 1,10,20,30,150| Router-HQ     |

## Access Port Examples
Gi0/0/1  → VLAN 10 (MGMT)
Gi0/0/11 → VLAN 20 (USER)
Gi0/0/41 → VLAN 30 (SRV)
```

---

## Common Design Mistakes

### Mistake 1: Too Many VLANs

❌ **Over-segmentation**
```
VLAN 100: Engineering Team A
VLAN 101: Engineering Team B
VLAN 102: Engineering Team C
...
VLAN 150: Engineering Team D
```

→ Difficult to manage, increased routing complexity, STP issues.

✅ **Correct**
```
VLAN 50: Engineering (all teams)
→ Teams segmented at application/firewall level, not VLAN
```

---

### Mistake 2: Using VLAN 1 for Everything

❌ **Bad**
```
All devices → VLAN 1 (default)
No logical segregation
```

✅ **Correct**
```
Management → VLAN 10
Users → VLAN 20
Servers → VLAN 30
```

---

### Mistake 3: Not Planning IP Subnets

❌ **Bad**
```
VLAN 10: 192.168.0.0/24  (256 hosts)
VLAN 20: 192.168.0.0/24  (Same subnet!)
→ Routing conflicts, IP overlap
```

✅ **Correct**
```
VLAN 10: 192.168.10.0/24
VLAN 20: 192.168.20.0/24
VLAN 30: 192.168.30.0/24
→ Each VLAN has unique subnet
```

---

## Checklist: VLAN Implementation Plan

### Design Phase
- [ ] Define VLAN purpose & IP subnets
- [ ] Allocate VLAN IDs per company standard
- [ ] Design trunk topology (which ports)
- [ ] Plan native VLAN (non-default)
- [ ] Document in centralized wiki/repo

### Configuration Phase
- [ ] Create VLANs with descriptive names
- [ ] Assign access ports to VLANs (use ranges)
- [ ] Configure trunks (explicit mode, not DTP)
- [ ] Set native VLAN on trunks (unused VLAN)
- [ ] Filter allowed VLANs on trunks
- [ ] Enable inter-VLAN routing (SVI or router-on-stick)

### Security Phase
- [ ] Disable DTP (`switchport nonegotiate`)
- [ ] Remove VLAN 1 from production
- [ ] Enable port security (MAC limiting)
- [ ] Configure SVI management IP (VLAN 10 only)
- [ ] Add ACLs for sensitive VLAN access

### Testing Phase
- [ ] Verify intra-VLAN connectivity (ping same VLAN)
- [ ] Verify inter-VLAN routing (ping different VLAN)
- [ ] Test trunk status and allowed VLANs
- [ ] Verify STP not blocking user traffic
- [ ] Document any design changes

### Operational Phase
- [ ] Backup running-config to TFTP/GitHub
- [ ] Document VLAN assignments in spreadsheet/wiki
- [ ] Monitor VLAN creation/deletion via Syslog
- [ ] Schedule quarterly VLAN cleanup (remove unused)
- [ ] Review security policies annually

---

## Exam Callouts: Best Practices

| Topic | Guideline |
|-------|-----------|
| **Native VLAN** | Change from 1 to unused VLAN (e.g., 999) |
| **VLAN IDs** | Use 10–49 (mgmt), 50–99 (users), 100–149 (servers) |
| **DTP** | Disable globally: `switchport nonegotiate` |
| **VLAN 1** | Never use for user or device communication |
| **Port Security** | Enable on access ports: `switchport port-security` |
| **Documentation** | Maintain VLAN spreadsheet + running-config backup |

---

**End of VLAN Documentation**
