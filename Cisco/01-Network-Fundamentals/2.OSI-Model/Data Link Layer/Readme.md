# Data Link Layer (OSI Layer 2)

## Overview

The **Data Link Layer** is Layer 2 of the OSI model. It is responsible for node-to-node communication, framing, physical addressing, error detection, and controlling access to the transmission medium.

The Data Link Layer receives packets from the Network Layer and encapsulates them into frames for transmission over the Physical Layer.

---

## Functions of the Data Link Layer

### Framing

Encapsulates Network Layer packets into frames for transmission.

### Physical Addressing

Uses **MAC (Media Access Control) addresses** to identify devices on a local network.

### Error Detection

Detects transmission errors using mechanisms such as the **Frame Check Sequence (FCS)**.

### Media Access Control

Determines how devices share and access the network medium.

### Flow Control

Helps regulate data transmission between devices.

---

## Data Link Layer Sub-Layers

### LLC (Logical Link Control)

* Communicates with the Network Layer
* Identifies Network Layer protocols
* Defined by IEEE 802.2

### MAC (Media Access Control)

* Controls access to the physical medium
* Handles MAC addressing
* Defined by IEEE 802 standards

```text id="nccu1q"
+-----------------------+
| Logical Link Control  |
+-----------------------+
| Media Access Control  |
+-----------------------+
```

---

## Frame Structure

A Layer 2 frame typically contains:

```text id="wsq9gl"
+---------+---------+------+------+
| Dest MAC| Src MAC | Data | FCS  |
+---------+---------+------+------+
```

### Frame Fields

| Field           | Purpose                     |
| --------------- | --------------------------- |
| Destination MAC | Receiver's MAC address      |
| Source MAC      | Sender's MAC address        |
| Data            | Encapsulated Layer 3 packet |
| FCS             | Error detection field       |

---

## MAC Addresses

A MAC address is a unique 48-bit hardware address assigned to a network interface.

Example:

```text id="hyq77n"
00:1A:2B:3C:4D:5E
```

### MAC Address Structure

```text id="4c0b0o"
00:1A:2B | 3C:4D:5E
   OUI   | Device ID
```

* **OUI (Organizationally Unique Identifier)**: Manufacturer identifier
* **Device ID**: Unique identifier assigned by the manufacturer

---

## Switching

Switches operate primarily at Layer 2.

### Switch Functions

* Learn MAC addresses
* Build a MAC address table
* Forward frames
* Filter frames
* Flood unknown unicast traffic

---

## VLANs (Virtual LANs)

VLANs logically separate devices into different broadcast domains.

### Benefits

* Improved security
* Reduced broadcasts
* Better network management
* Increased scalability

Example:

```text id="mrm9nk"
VLAN 10 → HR Department
VLAN 20 → IT Department
VLAN 30 → Finance Department
```

---

## Layer 2 Protocols

* Ethernet (IEEE 802.3)
* Wi-Fi (IEEE 802.11)
* PPP (Point-to-Point Protocol)
* HDLC (High-Level Data Link Control)

---

## Common CCNA Topics

### ARP (Address Resolution Protocol)

Maps IPv4 addresses to MAC addresses.

### STP (Spanning Tree Protocol)

Prevents Layer 2 loops in switched networks.

### EtherChannel

Combines multiple physical links into a single logical connection.

### VLAN Trunking

Allows multiple VLANs to traverse a single link using IEEE 802.1Q tagging.

---

## Troubleshooting Commands

### Cisco IOS

```bash
show mac address-table
show interfaces
show interfaces status
show vlan brief
show spanning-tree
show etherchannel summary
```

---

## Common Layer 2 Issues

* Duplex mismatch
* VLAN misconfiguration
* MAC address table problems
* Layer 2 loops
* STP blocking ports
* Faulty cables or transceivers

---

## Key Takeaway

The Data Link Layer provides reliable local network communication by using frames, MAC addresses, switching, VLANs, and error detection mechanisms. It serves as the bridge between the Physical Layer and the Network Layer in the OSI model.

## References

* Cisco CCNA 200-301 Official Cert Guide
* IEEE 802 Standards
* Cisco Networking Academy
* RFC 826 (ARP)
