# Network Bridge Device

A focused reference on the **network bridge as a physical or logical device** — its hardware, internal architecture, how it processes frames, and where it fits in modern networks.

---

## Table of Contents

1. [Definition](#1-definition)
2. [Bridge Device Architecture](#2-bridge-device-architecture)
3. [Types of Bridge Devices](#3-types-of-bridge-devices)
4. [How a Bridge Device Processes a Frame](#4-how-a-bridge-device-processes-a-frame)
5. [Bridge Device Components](#5-bridge-device-components)
6. [Bridge vs. Switch vs. Router (Device Comparison)](#6-bridge-vs-switch-vs-router-device-comparison)
7. [Transparent Bridging (IEEE 802.1D)](#7-transparent-bridging-ieee-8021d)
8. [Source-Route Bridging (SRB)](#8-source-route-bridging-srb)
9. [Translational Bridging](#9-translational-bridging)
10. [Bridge Device in Modern Networks](#10-bridge-device-in-modern-networks)
11. [Physical Bridge Device Examples](#11-physical-bridge-device-examples)
12. [Quick Reference](#12-quick-reference)

---

## 1. Definition

A **network bridge device** is a Layer 2 networking device that connects two or more LAN segments into a single broadcast domain. It makes forwarding decisions based on **MAC addresses** and maintains a **Forwarding Database (FDB)** — also called a bridge table or CAM table.

```
┌──────────────────────────────────────────────┐
│              NETWORK BRIDGE DEVICE           │
│                                              │
│  Port 1 ──── [ FDB / MAC Table ] ──── Port 2│
│                     │                        │
│              [ STP Engine ]                  │
└──────────────────────────────────────────────┘
      │                                   │
  Segment A                           Segment B
(192.168.1.x)                       (192.168.1.x)
  Same subnet — bridged, not routed
```

> A bridge device **does not** change IP addresses or subnet boundaries. Both connected segments share the same Layer 3 network.

---

## 2. Bridge Device Architecture

```
                    ┌─────────────────────────────────┐
                    │         BRIDGE DEVICE            │
                    │                                  │
  Port 1 (e0) ──►  │  ┌──────────┐  ┌─────────────┐  │  ◄── Port 2 (e1)
                    │  │  Input   │  │   Output    │  │
  Port 3 (e2) ──►  │  │ Pipeline │─►│   Pipeline  │  │  ◄── Port 4 (e3)
                    │  └──────────┘  └─────────────┘  │
                    │        │              ▲          │
                    │        ▼              │          │
                    │  ┌─────────────────────────┐    │
                    │  │  Forwarding Database     │    │
                    │  │  (MAC → Port mapping)    │    │
                    │  └─────────────────────────┘    │
                    │        │                         │
                    │        ▼                         │
                    │  ┌─────────────────────────┐    │
                    │  │  STP / RSTP Engine       │    │
                    │  │  (Loop prevention)       │    │
                    │  └─────────────────────────┘    │
                    │                                  │
                    │  ┌─────────────────────────┐    │
                    │  │  Management Plane        │    │
                    │  │  (CLI / SNMP / Console)  │    │
                    │  └─────────────────────────┘    │
                    └─────────────────────────────────┘
```

---

## 3. Types of Bridge Devices

### 3.1 Local Bridge
Connects two segments **in the same physical location**. Both ports are on the same device.

```
[LAN A] ──── [Bridge] ──── [LAN B]
              (local)
```

### 3.2 Remote Bridge (WAN Bridge)
Two bridge devices connected over a **WAN link** (serial, T1, leased line). Used to extend a LAN across distance.

```
[LAN A] ──── [Bridge A] ════ WAN ════ [Bridge B] ──── [LAN B]
```

### 3.3 Wireless Bridge
Connects two LAN segments over a **wireless link** (IEEE 802.11). Common for building-to-building connectivity.

```
[LAN A] ──── [AP/Bridge A] )))  ((( [AP/Bridge B] ──── [LAN B]
                           RF Link
```

### 3.4 Multi-Port Bridge (Ethernet Switch)
A modern switch **is** a multi-port bridge with hardware ASICs.

```
[Host 1] ──┐
[Host 2] ──┤
[Host 3] ──┤── [Multi-Port Bridge] ──── Uplink
[Host 4] ──┤
[Host 5] ──┘
```

### 3.5 Translation Bridge
Bridges **between different Layer 2 technologies** (e.g., Ethernet ↔ Token Ring). Largely obsolete.

---

## 4. How a Bridge Device Processes a Frame

```
Frame arrives on Port X
        │
        ▼
┌───────────────────┐
│  1. LEARN         │  Source MAC → add/refresh entry in FDB for Port X
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│  2. LOOKUP        │  Look up Destination MAC in FDB
└────────┬──────────┘
         │
    ┌────┴──────────────────────────────────┐
    │                                       │
    ▼                                       ▼
Destination MAC KNOWN                Destination MAC UNKNOWN
(FDB has an entry)                   (or Broadcast/Multicast)
    │                                       │
    ▼                                       ▼
┌──────────────────┐             ┌──────────────────────┐
│  3a. FORWARD     │             │  3b. FLOOD           │
│  Out the port    │             │  Out ALL ports       │
│  in the FDB      │             │  EXCEPT Port X       │
└──────────────────┘             └──────────────────────┘
    │                                       │
    └─────────────────┬─────────────────────┘
                      ▼
              ┌───────────────┐
              │  4. FILTER    │  If src port == dst port → DROP
              │  (same port)  │  (both hosts on same segment)
              └───────────────┘
```

### Special Cases

| Frame Type | Action |
|---|---|
| Unicast, destination known | Forward to specific port |
| Unicast, destination unknown | Flood all ports except ingress |
| Broadcast (FF:FF:FF:FF:FF:FF) | Flood all ports except ingress |
| Multicast | Flood all ports except ingress (unless IGMP snooping) |
| Same-port src/dst | Filter (drop) |

---

## 5. Bridge Device Components

| Component | Function |
|---|---|
| **Ports / Interfaces** | Physical connections to LAN segments |
| **FDB (Forwarding Database)** | MAC-to-port table, aged out (default 300 s) |
| **STP Engine** | Detects and blocks loops; elects root bridge |
| **Frame Buffer** | Temporary queue for in-flight frames |
| **CPU / Control Plane** | Manages STP, FDB aging, management protocols |
| **ASIC (in switches)** | Hardware-accelerated frame forwarding |
| **Management Interface** | Console, Telnet/SSH, SNMP, HTTP |

### FDB Entry Lifecycle

```
Frame arrives with new source MAC
          │
          ▼
    Entry added to FDB
    (MAC, Port, Timestamp)
          │
          ▼
    Timer starts (default 300 s)
          │
    ┌─────┴──────────────────┐
    │                        │
 Traffic seen            No traffic
 → Timer reset           → Entry aged out
                         → Deleted from FDB
```

---

## 6. Bridge vs. Switch vs. Router (Device Comparison)

| Property | Bridge Device | Switch | Router |
|---|---|---|---|
| OSI Layer | 2 | 2 (or 3) | 3 |
| Forwarding basis | MAC address | MAC address | IP address |
| Port count | 2–4 (typically) | 8–48+ | 1–8 (typically) |
| Hardware forwarding | Software (mostly) | ASIC | ASIC / software |
| Broadcast domain | 1 shared | 1 per VLAN | 1 per interface |
| Collision domain | Per port | Per port | Per interface |
| VLAN support | Rare | Standard | Via sub-interfaces |
| Loop prevention | STP | STP / RSTP | N/A (routed) |
| IP awareness | No | Only in L3 mode | Yes |
| Speed | 10/100 Mbps era | Up to 400 Gbps+ | Line-rate routing |
| Modern relevance | Legacy / niche | Universal | Universal |

---

## 7. Transparent Bridging (IEEE 802.1D)

The dominant bridging standard for Ethernet networks. Called "transparent" because end hosts are **unaware** of the bridge's presence.

### Key Behaviors

- **Learning** — populates FDB from source MACs of incoming frames.
- **Forwarding** — sends frames to the correct port per FDB.
- **Flooding** — sends unknown frames to all ports except ingress.
- **Filtering** — drops frames where src and dst are on the same port.
- **Aging** — removes stale FDB entries after the aging timer expires.

### STP Integration

IEEE 802.1D mandates STP to prevent loops created by redundant bridge paths.

```
Root Bridge elected (lowest Bridge ID)
        │
        ├── Root Port selected per non-root bridge (best path to root)
        │
        └── Designated Port selected per segment (one per link)
                │
                └── All other ports → Blocked
```

---

## 8. Source-Route Bridging (SRB)

Used in **Token Ring** networks (IBM). The source host embeds the full path (route) in the frame header. Bridges simply follow the embedded route rather than maintaining their own FDB.

| Property | Transparent Bridging | Source-Route Bridging |
|---|---|---|
| Path decision | Bridge (FDB lookup) | Source host (route in frame) |
| Technology | Ethernet | Token Ring |
| Host awareness | None | Host must know the route |
| Standard | IEEE 802.1D | IEEE 802.5 |
| Modern use | Active | Obsolete |

---

## 9. Translational Bridging

Bridges two **different Layer 2 technologies** by translating frame formats.

```
[ Ethernet Frame ]                    [ Token Ring Frame ]
  DA | SA | Type | Data | FCS  ──►   AC | FC | DA | SA | RIF | Data | FCS
                         ▲
               Translation Bridge
               (converts frame format,
                bit ordering, MTU)
```

Common historical use cases:
- Ethernet ↔ Token Ring
- Ethernet ↔ FDDI

> Largely obsolete. Token Ring and FDDI are no longer deployed in modern networks.

---

## 10. Bridge Device in Modern Networks

Pure bridge devices (2-port, hardware appliances) are rare today. Bridging functionality lives on in:

| Context | Where Bridging Exists Today |
|---|---|
| **Ethernet switch** | Every switch is a multi-port bridge |
| **Wireless AP** | AP bridges wireless clients to wired LAN |
| **Wireless bridge mode** | Dedicated AP-to-AP building links |
| **Hypervisor vSwitch** | VMware vSwitch, Linux br0, OVS bridge VMs to physical NIC |
| **Container networking** | Docker `docker0`, Linux bridge per namespace |
| **DSL/Cable modem** | Bridge mode passes PPPoE/DHCP to router |
| **Cisco IRB** | Router acts as bridge for specific protocols |
| **SD-WAN / MPLS PE** | L2VPN bridges remote LANs over WAN |

### Modem/CPE Bridge Mode

A common real-world scenario — ISP modem set to **bridge mode** passes the public IP directly to the downstream router:

```
Internet ──── [Modem in Bridge Mode] ──── [Router] ──── LAN
                 (no NAT, no DHCP)         (NAT, DHCP)
```

---

## 11. Physical Bridge Device Examples

| Device / Product | Type | Era |
|---|---|---|
| DEC LAN Bridge 100 | Local Ethernet bridge | 1984 |
| Cisco Catalyst 1900 | Multi-port bridge / early switch | 1990s |
| 3Com LinkBuilder | Local bridge | 1990s |
| Cisco 2924 | L2 switch (bridge successor) | Late 1990s |
| Ubiquiti NanoStation | Wireless bridge | 2010s–present |
| Cisco Aironet (bridge mode) | Wireless bridge | 2000s–present |
| MikroTik RB series (bridge mode) | Software-defined bridge | 2010s–present |
| Any Ethernet switch | Multi-port bridge | Present |

---

## 12. Quick Reference

### Frame Decision Table

| Destination MAC | In FDB? | Action |
|---|---|---|
| Unicast | Yes | Forward to mapped port |
| Unicast | No | Flood all ports except ingress |
| Broadcast | — | Flood all ports except ingress |
| Multicast | — | Flood (or selective w/ IGMP snooping) |
| Same segment | — | Filter (drop) |

### Bridge Device Facts

| Parameter | Default / Typical Value |
|---|---|
| FDB aging timer | 300 seconds |
| STP Hello interval | 2 seconds |
| STP Max Age | 20 seconds |
| STP Forward Delay | 15 seconds |
| Default bridge priority | 32768 |
| Minimum bridge priority | 0 (root forced) |
| Bridge priority increment | 4096 |

### Key Standards

| Standard | Description |
|---|---|
| IEEE 802.1D | Transparent bridging + STP |
| IEEE 802.1w | Rapid STP (RSTP) |
| IEEE 802.1s | Multiple STP (MSTP) |
| IEEE 802.1Q | VLAN tagging (used with bridges/switches) |
| IEEE 802.5 | Token Ring / Source-Route Bridging |

---

*Part of the networking study repository.*
