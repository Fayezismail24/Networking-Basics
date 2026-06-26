
# Transport Layer (OSI Layer 4)

## What is the Transport Layer?

The Transport Layer is the fourth layer of the OSI model.
It sits between the Network Layer (Layer 3) and the Session Layer (Layer 5).

Its job is to provide end-to-end communication between applications
running on different hosts. While Layer 3 delivers packets between
devices, Layer 4 delivers data between specific applications on those devices.

Layer 4 works with port numbers — not IP addresses or MAC addresses.

---

## Responsibilities

- Segmentation — breaking large data into smaller segments
- Reassembly — putting segments back in order at the destination
- Port numbering — identifying which application the data belongs to
- Connection establishment and termination (TCP)
- Reliability and error recovery (TCP)
- Flow control — preventing sender from overwhelming receiver (TCP)
- Multiplexing — allowing multiple applications to use the network simultaneously

---

## Two Main Protocols

| Feature | TCP | UDP |
|---------|-----|-----|
| Full name | Transmission Control Protocol | User Datagram Protocol |
| Connection | Connection-oriented | Connectionless |
| Reliability | Guaranteed delivery | No guarantee |
| Ordering | Segments reordered if needed | No reordering |
| Error recovery | Retransmits lost segments | No retransmission |
| Flow control | Yes — sliding window | No |
| Congestion control | Yes | No |
| Speed | Slower — more overhead | Faster — less overhead |
| Header size | 20 bytes minimum | 8 bytes |
| Use case | Web, email, file transfer | VoIP, video streaming, DNS, gaming |

---

## TCP — Transmission Control Protocol

TCP provides reliable, ordered, and error-checked delivery of data
between applications.

### TCP Header

```
┌──────────────────┬──────────────────┐
│   Source Port    │  Destination Port │  (16 bits each)
├──────────────────┴──────────────────┤
│           Sequence Number            │  (32 bits)
├─────────────────────────────────────┤
│         Acknowledgment Number        │  (32 bits)
├────────┬───────────────┬────────────┤
│  Data  │   Reserved    │   Flags    │
│ Offset │               │ (9 bits)   │
├────────┴───────────────┴────────────┤
│    Window Size   │     Checksum     │
├──────────────────┴──────────────────┤
│   Urgent Pointer │     Options      │
└──────────────────┴──────────────────┘
```

| Field | Size | Description |
|-------|------|-------------|
| Source Port | 16 bits | Sending application port |
| Destination Port | 16 bits | Receiving application port |
| Sequence Number | 32 bits | Tracks byte order of segments |
| Acknowledgment Number | 32 bits | Next expected byte from sender |
| Data Offset | 4 bits | Header length in 32-bit words |
| Flags | 9 bits | Control bits — SYN, ACK, FIN, RST, PSH, URG |
| Window Size | 16 bits | Number of bytes sender can receive before ACK |
| Checksum | 16 bits | Error detection for header and data |
| Urgent Pointer | 16 bits | Points to urgent data if URG flag is set |

### TCP Flags

| Flag | Name | Description |
|------|------|-------------|
| SYN | Synchronize | Initiates a connection |
| ACK | Acknowledge | Confirms receipt of data |
| FIN | Finish | Gracefully closes a connection |
| RST | Reset | Abruptly terminates a connection |
| PSH | Push | Tells receiver to pass data to application immediately |
| URG | Urgent | Data in this segment should be prioritized |

---

## TCP Three-Way Handshake

Before any data is sent, TCP establishes a connection using
a three-way handshake.

```
Client                          Server
  │                               │
  │ ── SYN (SEQ=100) ──────────►  │   Step 1: Client requests connection
  │                               │
  │ ◄── SYN-ACK (SEQ=200, ACK=101)│   Step 2: Server acknowledges and syncs
  │                               │
  │ ── ACK (ACK=201) ──────────►  │   Step 3: Client acknowledges
  │                               │
  │        [Data transfer]        │
```

| Step | Sender | Flags | Description |
|------|--------|-------|-------------|
| 1 | Client | SYN | Client sends initial sequence number |
| 2 | Server | SYN + ACK | Server acknowledges and sends its own sequence number |
| 3 | Client | ACK | Client acknowledges server sequence number |

> After the three-way handshake the connection is established and
> data transfer begins.

---

## TCP Connection Termination — Four-Way Handshake

TCP closes connections gracefully using four steps.

```
Client                          Server
  │                               │
  │ ── FIN ────────────────────►  │   Step 1: Client signals end of data
  │                               │
  │ ◄── ACK ──────────────────── │   Step 2: Server acknowledges
  │                               │
  │ ◄── FIN ──────────────────── │   Step 3: Server signals end of data
  │                               │
  │ ── ACK ────────────────────►  │   Step 4: Client acknowledges
  │                               │
  │        [Connection closed]    │
```

> RST immediately terminates a connection without the graceful teardown.
> RST is sent when a connection is invalid, rejected, or forcibly closed.

---

## TCP Reliability — Sequence and Acknowledgment

TCP tracks every byte using sequence numbers.

```
Sender sends:    SEQ=1    SEQ=2    SEQ=3    SEQ=4
                  ──►      ──►      ──►      ──►

Receiver replies:         ACK=2            ACK=4   (cumulative)

If SEQ=3 is lost:
Receiver sends:                   ACK=3            (requesting retransmit)
Sender retransmits:                        SEQ=3 ──►
```

| Mechanism | Description |
|-----------|-------------|
| Sequence numbers | Track order of bytes sent |
| Acknowledgment numbers | Confirm bytes received — value = next expected byte |
| Retransmission | Sender retransmits unacknowledged segments after timeout |
| Duplicate ACK | Three duplicate ACKs trigger fast retransmit |

---

## TCP Flow Control — Sliding Window

The window size tells the sender how many bytes the receiver
can accept before requiring an acknowledgment.

```
Window size = 3000 bytes

Sender:   [SEG1][SEG2][SEG3] ──► (sends up to window size without waiting)
Receiver: ◄── ACK=3001, Window=3000 (acknowledges and slides window forward)
Sender:   [SEG4][SEG5][SEG6] ──► (sends next window)
```

| Condition | Window Behavior |
|-----------|----------------|
| Receiver buffer filling up | Window size decreases |
| Receiver buffer full | Window size = 0 (sender pauses) |
| Receiver buffer clears | Window size increases again |

> This prevents a fast sender from overwhelming a slow receiver.

---

## TCP Congestion Control

TCP also monitors network congestion and adjusts its sending rate.

| Phase | Description |
|-------|-------------|
| Slow Start | Begins with small window, doubles each RTT until threshold |
| Congestion Avoidance | Increases window linearly after threshold |
| Fast Retransmit | Retransmits on 3 duplicate ACKs without waiting for timeout |
| Fast Recovery | Reduces window by half on congestion, resumes from there |

---

## UDP — User Datagram Protocol

UDP is a lightweight, connectionless protocol.
It sends data without establishing a connection or guaranteeing delivery.

### UDP Header

```
┌──────────────────┬───────────────────┐
│   Source Port    │  Destination Port  │  (16 bits each)
├──────────────────┼───────────────────┤
│     Length       │     Checksum       │  (16 bits each)
├──────────────────┴───────────────────┤
│                 Data                  │
└───────────────────────────────────────┘
```

| Field | Size | Description |
|-------|------|-------------|
| Source Port | 16 bits | Sending application port |
| Destination Port | 16 bits | Receiving application port |
| Length | 16 bits | Length of UDP header and data |
| Checksum | 16 bits | Optional error detection |

> UDP header is only 8 bytes — much lighter than TCP's 20 bytes.
> No sequence numbers, no ACKs, no retransmission.

### When UDP is Preferred

| Scenario | Reason |
|----------|--------|
| VoIP / video calls | Latency matters more than occasional lost packet |
| Live video streaming | Retransmission would cause buffering |
| DNS queries | Short single request/reply — overhead not worth it |
| DHCP | Broadcast-based — connection not possible before IP is assigned |
| SNMP | Polling — occasional loss acceptable |
| Online gaming | Speed and low latency are critical |
| TFTP | Simple file transfer — application handles reliability |

---

## Port Numbers

Port numbers identify which application or service the data belongs to.

### Port Ranges

| Range | Name | Description |
|-------|------|-------------|
| 0–1023 | Well-known ports | Reserved for standard services |
| 1024–49151 | Registered ports | Used by vendor applications |
| 49152–65535 | Ephemeral / Dynamic ports | Assigned temporarily to client-side connections |

### Well-Known Port Numbers

| Port | Protocol | Service |
|------|----------|---------|
| 20 | TCP | FTP Data |
| 21 | TCP | FTP Control |
| 22 | TCP | SSH |
| 23 | TCP | Telnet |
| 25 | TCP | SMTP |
| 53 | TCP + UDP | DNS |
| 67 | UDP | DHCP Server |
| 68 | UDP | DHCP Client |
| 69 | UDP | TFTP |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 143 | TCP | IMAP |
| 161 | UDP | SNMP |
| 162 | UDP | SNMP Trap |
| 179 | TCP | BGP |
| 389 | TCP | LDAP |
| 443 | TCP | HTTPS |
| 514 | UDP | Syslog |
| 636 | TCP | LDAPS |
| 3389 | TCP | RDP |
| 5060 | TCP + UDP | SIP (VoIP) |
| 5061 | TCP | SIP over TLS |

> DNS uses both TCP and UDP.
> UDP for standard queries (under 512 bytes).
> TCP for zone transfers and large responses.

---

## Multiplexing and Demultiplexing

Layer 4 allows multiple applications on the same host to
use the network simultaneously.

```
Host A

App 1 (Browser)    ──► Source Port 50001 ──► Dest Port 443  ──► Web Server
App 2 (Email)      ──► Source Port 50002 ──► Dest Port 25   ──► Mail Server
App 3 (SSH)        ──► Source Port 50003 ──► Dest Port 22   ──► SSH Server
```

The combination of source IP + source port + destination IP + destination port
is called a **socket** — it uniquely identifies every connection.

| Component | Example |
|-----------|---------|
| Source IP | 192.168.1.10 |
| Source Port | 50001 |
| Destination IP | 93.184.216.34 |
| Destination Port | 443 |
| Socket pair | 192.168.1.10:50001 ↔ 93.184.216.34:443 |

---

## TCP vs UDP — When to Use Which

| Use TCP when... | Use UDP when... |
|-----------------|-----------------|
| Data must arrive complete and in order | Speed is more important than reliability |
| File transfer | Real-time audio or video |
| Web browsing | DNS resolution |
| Email | DHCP |
| Remote access (SSH, RDP) | Live streaming |
| Database transactions | Online gaming |

---

## Layer 4 in the Context of the OSI Model

| Layer | Name | PDU | Address Used |
|-------|------|-----|-------------|
| Layer 5 | Session | Data | — |
| Layer 4 | Transport | Segment | Port number |
| Layer 3 | Network | Packet | IP address |
| Layer 2 | Data Link | Frame | MAC address |
| Layer 1 | Physical | Bits | — |

> The PDU at Layer 4 is called a segment (TCP) or datagram (UDP).

---

## Key Cisco Commands — Layer 4

```bash
R1# show ip socket                        // View active sockets
R1# show tcp brief                        // View TCP connections
R1# show udp                              // View UDP sessions
R1# debug ip tcp transactions             // Debug TCP connection events
```

```bash
PC> netstat -an                           // View all active connections and ports (Windows/Linux)
PC> netstat -b                            // Show which application owns each connection (Windows)
```

---

## Summary

- Layer 4 provides end-to-end communication between applications using port numbers
- TCP is connection-oriented — reliable, ordered, with flow and congestion control
- UDP is connectionless — fast, lightweight, no guarantee of delivery
- TCP uses a three-way handshake (SYN, SYN-ACK, ACK) to establish connections
- TCP uses sequence and acknowledgment numbers to ensure reliable delivery
- UDP is preferred for real-time applications where speed matters more than reliability
- Port numbers 0–1023 are well-known — memorize the key ones for the CCNA exam
- A socket is the unique combination of source IP, source port, destination IP, destination port
- DNS uses both TCP and UDP — queries on UDP, zone transfers on TCP

