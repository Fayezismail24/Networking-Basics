# Data Link Layer (OSI Layer 2)

## What is the Data Link Layer?

The Data Link Layer is the second layer of the OSI model.
It sits between the Physical Layer (Layer 1) and the Network Layer (Layer 3).

Its job is to take raw bits from Layer 1 and organize them into
frames, then deliver those frames between directly connected devices
on the same network segment.

Layer 2 does not care about IP addresses — it works with MAC addresses.

---

## Responsibilities

- Framing — encapsulating data into frames
- MAC addressing — identifying source and destination on the local segment
- Error detection — catching bit errors introduced by Layer 1
- Flow control — preventing a fast sender from overwhelming a slow receiver
- Media access control — deciding which device can transmit at a given time

---

## Two Sub-Layers

The Data Link Layer is split into two sub-layers:

### LLC — Logical Link Control (Upper)

| Detail | Value |
|--------|-------|
| Defined by | IEEE 802.2 |
| Role | Interface between Layer 2 and Layer 3 |
| Function | Identifies which Layer 3 protocol is carried (IPv4, IPv6, etc.) |

### MAC — Media Access Control (Lower)

| Detail | Value |
|--------|-------|
| Defined by | IEEE 802.3 (Ethernet), 802.11 (Wi-Fi) |
| Role | Hardware addressing and media access |
| Function | Controls how devices share the physical medium |

---

## MAC Address

A MAC address is a 48-bit hardware address burned into the NIC.
It is used to identify devices on the same local network segment.

### Format

```
00:1A:2B:3C:4D:5E
└─────┘ └─────────┘
  OUI     Device ID
```

| Field | Size | Description |
|-------|------|-------------|
| OUI | 24 bits (3 bytes) | Organizationally Unique Identifier — assigned to the manufacturer |
| Device ID | 24 bits (3 bytes) | Unique identifier assigned by the manufacturer per device |

### Types of MAC Addresses

| Type | Example | Description |
|------|---------|-------------|
| Unicast | 00:1A:2B:3C:4D:5E | One specific device |
| Broadcast | FF:FF:FF:FF:FF:FF | All devices on the segment |
| Multicast | 01:00:5E:xx:xx:xx | A group of devices |

> MAC addresses are written in hex.
> The broadcast address FF:FF:FF:FF:FF:FF is sent to every device on the LAN.

---

## Ethernet Frame Structure

When data is passed down from Layer 3, Layer 2 wraps it in an Ethernet frame.

```
┌──────────┬─────────┬──────────┬──────┬──────────────┬─────┐
│ Preamble │  Dest   │  Source  │ Type │   Payload    │ FCS │
│  8 bytes │ MAC 6B  │  MAC 6B  │  2B  │ 46–1500 bytes│  4B │
└──────────┴─────────┴──────────┴──────┴──────────────┴─────┘
```

| Field | Size | Description |
|-------|------|-------------|
| Preamble | 8 bytes | Synchronizes the receiver clock — 7 bytes preamble + 1 byte SFD |
| Destination MAC | 6 bytes | MAC address of the receiving device |
| Source MAC | 6 bytes | MAC address of the sending device |
| EtherType / Length | 2 bytes | Identifies Layer 3 protocol (0x0800 = IPv4, 0x86DD = IPv6, 0x0806 = ARP) |
| Payload | 46–1500 bytes | The actual data from upper layers |
| FCS | 4 bytes | Frame Check Sequence — CRC error detection |

> Minimum frame size = 64 bytes. Maximum = 1518 bytes (without VLAN tag).
> Frames smaller than 64 bytes are called runts and are discarded.
> Frames larger than 1518 bytes are called giants and are discarded.

---

## EtherType Common Values

| EtherType | Protocol |
|-----------|----------|
| 0x0800 | IPv4 |
| 0x86DD | IPv6 |
| 0x0806 | ARP |
| 0x8100 | 802.1Q VLAN tag |
| 0x8847 | MPLS |

---

## Error Detection — FCS

The FCS (Frame Check Sequence) uses CRC (Cyclic Redundancy Check).

| Detail | Value |
|--------|-------|
| Size | 4 bytes |
| Algorithm | CRC-32 |
| How it works | Sender calculates CRC on the frame and appends it. Receiver recalculates and compares. |
| On mismatch | Frame is discarded silently — Layer 2 does not retransmit |

> Layer 2 detects errors but does not correct them.
> Error recovery is handled by upper layers (TCP at Layer 4).

---

## Media Access Control Methods

Multiple devices sharing the same medium need rules for who transmits when.

| Method | Used In | How It Works |
|--------|---------|--------------|
| CSMA/CD | Wired Ethernet (half-duplex) | Listen before transmit, detect collision, back off and retry |
| CSMA/CA | Wi-Fi (802.11) | Listen before transmit, avoid collision using random backoff |
| Token Passing | Token Ring (legacy) | Only the device holding the token can transmit |

> Modern switches use full-duplex — CSMA/CD is not needed.
> CSMA/CD is still a CCNA exam topic for legacy and half-duplex scenarios.

---

## Half-Duplex vs Full-Duplex

| Mode | Description | Collision Domain |
|------|-------------|-----------------|
| Half-duplex | One direction at a time | Yes — CSMA/CD required |
| Full-duplex | Both directions simultaneously | No — dedicated switch port |

> Hubs = half-duplex. Switches = full-duplex per port.
> A duplex mismatch (one side full, other side half) causes collisions and poor performance.

---

## Layer 2 Devices

### Switch

| Feature | Detail |
|---------|--------|
| Operates at | Layer 2 |
| Uses | MAC address table (CAM table) |
| Forwarding logic | Learns source MAC, forwards to destination MAC port only |
| Collision domain | One per port — no collisions in full-duplex |
| Broadcast domain | One per VLAN |

### Hub (Legacy)

| Feature | Detail |
|---------|--------|
| Operates at | Layer 1 |
| Uses | No intelligence — repeats bits to all ports |
| Collision domain | All ports share one collision domain |
| Broadcast domain | One for all ports |

> Hubs are Layer 1 devices. Switches are Layer 2 devices.
> Never confuse the two on the exam.

### Bridge (Legacy)

| Feature | Detail |
|---------|--------|
| Operates at | Layer 2 |
| Ports | Typically 2 ports |
| Function | Segments collision domains — predecessor to the switch |

---

## MAC Address Table (CAM Table)

A switch learns MAC addresses dynamically by reading the source MAC
of incoming frames and recording which port they arrived on.

### Learning Process

```
1. Frame arrives on port Gi0/1 with source MAC AA:BB:CC:DD:EE:FF
2. Switch records: AA:BB:CC:DD:EE:FF → Gi0/1 in the MAC table
3. Switch checks destination MAC in the table
4. If found → forwards only to that port (unicast)
5. If not found → floods to all ports except source (unknown unicast flood)
```

### Cisco Command — View MAC Table

```bash
SW1# show mac address-table
```

### MAC Table Entry Types

| Type | Description |
|------|-------------|
| Dynamic | Learned automatically — ages out after 300 seconds by default |
| Static | Manually configured — never ages out |
| Secure | Configured via port security |

---

## ARP — Address Resolution Protocol

ARP operates at the boundary of Layer 2 and Layer 3.
It resolves an IP address to a MAC address so a frame can be sent.

### ARP Process

```
1. PC1 wants to send data to 192.168.1.2 but does not know its MAC
2. PC1 sends ARP Request — broadcast FF:FF:FF:FF:FF:FF
   "Who has 192.168.1.2? Tell 192.168.1.1"
3. PC2 (192.168.1.2) replies with ARP Reply — unicast back to PC1
   "192.168.1.2 is at AA:BB:CC:DD:EE:FF"
4. PC1 stores the result in its ARP cache
5. PC1 can now build the Ethernet frame with the correct destination MAC
```

### Cisco Commands

```bash
R1# show arp
PC> arp -a
```

---

## VLANs at Layer 2

VLANs (Virtual LANs) segment a switch into multiple broadcast domains at Layer 2.

| Feature | Detail |
|---------|--------|
| Standard | IEEE 802.1Q |
| Tag size | 4 bytes added to the Ethernet frame |
| VLAN ID range | 1–4094 |
| Default VLAN | VLAN 1 |
| Native VLAN | Untagged traffic on a trunk port (default VLAN 1) |

### 802.1Q Frame Tag

```
┌──────────┬──────────┬──────────┬──────────┬─────────────────┬─────┐
│ Dest MAC │  Src MAC │  0x8100  │ VLAN Tag │    EtherType    │ ... │
│  6 bytes │  6 bytes │  2 bytes │  2 bytes │     2 bytes     │     │
└──────────┴──────────┴──────────┴──────────┴─────────────────┴─────┘
                         TPID         TCI
                                  (PCP 3b | DEI 1b | VID 12b)
```

| Field | Size | Description |
|-------|------|-------------|
| TPID | 2 bytes | Always 0x8100 — identifies this as an 802.1Q frame |
| PCP | 3 bits | Priority Code Point — QoS marking |
| DEI | 1 bit | Drop Eligible Indicator |
| VID | 12 bits | VLAN ID — 0 to 4095 (usable: 1–4094) |

---

## Port Types on a Switch

| Port Type | Description | Carries |
|-----------|-------------|---------|
| Access port | Belongs to one VLAN | Untagged frames |
| Trunk port | Carries multiple VLANs | Tagged frames (802.1Q) |
| Native VLAN port | Untagged traffic on a trunk | No tag — default VLAN 1 |

---

## Spanning Tree Protocol (STP)

STP prevents Layer 2 loops in redundant switch topologies.

| Detail | Value |
|--------|-------|
| Standard | IEEE 802.1D (classic STP) |
| Improved versions | RSTP 802.1w, PVST+, Rapid PVST+ (Cisco) |
| Problem it solves | Broadcast storms caused by switching loops |
| How it works | Elects a Root Bridge, blocks redundant paths |

### STP Port States (Classic 802.1D)

| State | Forwards Frames | Learns MACs | Description |
|-------|-----------------|-------------|-------------|
| Blocking | No | No | Receives BPDUs only |
| Listening | No | No | Transitioning — sends/receives BPDUs |
| Learning | No | Yes | Builds MAC table, no forwarding yet |
| Forwarding | Yes | Yes | Normal operation |
| Disabled | No | No | Administratively shut down |

---

## Key Layer 2 Protocols Summary

| Protocol | Standard | Purpose |
|----------|----------|---------|
| Ethernet | IEEE 802.3 | Wired LAN framing and MAC |
| Wi-Fi | IEEE 802.11 | Wireless LAN |
| ARP | RFC 826 | IP to MAC resolution |
| 802.1Q | IEEE 802.1Q | VLAN tagging on trunks |
| STP | IEEE 802.1D | Loop prevention |
| RSTP | IEEE 802.1w | Faster loop prevention |
| CDP | Cisco proprietary | Cisco device discovery |
| LLDP | IEEE 802.1AB | Vendor-neutral device discovery |

---

## Layer 1 vs Layer 2 vs Layer 3 — Boundary Reference

| Layer | Name | Address Used | Device | PDU |
|-------|------|-------------|--------|-----|
| Layer 1 | Physical | None | Hub, Repeater | Bits |
| Layer 2 | Data Link | MAC address | Switch, Bridge | Frame |
| Layer 3 | Network | IP address | Router | Packet |

---

## Summary

- Layer 2 organizes bits into frames and delivers them between directly connected devices
- MAC addresses identify devices on the local segment — 48-bit, burned into the NIC
- Ethernet frames include destination MAC, source MAC, EtherType, payload, and FCS
- Switches learn MAC addresses dynamically and forward frames to the correct port
- ARP resolves IP addresses to MAC addresses
- VLANs segment broadcast domains at Layer 2 using 802.1Q tagging
- STP prevents loops in redundant Layer 2 topologies
- Error detection uses CRC/FCS — Layer 2 detects but does not correct errors

---

*Part of the CCNA 200-301 study repo — github.com/Fayezismail24/IT*
```
