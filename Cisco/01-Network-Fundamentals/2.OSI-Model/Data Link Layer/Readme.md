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


## CSMA/CD (Carrier Sense Multiple Access with Collision Detection)

CSMA/CD is a media access control method used by traditional Ethernet networks to manage access to a shared transmission medium.

It allows multiple devices to share the same network while minimizing the impact of collisions.

### How CSMA/CD Works

1. **Carrier Sense**: Listen to the medium before transmitting.
2. **Multiple Access**: Multiple devices can share the same network segment.
3. **Collision Detection**: Detect if another device transmits at the same time.
4. **Jam Signal**: Notify all devices that a collision occurred.
5. **Backoff**: Wait a random period before retransmitting.

### CSMA/CD Process

```text
Listen → Transmit → Collision?
                  ├─ No → Continue
                  └─ Yes → Send Jam Signal → Wait → Retransmit
```

### Collision Domains

#### Hub-Based Network

```text
PC ─┐
PC ─┼─ Hub
PC ─┘
```

All devices share the same collision domain.

#### Switched Network

```text
PC ─ Switch ─ PC
```

Each switch port creates a separate collision domain.

### Binary Exponential Backoff

After a collision occurs, devices wait for a random amount of time before retransmitting. The waiting period increases with each additional collision, reducing the chance of repeated collisions.

### Where is CSMA/CD Used?

**Used In**

* Ethernet hubs
* Shared Ethernet segments
* Half-duplex Ethernet

**Not Used In**

* Ethernet switches operating in full-duplex mode
* Modern enterprise networks
* Wi-Fi networks

### CSMA/CD vs CSMA/CA

| Feature            | CSMA/CD            | CSMA/CA           |
| ------------------ | ------------------ | ----------------- |
| Used In            | Ethernet           | Wi-Fi             |
| Collision Handling | Detects collisions | Avoids collisions |
| Network Type       | Wired              | Wireless          |
| Common Today       | Rare               | Common            |

### CCNA Exam Notes

* CSMA/CD operates at **Layer 2 (Data Link Layer)**.
* It is associated with **legacy Ethernet networks**.
* **Hubs create collisions**.
* **Switches eliminate collisions** by creating separate collision domains.
* **Full-duplex Ethernet does not use CSMA/CD**.




## CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)

CSMA/CA is a media access control method used by wireless networks (Wi-Fi) to reduce the likelihood of collisions before they occur.

Unlike Ethernet, wireless devices cannot reliably detect collisions while transmitting. Therefore, Wi-Fi attempts to avoid collisions rather than detect them.

### How CSMA/CA Works

1. **Carrier Sense**: Listen to the wireless medium.
2. **Medium Busy?** Wait until it becomes available.
3. **Random Backoff Timer**: Wait for a random period before transmitting.
4. **Transmit Data**.
5. **Receive ACK (Acknowledgment)** from the receiver.
6. **No ACK Received?** Assume a collision occurred and retransmit.

### CSMA/CA Process

```text
Listen → Medium Free?
          ├─ No → Wait
          └─ Yes → Random Backoff
                     ↓
                  Transmit
                     ↓
                 ACK Received?
                 ├─ Yes → Success
                 └─ No → Retransmit
```

### Why Wi-Fi Uses CSMA/CA

In wireless networks, devices cannot transmit and listen at the same time.

As a result, they cannot reliably detect collisions while sending data.

To overcome this limitation, Wi-Fi uses collision avoidance techniques.

### RTS/CTS (Optional Collision Avoidance)

Some Wi-Fi networks use:

* **RTS (Request To Send)**
* **CTS (Clear To Send)**

This mechanism helps reduce collisions, especially in environments with hidden nodes.

```text
Client → RTS → Access Point
Client ← CTS ← Access Point
Client → Data → Access Point
Client ← ACK ← Access Point
```

### Where is CSMA/CA Used?

**Used In**

* Wi-Fi (IEEE 802.11)
* Wireless LANs (WLANs)

**Not Used In**

* Traditional Ethernet
* Switched wired networks

### Advantages

* Reduces collision probability
* Works effectively in wireless environments
* Supports shared wireless mediums

### Disadvantages

* Additional overhead from waiting and acknowledgments
* Lower efficiency than switched Ethernet
* Performance decreases as wireless congestion increases

### CSMA/CD vs CSMA/CA

| Feature            | CSMA/CD                                                | CSMA/CA                                                |
| ------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| Full Name          | Carrier Sense Multiple Access with Collision Detection | Carrier Sense Multiple Access with Collision Avoidance |
| Network Type       | Wired Ethernet                                         | Wireless Wi-Fi                                         |
| Collision Handling | Detects collisions after they occur                    | Attempts to prevent collisions before they occur       |
| ACK Required       | No                                                     | Yes                                                    |
| RTS/CTS Support    | No                                                     | Yes                                                    |
| Common Today       | Rare                                                   | Very Common                                            |

### CCNA Exam Notes

* CSMA/CA operates at **Layer 2 (Data Link Layer)**.
* Used by **IEEE 802.11 (Wi-Fi)** networks.
* Uses **ACK frames** to confirm successful delivery.
* May use **RTS/CTS** to reduce collisions.
* Modern Wi-Fi relies on **CSMA/CA**, not CSMA/CD.

### Key Takeaway

* **CSMA/CD = Wired Ethernet (Collision Detection)**
* **CSMA/CA = Wireless Wi-Fi (Collision Avoidance)**

For the CCNA exam, remember:

> Ethernet uses **CSMA/CD** (historically), while Wi-Fi uses **CSMA/CA**.

Also update the **Common CCNA Topics** section:

```md
### CSMA/CD (Carrier Sense Multiple Access with Collision Detection)

Manages access to shared Ethernet media and handles collisions in half-duplex Ethernet networks.

### CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)

Used by Wi-Fi networks to reduce the likelihood of collisions through carrier sensing, random backoff timers, acknowledgments, and optional RTS/CTS mechanisms.
```


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

**Suggested repo names:**

* `osi-layer2-guide`
* `ccna-data-link-layer`
* `layer2-networking`
* `ethernet-and-switching`
* `ccna-layer2-fundamentals`
