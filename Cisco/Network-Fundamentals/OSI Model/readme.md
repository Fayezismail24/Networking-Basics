## 📌 What is the OSI Model?

The OSI (Open Systems Interconnection) model is a **conceptual framework** used to understand and troubleshoot how networks communicate. It has **7 layers**, each with a specific role. While TCP/IP is what networks actually use, OSI is the **universal language of network troubleshooting**.

```
┌─────────────────────────────────┐
│       APPLICATION LAYER         │  ← Layer 7  (HTTP, FTP, DNS, DHCP)
├─────────────────────────────────┤
│       PRESENTATION LAYER        │  ← Layer 6  (Encryption, Compression)
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
