## 📌 What is the OSI Model?

The OSI (Open Systems Interconnection) model is a **conceptual framework** used to understand and troubleshoot how networks communicate. It has **7 layers**, each with a specific role. While TCP/IP is what networks actually use, OSI is the **universal language of network troubleshooting**.

```
┌─────────────────────────────────┐
│       APPLICATION LAYER         │  ← Layer 7  (HTTP, FTP, DNS, DHCP)
├─────────────────────────────────┤
│       PRESENTATION LAYER        │  ← Layer 6  (Encryption(TLS/SSL), Compression)
├─────────────────────────────────┤
│       SESSION LAYER             │  ← Layer 5  (Sessions, NetBIOS)
├─────────────────────────────────┤
│       TRANSPORT LAYER           │  ← Layer 4  (TCP & UDP, Port Numbers)
├─────────────────────────────────┤
│       NETWORK LAYER             │  ← Layer 3  (IP, Routing, Router)
├─────────────────────────────────┤
│       DATA LINK LAYER           │  ← Layer 2  (MAC, Frames, Switch)
├─────────────────────────────────┤
│       PHYSICAL LAYER            │  ← Layer 1  (Cables, Bits, NIC)
└─────────────────────────────────┘
```

> 💡 **Memory Trick (top → bottom):** **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing  
> 💡 **Memory Trick (bottom → top):** **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way

---

## 🔁 OSI vs TCP/IP Mapping

```
OSI Model (7 Layers)          TCP/IP Model (5 Layers)
─────────────────────         ────────────────────────
7. Application   ──┐
6. Presentation  ──┼────────► 5. Application
5. Session       ──┘
4. Transport     ──────────► 4. Transport
3. Network       ──────────► 3. Internet
2. Data Link     ──────────► 2. Data Link
1. Physical      ──────────► 1. Physical
```

> 💡 **Exam Tip:** OSI is used for **troubleshooting and theory**. TCP/IP is used in **real implementation**.

---

## 🧱 Each Layer Explained

### Layer 1 — Physical Layer
Handles the **raw transmission of bits** over a physical medium. No addressing, no logic — just signals.

| Component | Role |
|---|---|
| Cables (Copper/Fiber) | Physical medium for signal transmission |
| Wi-Fi Radio (802.11) | Wireless signal transmission |
| Hubs / Repeaters | Amplify/repeat signals (Layer 1 only) |
| NIC (Physical part) | Converts bits to electrical/optical signals |
| Clocking & Encoding | Defines how bits are represented on the wire |

**PDU:** Bits (1s and 0s)  
**Address Used:** None  
**Devices:** Hub, Repeater, Cable, NIC (hardware)

---

### Layer 2 — Data Link Layer
Handles **node-to-node delivery** on the same local network. Responsible for framing, MAC addressing, and error detection.

| Component | Role |
|---|---|
| Ethernet (802.3) | Wired LAN framing standard |
| Wi-Fi (802.11) | Wireless LAN framing standard |
| MAC Address | Hardware address for local frame delivery |
| Switch / Bridge | Forwards frames based on MAC address table |
| NIC (Logical part) | Builds and reads Ethernet frames |
| ARP | Resolves IP address → MAC address |

**PDU:** Frame  
**Address Used:** MAC Address  
**Devices:** Switch, Bridge, NIC (logical)

> 💡 **Key Point:** Layer 2 is split into two sublayers:
> - **LLC (Logical Link Control)** — interfaces with Layer 3 above
> - **MAC (Media Access Control)** — controls access to the physical medium

---

### Layer 3 — Network Layer
Handles **logical addressing** and **routing** between different networks. This is where packets travel across the internet.

| Component | Role |
|---|---|
| IP (v4/v6) | Logical addressing and routing |
| ICMP | Error reporting (used by `ping` and `traceroute`) |
| ARP | Resolves IP → MAC address |
| Router | Routes packets between networks |
| RIP, OSPF, EIGRP, BGP | Routing protocols |

**PDU:** Packet  
**Address Used:** IP Address  
**Devices:** Router, Layer 3 Switch

---

### Layer 4 — Transport Layer ⭐
Handles **end-to-end communication** between hosts. Responsible for segmentation, flow control, and reliability.

| Component | Role |
|---|---|
| TCP | Reliable, connection-oriented delivery |
| UDP | Fast, connectionless, best-effort delivery |
| Port Numbers | Identify specific services/applications |
| Segmentation | Breaks data into segments for transmission |
| Flow Control | Windowing prevents receiver overflow |
| Error Recovery | TCP retransmits lost segments |

**PDU:** Segment (TCP) / Datagram (UDP)  
**Address Used:** Port Numbers  
**Devices:** Firewall (stateful), Load Balancer

---

### Layer 5 — Session Layer
Manages **sessions (connections) between applications**. Responsible for establishing, maintaining, and terminating communication sessions.

| Component | Role |
|---|---|
| NetBIOS | Session establishment for Windows networking |
| RPC (Remote Procedure Call) | Allows programs to request services over a network |
| PPTP | Tunneling protocol for VPNs |
| Session establishment | Opens and closes communication sessions |
| Synchronization | Adds checkpoints to long data transfers |

**PDU:** Data  
**Address Used:** None  
**Real-world example:** When you log into a web app, Layer 5 manages that ongoing session.

> 💡 **Exam Tip:** Layer 5 is rarely tested in depth on CCNA. Focus on Layers 1–4 and 7.

---

### Layer 6 — Presentation Layer
Responsible for **data translation, encryption, and compression**. Acts as the "translator" between the application and the network.

| Function | Description |
|---|---|
| Encryption / Decryption | SSL/TLS encrypts data for HTTPS |
| Compression | Reduces data size before transmission |
| Data Translation | Converts formats (e.g., JPEG, MP4, ASCII) |
| Encoding | Ensures data is in a readable format for Layer 7 |

**PDU:** Data  
**Address Used:** None  
**Examples:** SSL/TLS, JPEG, MP3, ASCII, Unicode

> 💡 **Exam Tip:** If a question mentions **encryption or data format conversion**, think Layer 6.

---

### Layer 7 — Application Layer
The layer **closest to the user**. Provides network services directly to applications. This is what you actually interact with.

| Protocol | Port | Uses |
|---|---|---|
| HTTP | 80 | Web browsing |
| HTTPS | 443 | Secure web |
| DNS | 53 | Domain resolution |
| DHCP | 67/68 | IP assignment |
| FTP | 20/21 | File transfer |
| SSH | 22 | Secure remote access |
| Telnet | 23 | Remote access (unsecure) |
| SMTP | 25 | Email sending |
| POP3 | 110 | Email receiving |
| IMAP | 143 | Email access |
| SNMP | 161 | Network management |

**PDU:** Data  
**Address Used:** None (uses Layer 4 ports)

> 💡 **Key Point:** Layer 7 is NOT the user itself — it's the **interface between the user's application and the network**.

---

## 📦 Data Encapsulation Flow (Sender)

```
Layer 7 — Application   → Data
          ↓
Layer 6 — Presentation  → Data (encrypted/formatted)
          ↓
Layer 5 — Session       → Data (session info added)
          ↓
Layer 4 — Transport     → Segment  (TCP/UDP Header + Data)
          ↓
Layer 3 — Network       → Packet   (IP Header + Segment)
          ↓
Layer 2 — Data Link     → Frame    (Ethernet Header + Packet + FCS)
          ↓
Layer 1 — Physical      → Bits     (1s and 0s on the wire)
```

**De-encapsulation** happens in reverse on the receiving end — each layer strips its header and passes data up.

---

## 🔄 PDU Names Per Layer

| Layer | Name | PDU |
|---|---|---|
| 7 — Application | Data | Data |
| 6 — Presentation | Data | Data |
| 5 — Session | Data | Data |
| 4 — Transport | Segment / Datagram | TCP Segment / UDP Datagram |
| 3 — Network | Packet | IP Packet |
| 2 — Data Link | Frame | Ethernet Frame |
| 1 — Physical | Bits | 1s and 0s |

> 💡 **Exam Tip:** Knowing PDU names per layer is a **guaranteed exam topic**.

---

## 🖥️ Devices by Layer

| Layer | Device |
|---|---|
| Layer 7 | Proxy Server, Application Firewall |
| Layer 4 | Stateful Firewall, Load Balancer |
| Layer 3 | Router, Layer 3 Switch |
| Layer 2 | Switch, Bridge |
| Layer 1 | Hub, Repeater, Cable, NIC |

> 💡 **Key Rule:** A device that operates at Layer X also understands all layers **below** Layer X.  
> Example: A Router (Layer 3) also understands Layers 1 and 2.

---

## 🔧 Troubleshooting with OSI — Bottom-Up Approach

When something isn't working, start from Layer 1 and work your way up:

```
Layer 1 — Is the cable plugged in? Are link lights on?
Layer 2 — Is the MAC address in the switch table? Is the VLAN correct?
Layer 3 — Do devices have correct IPs? Is there a valid route?
Layer 4 — Is the correct port open? Is a firewall blocking it?
Layer 5 — Is the session being established properly?
Layer 6 — Is there a certificate or encoding issue?
Layer 7 — Is the application configured correctly?
```

---


## ❓ CCNA Exam Practice Questions

**Q1:** At which OSI layer does a Router primarily operate?  
**A:** Layer 3 — Network Layer

**Q2:** What PDU is used at the Data Link layer?  
**A:** Frame

**Q3:** Which layer is responsible for encryption and data formatting?  
**A:** Layer 6 — Presentation Layer

**Q4:** A switch operates at which layer?  
**A:** Layer 2 — Data Link Layer

**Q5:** Which layer uses port numbers to identify applications?  
**A:** Layer 4 — Transport Layer

**Q6:** What is the PDU at Layer 3?  
**A:** Packet

**Q7:** A technician can ping a server by IP but cannot reach it by hostname. Which layer is the issue most likely at?  
**A:** Layer 7 (Application) — DNS resolution failure

**Q8:** Which OSI layers does TCP/IP's Application layer combine?  
**A:** Layers 5, 6, and 7 (Session, Presentation, Application)

**Q9:** What is the correct bottom-up order of OSI layers?  
**A:** Physical → Data Link → Network → Transport → Session → Presentation → Application

---

## ⚔️ OSI vs TCP/IP — Side by Side

| Feature | OSI Model | TCP/IP Model |
|---|---|---|
| Layers | 7 | 5 |
| Purpose | Theory / Troubleshooting | Real-world implementation |
| Developed by | ISO | DARPA |
| Layer 5–7 equivalent | Session, Presentation, Application | Application |
| Still used? | As a reference model | Yes — the actual internet |

---

## 🔑 Key Takeaways

- OSI has **7 layers** — each with a distinct role in network communication
- **Layer 1** = Physical (bits, cables, hubs)
- **Layer 2** = Data Link (frames, MAC, switches)
- **Layer 3** = Network (packets, IP, routers)
- **Layer 4** = Transport (segments, TCP/UDP, ports)
- **Layer 5** = Session (session management)
- **Layer 6** = Presentation (encryption, formatting)
- **Layer 7** = Application (user-facing protocols)
- **Encapsulation** adds headers layer by layer going down; **de-encapsulation** strips them going up
- Troubleshoot **bottom-up**: start at Layer 1 and work toward Layer 7
- OSI is a **reference model** — TCP/IP is what actually runs the internet


# 📦 Packet Headers & Encapsulation — Complete Structure

## 🎯 Overview: The Complete Packet

When data travels through the OSI model, each layer **wraps the data** with its own header. This is called **encapsulation**. Here's what the final packet looks like:

```
┌─────────────────────────────────────────────────────────────────────┐
│                    COMPLETE FRAME ON THE WIRE                       │
├─────────────────────────────────────────────────────────────────────┤
│ Layer 2 Header  │ Layer 3 Header │ Layer 4 Header │  Application   │
│  (14 bytes)     │  (20+ bytes)   │  (20+ bytes)   │    Data        │
├─────────────────────────────────────────────────────────────────────┤
│ Ethernet Frame                                                       │
│ Dest MAC │ Src MAC │ Type │ IP Packet                   │ FCS      │
├─────────────────────────────────────────────────────────────────────┤
                           │
                           ├─ IP Header
                           │  Dest IP │ Src IP │ TCP Segment
                           │
                           ├─────────────────────────────────────┤
                           │ Dest Port │ Src Port │ App Data     │
                           └─────────────────────────────────────┘
```

---

## 🔴 Layer 1 — Physical Layer
**No Headers** — Just raw **bits (1s and 0s)** on the wire.

```
Bits: 10101100 11010011 01001101 ...
```

---

## 🟠 Layer 2 — Data Link Layer (Ethernet Frame)

**Frame Header:** 14 bytes (before payload) + 4 bytes (FCS at end)

```
┌──────────────┬──────────────┬──────┬──────────────────────────────┬─────┐
│ Dest MAC Add │ Src MAC Add  │ Type │        Payload (IP Packet)   │ FCS │
│  (6 bytes)   │  (6 bytes)   │ (2)  │        up to 1500 bytes      │ (4) │
└──────────────┴──────────────┴──────┴──────────────────────────────┴─────┘
```

### Ethernet Frame Header Fields:

| Field | Size | Purpose | Example |
|-------|------|---------|---------|
| **Preamble** | 7 bytes | Synchronization (added by NIC) | 10101010 × 7 |
| **Start Frame Delimiter (SFD)** | 1 byte | Frame boundary marker | 10101011 |
| **Destination MAC** | 6 bytes | Hardware address of next hop | `AA:BB:CC:DD:EE:FF` |
| **Source MAC** | 6 bytes | Hardware address of sender | `11:22:33:44:55:66` |
| **EtherType** | 2 bytes | Identifies Layer 3 protocol | `0x0800` = IPv4, `0x86DD` = IPv6 |
| **Payload** | 46–1500 bytes | IP Packet (Layer 3 + above) | [IP Packet] |
| **Frame Check Sequence (FCS)** | 4 bytes | Error detection (CRC) | Calculated checksum |

### Real Example — Ethernet Frame:

```
Destination MAC:  00:1A:2B:3C:4D:5E
Source MAC:       AA:BB:CC:DD:EE:FF
EtherType:        0x0800 (IPv4)
Payload:          [IP Packet - 60 bytes]
FCS:              0x12345678
```

**Frame Checksum (FCS):** Uses CRC-32 to detect transmission errors.

---

## 🟡 Layer 3 — Network Layer (IP Header)

**IP Header:** 20 bytes minimum (160 bits) — can be up to 60 bytes with options

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
┌───┬───┬───┬───┬───────────────────────┬─────────────────────────┐
│Ver│IHL│DSCP      │ECN│      Total Length (including header)      │
├───┴───┴───┴───┴───┴───────────────────┴─────────────────────────┤
│              Identification                │Flags│  Fragment Offset  │
├─────────────────────────────────────────────┴──────┴─────────────────┤
│  Time to Live (TTL)  │  Protocol  │        Header Checksum         │
├──────────────────────┴────────────┴─────────────────────────────────┤
│                       Source IP Address (4 bytes)                    │
├────────────────────────────────────────────────────────────────────┤
│                     Destination IP Address (4 bytes)                │
├────────────────────────────────────────────────────────────────────┤
│              Options (if IHL > 5) + Padding                         │
└────────────────────────────────────────────────────────────────────┘
```

### IPv4 Header Fields Explained:

| Field | Size | Purpose | Example |
|-------|------|---------|---------|
| **Version** | 4 bits | IP version (4 for IPv4, 6 for IPv6) | `4` |
| **IHL (Internet Header Length)** | 4 bits | Header length in 32-bit words (min=5, max=15) | `5` = 20 bytes |
| **DSCP (Differentiated Services Code Point)** | 6 bits | Quality of Service (QoS) marking | `0–63` |
| **ECN (Explicit Congestion Notification)** | 2 bits | Congestion feedback | `0–3` |
| **Total Length** | 16 bits | Entire packet size (header + payload) | `1500` bytes |
| **Identification** | 16 bits | Unique ID for packet fragments | `0x1234` |
| **Flags** | 3 bits | Control routing behavior | Bit 0: Reserved, Bit 1: DF (Don't Fragment), Bit 2: MF (More Fragments) |
| **Fragment Offset** | 13 bits | Position in fragmented packet (in 8-byte blocks) | `0` (no fragmentation) |
| **Time to Live (TTL)** | 8 bits | Hops before packet is discarded | `64` or `255` (decrements at each router) |
| **Protocol** | 8 bits | Layer 4 protocol identifier | `6` = TCP, `17` = UDP, `1` = ICMP |
| **Header Checksum** | 16 bits | Error detection for header only | Calculated CRC |
| **Source IP** | 32 bits | Sender's IP address | `192.168.1.100` |
| **Destination IP** | 32 bits | Recipient's IP address | `10.0.0.50` |
| **Options** | 0–40 bytes | Optional (record route, timestamps, etc.) | Padding to 32-bit boundary |

### Real IPv4 Header Example:

```
Version:        4 (IPv4)
IHL:            5 (20 bytes header)
DSCP:           0
ECN:            0
Total Length:   1480 bytes (header 20 + payload 1460)
Identification: 0x4321
Flags:          DF (Don't Fragment) = 1
Fragment Offset: 0
TTL:            64
Protocol:       6 (TCP)
Header Checksum: 0xABCD
Source IP:      192.168.1.100
Dest IP:        8.8.8.8
```

**Minimum Header:** 20 bytes  
**Maximum Header:** 60 bytes (with options)

---

## 🟢 Layer 4 — Transport Layer

### TCP Header (20 bytes minimum)

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
┌──────────────────────────────────────────────────────────────────┐
│            Source Port                  │    Destination Port     │
├──────────────────────────────────────────────────────────────────┤
│                       Sequence Number                             │
├──────────────────────────────────────────────────────────────────┤
│                     Acknowledgment Number                         │
├─────────┬───────┬─────────────────┬──────────────────────────────┤
│ Offset  │Reserv│  Control Flags   │        Window Size           │
├─────────┼───────┼─────────────────┼──────────────────────────────┤
│           Checksum                │    Urgent Pointer (if URG)    │
├──────────────────────────────────────────────────────────────────┤
│              Options (if Offset > 5) + Padding                   │
└──────────────────────────────────────────────────────────────────┘
```

### TCP Header Fields:

| Field | Size | Purpose | Example |
|-------|------|---------|---------|
| **Source Port** | 16 bits | Sender's port number | `49152` (ephemeral) |
| **Destination Port** | 16 bits | Receiver's port number | `80` (HTTP) |
| **Sequence Number** | 32 bits | Byte offset in stream (for ordering) | `0x10000000` |
| **Acknowledgment Number** | 32 bits | Next expected byte (ACK) | `0x10000001` |
| **Data Offset** | 4 bits | TCP header length in 32-bit words | `5` = 20 bytes |
| **Reserved** | 3 bits | Must be zero | `0` |
| **Control Flags** | 9 bits | SYN, ACK, FIN, RST, PSH, URG, etc. | See below |
| **Window Size** | 16 bits | Receiver's buffer space (flow control) | `65535` bytes |
| **Checksum** | 16 bits | Error detection for header + payload | Calculated |
| **Urgent Pointer** | 16 bits | Points to urgent data (if URG flag set) | Byte offset |
| **Options** | 0–40 bytes | MSS, Window Scale, Timestamps, SACK | Padding to 32-bit boundary |

### TCP Control Flags (9 bits):

```
┌─┬─┬─┬─┬─┬─┬─┬─┬─┐
│R│R│R│N│C│E│U│A│F│
│E│E│E│S│W│C│R│C│I│
│S│S│S│ │R│E│G│K│N│
└─┴─┴─┴─┴─┴─┴─┴─┴─┘
  Reserved (must be 0)
         NS  = ECN-Nonce Concealment Protection
         CWR = Congestion Window Reduced
         ECE = ECN-Echo
         URG = Urgent flag
         ACK = Acknowledgment flag
         PSH = Push flag (send data immediately)
         RST = Reset flag
         SYN = Synchronize sequence numbers
         FIN = Final flag (end connection)
```

### Real TCP Header Example (HTTP Request):

```
Source Port:        54321 (client's ephemeral port)
Destination Port:   80 (HTTP server)
Sequence Number:    0x00001000
Acknowledgment:     0x00005000
Data Offset:        5 (20 bytes header)
Flags:              SYN (initiating connection)
Window Size:        65535 (receiver can accept 65535 bytes)
Checksum:           0x1234
Options:            MSS = 1460, Window Scale = 7
```

### TCP Connection Sequence (3-Way Handshake):

```
Client                          Server
  |                               |
  |──────── SYN (seq=X) ────────> |  Step 1: Client initiates
  |                               |
  | <──── SYN-ACK (seq=Y, ack=X+1) |  Step 2: Server responds
  |                               |
  |──────── ACK (seq=X+1, ack=Y+1) |  Step 3: Client acknowledges
  |                               |
  |    Connection Established    |
  |                               |
```

---

### UDP Header (8 bytes)

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
┌──────────────────────────────────────────────────────────────────┐
│            Source Port                  │    Destination Port     │
├──────────────────────────────────────────────────────────────────┤
│              Length (header + payload)  │        Checksum         │
├──────────────────────────────────────────────────────────────────┤
│                      Payload (Data)                               │
└──────────────────────────────────────────────────────────────────┘
```

### UDP Header Fields:

| Field | Size | Purpose | Example |
|-------|------|---------|---------|
| **Source Port** | 16 bits | Sender's port number | `53` (DNS) |
| **Destination Port** | 16 bits | Receiver's port number | `53` (DNS) |
| **Length** | 16 bits | Total UDP size (header 8 + payload) | `64` bytes |
| **Checksum** | 16 bits | Error detection (optional in IPv4) | Calculated or `0x0000` |

### Real UDP Header Example (DNS Query):

```
Source Port:        54321 (client ephemeral port)
Destination Port:   53 (DNS server)
Length:             32 bytes (8 header + 24 payload)
Checksum:           0x0000 (omitted in IPv4)
Payload:            DNS query for "google.com"
```

---

## 🔵 Layers 5–7 (Session, Presentation, Application)

**No additional headers** — Just the **application-level data**

### Examples:

**HTTP Request:**
```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html

[Application Data — No Layer 5/6 headers]
```

**DNS Query:**
```
Header:
  Transaction ID: 0x1234
  Questions: 1
  Answer RRs: 0
  Authority RRs: 0
  Additional RRs: 0

Questions:
  Name: www.google.com
  Type: A (IPv4 address)
  Class: IN (Internet)
```

---

## 📊 Complete Packet Example: HTTP GET Request

### Full Packet Breakdown:

```
┌─────────────────────────────────────────────────────────────────┐
│                      ETHERNET FRAME                             │
├─────────────────────────────────────────────────────────────────┤
│ Dest MAC: 00:1A:2B:3C:4D:5E (6 bytes)                           │
│ Src MAC:  AA:BB:CC:DD:EE:FF (6 bytes)                           │
│ Type:     0x0800 (IPv4) (2 bytes)                               │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                   IP HEADER (20 bytes)                   │   │
│  ├──────────────────────────────────────────────────────────┤   │
│  │ Version: 4, IHL: 5, DSCP: 0, ECN: 0                     │   │
│  │ Total Length: 486 bytes                                  │   │
│  │ Identification: 0x4321                                   │   │
│  │ Flags: DF, Fragment Offset: 0                            │   │
│  │ TTL: 64, Protocol: 6 (TCP), Header Checksum: 0xABCD     │   │
│  │ Source IP: 192.168.1.100                                 │   │
│  │ Destination IP: 93.184.216.34 (example.com)              │   │
│  │                                                           │   │
│  │  ┌────────────────────────────────────────────────────┐  │   │
│  │  │            TCP HEADER (20 bytes)                   │  │   │
│  │  ├────────────────────────────────────────────────────┤  │   │
│  │  │ Source Port: 54321 (ephemeral)                     │  │   │
│  │  │ Destination Port: 80 (HTTP)                        │  │   │
│  │  │ Sequence Number: 0x00100000                        │  │   │
│  │  │ Acknowledgment Number: 0x00050000                  │  │   │
│  │  │ Data Offset: 5 (20 bytes), Reserved: 0            │  │   │
│  │  │ Flags: ACK, PSH                                    │  │   │
│  │  │ Window Size: 65535 bytes                           │  │   │
│  │  │ Checksum: 0x5678, Urgent Pointer: 0               │  │   │
│  │  │                                                    │  │   │
│  │  │  ┌──────────────────────────────────────────────┐ │  │   │
│  │  │  │       HTTP APPLICATION DATA (446 bytes)      │ │  │   │
│  │  │  ├──────────────────────────────────────────────┤ │  │   │
│  │  │  │ GET /index.html HTTP/1.1                     │ │  │   │
│  │  │  │ Host: example.com                            │ │  │   │
│  │  │  │ User-Agent: Mozilla/5.0                      │ │  │   │
│  │  │  │ Accept: text/html,application/xhtml+xml      │ │  │   │
│  │  │  │ Accept-Language: en-US,en;q=0.9              │ │  │   │
│  │  │  │ Cookie: sessionid=abc123; theme=dark         │ │  │   │
│  │  │  │ Connection: keep-alive                       │ │  │   │
│  │  │  │ [blank line]                                 │ │  │   │
│  │  │  └──────────────────────────────────────────────┘ │  │   │
│  │  └────────────────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│ FCS (Frame Check Sequence): 0x12345678 (4 bytes)               │
└─────────────────────────────────────────────────────────────────┘

TOTAL PACKET SIZE: 14 (Ethernet) + 20 (IP) + 20 (TCP) + 446 (Data) + 4 (FCS) = 504 bytes
```

---

## 🔍 Encapsulation Summary Table

| Layer | PDU Name | Header Name | Size | Key Fields |
|-------|----------|-------------|------|------------|
| 2 | Frame | Ethernet Header | 14 + 4 | Dest MAC, Src MAC, Type |
| 3 | Packet | IP Header | 20–60 | Src IP, Dest IP, TTL, Protocol |
| 4 | Segment/Datagram | TCP/UDP Header | 20+ / 8 | Src Port, Dest Port, Flags (TCP) |
| 7 | Data | Application Data | Variable | HTTP, DNS, SMTP, FTP, etc. |

---

## ⏬ Encapsulation Process (Sender → Wire)

```
Step 1: Application Layer generates data
        → "GET /index.html HTTP/1.1..."

Step 2: Transport Layer (TCP) adds header
        → [TCP Hdr][GET /index.html HTTP/1.1...]

Step 3: Network Layer (IP) adds header
        → [IP Hdr][TCP Hdr][GET /index.html HTTP/1.1...]

Step 4: Data Link Layer (Ethernet) adds header + FCS
        → [Eth Hdr][IP Hdr][TCP Hdr][GET /index.html HTTP/1.1...][FCS]

Step 5: Physical Layer converts to bits and transmits
        → 10101100 11010011 01001101 ...
```

---

## ⬆️ De-Encapsulation Process (Receiving)

```
Step 1: Physical Layer receives bits
        → 10101100 11010011 01001101 ...

Step 2: Data Link Layer reads Ethernet header, strips FCS
        → [IP Hdr][TCP Hdr][GET /index.html HTTP/1.1...]

Step 3: Network Layer reads IP header, verifies checksum
        → [TCP Hdr][GET /index.html HTTP/1.1...]

Step 4: Transport Layer reads TCP header, checks ACK/SEQ
        → [GET /index.html HTTP/1.1...]

Step 5: Application Layer processes data
        → Browser displays the HTML
```

---

## 🎓 Key Points for CCNA

✅ **Ethernet Frame:** 14 bytes header + payload + 4 bytes FCS  
✅ **IPv4 Header:** Minimum 20 bytes, can be up to 60 bytes with options  
✅ **TCP Header:** Minimum 20 bytes, can be up to 60 bytes with options  
✅ **UDP Header:** Fixed 8 bytes — no options  
✅ **PDU Names:** Bits → Frame → Packet → Segment/Datagram → Data  
✅ **TTL in IP:** Decrements at each router; reaches 0 = packet discarded  
✅ **TCP Flags:** SYN, ACK, FIN, RST, PSH, URG  
✅ **Checksum:** IP header only; TCP/UDP covers header + payload  
✅ **Maximum Frame Size (MTU):** 1500 bytes payload (Ethernet standard)  

---

## 📝 Common Packet Sizes

| Component | Size |
|-----------|------|
| Ethernet Header + FCS | 18 bytes |
| IP Header (no options) | 20 bytes |
| TCP Header (no options) | 20 bytes |
| UDP Header | 8 bytes |
| **Minimum TCP/IP packet** | 20 + 20 = 40 bytes |
| **Ethernet MTU (Max payload)** | 1500 bytes |
| **Maximum Ethernet frame** | 1518 bytes (1500 payload + 18 headers) |

---

## 🔧 Wireshark Interpretation

When you capture a packet in Wireshark, you'll see:

```
Frame 1: 486 bytes on wire (3888 bits), 486 bytes captured (3888 bits)

Ethernet II, Src: aa:bb:cc:dd:ee:ff, Dst: 00:1a:2b:3c:4d:5e
    Destination MAC Address: 00:1a:2b:3c:4d:5e
    Source MAC Address: aa:bb:cc:dd:ee:ff
    Type: IPv4 (0x0800)

Internet Protocol Version 4, Src: 192.168.1.100, Dst: 93.184.216.34
    Version: 4
    Header Length: 20 bytes (5)
    Differentiated Services Field: 0x00
    Total Length: 486
    Identification: 0x4321
    Flags: Don't fragment
    Fragment Offset: 0
    Time to Live: 64
    Protocol: TCP (6)
    Header Checksum: 0xabcd
    Source IP: 192.168.1.100
    Destination IP: 93.184.216.34

Transmission Control Protocol, Src Port: 54321, Dst Port: 80, Seq: 0, Ack: 0
    Source Port: 54321
    Destination Port: 80 (http)
    Sequence Number: 0
    Acknowledgment Number: 0
    Header Length: 20 bytes (5)
    Flags: 0x018 (SYN, ACK)
    Window Size: 65535
    Checksum: 0x5678
    Urgent Pointer: 0

Hypertext Transfer Protocol
    GET /index.html HTTP/1.1\r\n
    Host: example.com\r\n
    User-Agent: Mozilla/5.0\r\n
    ...
```

---

## 💾 Packet Capture Example (tcpdump format)

```
$ tcpdump -i eth0 -v

12:34:56.789123 IP (tos 0x0, ttl 64, id 0x4321, length 486) 
    192.168.1.100.54321 > 93.184.216.34.http: 
    Flags [S], cksum 0x5678 (correct), seq 0, win 65535, 
    options [mss 1460,sackOK,TS val 123456 ecr 0,nop,wscale 7], 
    length 0
```

---

## 🧪 Hands-On Lab: Packet Analysis

**Scenario:** Analyze an HTTP GET request packet

**Tools:**
- Wireshark (packet capture)
- tcpdump (command-line capture)
- Python Scapy (packet crafting)

**Steps:**
1. Start Wireshark on your NIC
2. Open a browser → visit `http://example.com`
3. In Wireshark, find the SYN packet (Flags = S)
4. Expand each layer:
   - Expand Ethernet II → note Dest/Src MAC, Type
   - Expand IP → note Src/Dst IP, TTL, Protocol
   - Expand TCP → note Src/Dst Port, Seq/Ack, Flags
   - Expand HTTP → note GET request
5. Calculate total frame size = Layer 2 + Layer 3 + Layer 4 + Data + FCS

---

## 🚨 Common Packet Issues & Troubleshooting

| Issue | Root Cause | Layer | Fix |
|-------|-----------|-------|-----|
| "Host unreachable" | MAC resolution failed | Layer 2 | Check ARP, VLAN |
| Slow packet delivery | MTU too small (fragmentation) | Layer 2/3 | Increase MTU or reduce payload |
| Packet loss | TTL reached 0 | Layer 3 | Check routing loops |
| Connection refused | Port not listening | Layer 4 | Check firewall, service status |
| Checksum error | Corrupted header | Layer 2/3/4 | Re-transmit, check cables |
| TCP retransmit storm | Packet loss on network | Layer 4 | Check congestion, QoS |

---

