
# TCP/IP Model — Complete Study Notes


## 📌 What is the TCP/IP Model?

The TCP/IP model is the **real-world framework** used by the internet and modern networks. It has **5 layers** (compared to OSI's 7). Every packet you send — whether it's a YouTube video, a Discord message, or a ping — follows this model.

```
┌─────────────────────────────────┐
│       APPLICATION LAYER         │  ← Layer 5
├─────────────────────────────────┤
│       TRANSPORT LAYER           │  ← Layer 4  (TCP & UDP live here)
├─────────────────────────────────┤
│       INTERNET LAYER            │  ← Layer 3  (IP lives here)
├─────────────────────────────────┤
│       DATA LINK LAYER           │  ← Layer 2  (MAC, Frames, Switch)
├─────────────────────────────────┤
│       PHYSICAL LAYER            │  ← Layer 1  (Cables, Bits, NIC)
└─────────────────────────────────┘
```

---

## 🔁 TCP/IP vs OSI Mapping

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
Handles the **raw transmission of bits** over a physical medium. No addressing, just electricity, light, or radio waves.

| Component | Role |
|---|---|
| Cables (Copper/Fiber) | Physical medium for signal transmission |
| Wi-Fi Radio (802.11) | Wireless signal transmission |
| Hubs / Repeaters | Amplify/repeat signals (Layer 1 only) |
| NIC (Physical part) | Converts bits to electrical/optical signals |
| Clocking & Encoding | Defines how bits are represented on wire |

**PDU:** Bits (1s and 0s)  
**Address Used:** None

---

### Layer 2 — Data Link Layer
Handles **node-to-node delivery** on the same network. Responsible for framing, MAC addressing, and error detection on the local link.

| Component | Role |
|---|---|
| Ethernet (802.3) | Wired LAN framing standard |
| Wi-Fi (802.11) | Wireless LAN framing standard |
| MAC Address | Hardware address for local frame delivery |
| Switch / Bridge  | Forwards frames based on MAC address table |
| NIC (Logical part) | Builds and reads Ethernet frames |
| ARP | Resolves IP address → MAC address |

**PDU:** Frame  
**Address Used:** MAC Address

> 💡 **Key Point:** The Data Link layer is split into two sublayers:
> - **LLC (Logical Link Control)** — interfaces with the Network layer above
> - **MAC (Media Access Control)** — controls access to the physical medium

---

### Layer 3 — Internet Layer (Network)
Handles **logical addressing** and **routing** between networks.

| Component | Role |
|---|---|
| IP (v4/v6) | Logical addressing |
| ICMP | Error reporting (used by `ping`) |
| ARP | Resolves IP → MAC address |
| Router | Routes packets between networks |

**PDU:** Packet  
**Address Used:** IP Address

---

### Layer 4 — Transport Layer ⭐
Handles **end-to-end communication**. This is where **TCP and UDP** operate.

**PDU:** Segment (TCP) / Datagram (UDP)  
**Address Used:** Port Numbers

---

### Layer 5 — Application Layer
Where user-facing protocols live.

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
| SNMP | 161 | Network management |

---

## ⚡ TCP vs UDP — Deep Dive

### TCP — Transmission Control Protocol

> **Reliable, connection-oriented, ordered delivery**

#### TCP 3-Way Handshake (Connection Setup)
```
Client                          Server
  │                               │
  │──────── SYN ─────────────────►│   "I want to connect"
  │                               │
  │◄─────── SYN-ACK ─────────────│   "OK, I'm ready"
  │                               │
  │──────── ACK ─────────────────►│   "Great, let's go"
  │                               │
  │    [ Data Transfer ]          │
  │                               │
```

#### TCP 4-Way Termination (Connection Teardown)
```
Client                          Server
  │──────── FIN ─────────────────►│
  │◄─────── ACK ──────────────────│
  │◄─────── FIN ──────────────────│
  │──────── ACK ─────────────────►│
```

#### TCP Key Features

| Feature | Description |
|---|---|
| Connection-oriented | Must establish connection before data |
| Reliable | Guarantees delivery with ACKs |
| Ordered | Data arrives in correct sequence |
| Flow Control | Sliding window prevents overflow |
| Error Detection | Checksums + retransmission |
| Slower | More overhead than UDP |

#### TCP Header Fields (Key Ones)
```
┌──────────────┬──────────────┐
│  Source Port │  Dest Port   │
├──────────────┴──────────────┤
│       Sequence Number        │
├─────────────────────────────┤
│    Acknowledgment Number     │
├────────┬────────────────────┤
│ Flags  │   Window Size      │
├────────┴────────────────────┤
│  Checksum  │  Urgent Ptr    │
└─────────────────────────────┘
```

**TCP Flags:**
- `SYN` — Synchronize (start connection)
- `ACK` — Acknowledge (confirm receipt)
- `FIN` — Finish (end connection)
- `RST` — Reset (abort connection)
- `PSH` — Push (send data immediately)

#### When to Use TCP
- Web browsing (HTTP/HTTPS)
- Email (SMTP, IMAP)
- File transfer (FTP)
- SSH, Telnet
- Any app where **data accuracy matters**

---

### UDP — User Datagram Protocol

> **Fast, connectionless, best-effort delivery**

#### UDP Communication (No Handshake)
```
Client                          Server
  │                               │
  │──────── Data ────────────────►│   (no setup, just send)
  │──────── Data ────────────────►│
  │──────── Data ────────────────►│
  │                               │
  (no acknowledgment, no order guaranteed)
```

#### UDP Key Features

| Feature | Description |
|---|---|
| Connectionless | No handshake needed |
| Unreliable | No guarantee of delivery |
| Unordered | Packets may arrive out of order |
| No Flow Control | No windowing |
| Fast | Low overhead |
| Lightweight header | Only 8 bytes (vs TCP's 20+) |

#### UDP Header Fields
```
┌──────────────┬──────────────┐
│  Source Port │  Dest Port   │
├──────────────┴──────────────┤
│   Length     │  Checksum    │
├──────────────────────────────┤
│           Data               │
└──────────────────────────────┘
```

#### When to Use UDP
- Video streaming (YouTube, Netflix)
- Voice/Video calls (VoIP, Zoom)
- Online gaming
- DNS queries
- DHCP
- SNMP
- TFTP
- Any app where **speed matters more than perfection**

---

## ⚔️ TCP vs UDP — Side by Side

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Reliable ✅ | Unreliable ❌ |
| Speed | Slower 🐢 | Faster 🐇 |
| Order | Ordered ✅ | Not guaranteed ❌ |
| Header Size | 20–60 bytes | 8 bytes |
| Flow Control | Yes (Windowing) | No |
| Error Recovery | Yes (Retransmission) | No |
| Use Case | HTTP, SSH, FTP, Email | DNS, VoIP, Video, Gaming |
| Handshake | 3-Way Handshake | None |

---

## 🔢 Port Numbers — Must Know for CCNA

### Well-Known Ports (0–1023)

| Port | Protocol | Transport |
|---|---|---|
| 20 | FTP Data | TCP |
| 21 | FTP Control | TCP |
| 22 | SSH | TCP |
| 23 | Telnet | TCP |
| 25 | SMTP | TCP |
| 53 | DNS | **TCP & UDP** |
| 67/68 | DHCP | UDP |
| 69 | TFTP | UDP |
| 80 | HTTP | TCP |
| 110 | POP3 | TCP |
| 143 | IMAP | TCP |
| 161/162 | SNMP | UDP |
| 443 | HTTPS | TCP |
| 514 | Syslog | UDP |

> 💡 **DNS uses both** TCP and UDP: UDP for queries, TCP for zone transfers.

---

## 📦 Data Encapsulation Flow

```
Application Layer → Data
        ↓
Transport Layer   → Segment  (TCP/UDP Header + Data)
        ↓
Internet Layer    → Packet   (IP Header + Segment)
        ↓
Data Link Layer   → Frame    (Ethernet Header + Packet + FCS)
        ↓
Physical Layer    → Bits     (1s and 0s on the wire)
```

**De-encapsulation** happens in reverse on the receiving end.

---

## 🧪 Lab Commands (GNS3/Packet Tracer)

```bash
# Test connectivity (uses ICMP — Internet Layer)
ping 192.168.1.1

# Trace the path packets take
traceroute 192.168.1.1

# See active TCP/UDP connections (on a PC)
netstat -an

# Capture and analyze TCP handshake
# → Use Wireshark on GNS3 links
```

---

## ❓ CCNA Exam Practice Questions

**Q1:** Which layer of the TCP/IP model is responsible for logical addressing?  
**A:** Internet Layer (maps to OSI Network Layer)

**Q2:** What protocol uses a 3-way handshake?  
**A:** TCP

**Q3:** A VoIP application needs fast delivery but can tolerate some packet loss. Which transport protocol should it use?  
**A:** UDP

**Q4:** What port does HTTPS use?  
**A:** 443 (TCP)

**Q5:** What does the ACK flag in TCP mean?  
**A:** Acknowledgment — confirms receipt of data

**Q6:** Which is faster — TCP or UDP, and why?  
**A:** UDP, because it has no handshake, no acknowledgments, and an 8-byte header vs TCP's 20+ bytes.

**Q7:** DNS primarily uses which transport protocol and why?  
**A:** UDP (port 53) for queries due to speed; TCP (port 53) for zone transfers requiring reliability.

---

## 🔑 Key Takeaways

- TCP/IP has **5 layers** — Application, Transport, Internet, Data Link, Physical
- **Data Link** handles MAC addressing and framing (Switch layer)
- **Physical** handles raw bit transmission (cables, signals, NIC hardware)
- **TCP** = reliable, ordered, connection-oriented (HTTP, SSH, FTP)
- **UDP** = fast, connectionless, best-effort (DNS, VoIP, streaming)
- The **3-way handshake** is SYN → SYN-ACK → ACK
- **Encapsulation** adds headers at each layer going down; **de-encapsulation** strips them going up
- Know your **port numbers** — they appear directly on the exam

---

*📅 Notes by: [Your Name] | CCNA 200-301 Study Journey*  
*📂 Repo: ccna-200-301/01-Network-Fundamentals/TCPIP-Model.md*
