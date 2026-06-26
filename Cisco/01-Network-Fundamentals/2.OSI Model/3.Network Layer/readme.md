

# Network Layer (OSI Layer 3)

## What is the Network Layer?

The Network Layer is the third layer of the OSI model.
It sits between the Data Link Layer (Layer 2) and the Transport Layer (Layer 4).

Its job is to deliver packets between devices across different networks.
Unlike Layer 2 which only moves frames between directly connected devices,
Layer 3 can route data across multiple networks to reach a destination
anywhere in the world.

Layer 3 works with IP addresses — not MAC addresses.

---

## Responsibilities

- Logical addressing — assigning and using IP addresses
- Routing — determining the best path to the destination network
- Packet forwarding — moving packets hop by hop toward the destination
- Encapsulation — wrapping Layer 4 segments into packets
- Fragmentation — splitting packets too large for the next link (IPv4 only)

---

## Layer 3 vs Layer 2 — Key Difference

| Feature | Layer 2 | Layer 3 |
|---------|---------|---------|
| Address used | MAC address | IP address |
| Scope | Local segment only | Across multiple networks |
| Device | Switch | Router |
| PDU | Frame | Packet |
| Changes hop to hop | No (end to end) | Yes — MAC changes every hop |

> MAC addresses change at every router hop.
> IP addresses stay the same end to end.

---

## IPv4 Addressing

### Format

IPv4 is a 32-bit address written in dotted decimal notation.

```
192     .     168     .       1     .       10
 8 bits         8 bits         8 bits         8 bits
└─────────────────────────────────────────────────┘
                    32 bits total
```

### Address Classes (Classful — Legacy)

| Class | First Octet Range | Default Mask | Use |
|-------|------------------|--------------|-----|
| A | 1–126 | /8 (255.0.0.0) | Large networks |
| B | 128–191 | /16 (255.255.0.0) | Medium networks |
| C | 192–223 | /24 (255.255.255.0) | Small networks |
| D | 224–239 | N/A | Multicast |
| E | 240–255 | N/A | Reserved / experimental |

> 127.x.x.x is reserved for loopback — not a Class A usable range.
> Classful addressing is legacy — modern networks use CIDR.

### Private IP Ranges (RFC 1918)

| Range | CIDR | Class |
|-------|------|-------|
| 10.0.0.0 – 10.255.255.255 | 10.0.0.0/8 | A |
| 172.16.0.0 – 172.31.255.255 | 172.16.0.0/12 | B |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 | C |

> Private addresses are not routable on the internet.
> NAT is used to translate private addresses to a public IP.

### Special Addresses

| Address | Purpose |
|---------|---------|
| 127.0.0.1 | Loopback — tests local TCP/IP stack |
| 0.0.0.0 | Unspecified — used in routing as default route |
| 255.255.255.255 | Limited broadcast — all devices on local segment |
| 169.254.x.x | APIPA — auto-assigned when DHCP fails |

---

## Subnetting

Subnetting divides a network into smaller segments.
Each subnet has three key addresses:

| Address | Description |
|---------|-------------|
| Network address | First address — identifies the subnet (not assignable) |
| Usable host range | All addresses between network and broadcast |
| Broadcast address | Last address — sent to all hosts in subnet (not assignable) |

### Subnet Mask Cheat Sheet

| CIDR | Subnet Mask | Hosts per Subnet |
|------|-------------|-----------------|
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /29 | 255.255.255.248 | 6 |
| /30 | 255.255.255.252 | 2 |
| /31 | 255.255.255.254 | 2 (point-to-point, RFC 3021) |
| /32 | 255.255.255.255 | 1 (host route) |

> Formula: usable hosts = 2^(host bits) - 2
> /30 is standard for point-to-point links between routers.

### Example — Subnetting 192.168.1.0/26

| Field | Value |
|-------|-------|
| Subnet mask | 255.255.255.192 |
| Network address | 192.168.1.0 |
| First usable host | 192.168.1.1 |
| Last usable host | 192.168.1.62 |
| Broadcast | 192.168.1.63 |
| Total usable hosts | 62 |

---

## IPv4 Packet Structure

```
┌──────┬──────┬──────────┬───────────┬────────┬──────┬──────────────────┬─────────────┬────────────┬──────────┐
│  Ver │  IHL │   DSCP   │    ECN    │  Total │  ID  │ Flags / Fragment │     TTL     │  Protocol  │ Checksum │
│  4b  │  4b  │   6b     │    2b     │  Length│  16b │     Offset 13b   │    8b       │    8b      │   16b    │
├──────┴──────┴──────────┴───────────┴────────┴──────┴──────────────────┴─────────────┴────────────┴──────────┤
│                                        Source IP Address (32 bits)                                           │
├──────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                     Destination IP Address (32 bits)                                         │
├──────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                    Options (if IHL > 5) + Padding                                            │
├──────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                             Payload (Data)                                                   │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

| Field | Size | Description |
|-------|------|-------------|
| Version | 4 bits | IP version — 4 for IPv4 |
| IHL | 4 bits | Internet Header Length — number of 32-bit words in the header |
| DSCP | 6 bits | Differentiated Services — QoS marking |
| ECN | 2 bits | Explicit Congestion Notification |
| Total Length | 16 bits | Total size of packet including header and data |
| ID | 16 bits | Identifies fragments of the same original packet |
| Flags | 3 bits | DF (Don't Fragment), MF (More Fragments) |
| Fragment Offset | 13 bits | Position of fragment in original packet |
| TTL | 8 bits | Time to Live — decremented by 1 at each router hop, dropped at 0 |
| Protocol | 8 bits | Identifies Layer 4 protocol (6 = TCP, 17 = UDP, 1 = ICMP) |
| Header Checksum | 16 bits | Error checking for the header only |
| Source IP | 32 bits | Sender IP address |
| Destination IP | 32 bits | Receiver IP address |

### Common Protocol Field Values

| Value | Protocol |
|-------|----------|
| 1 | ICMP |
| 6 | TCP |
| 17 | UDP |
| 89 | OSPF |
| 47 | GRE |

---

## TTL — Time to Live

TTL prevents packets from looping forever in the network.

| Event | TTL Behavior |
|-------|-------------|
| Packet leaves a host | TTL set (Windows default = 128, Linux/Cisco = 64) |
| Packet passes through a router | TTL decremented by 1 |
| TTL reaches 0 | Router discards packet and sends ICMP Time Exceeded back to source |

> TTL is a Layer 3 loop prevention mechanism.
> Traceroute works by intentionally sending packets with TTL = 1, 2, 3...
> and reading the ICMP Time Exceeded replies from each hop.

---

## Routing

Routing is the process of selecting the best path for a packet to reach
its destination network.

### Routing Table

Every router maintains a routing table — a list of known networks
and how to reach them.

```bash
R1# show ip route
```

```
C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
L    192.168.1.1/32 is directly connected, GigabitEthernet0/0
S    10.0.0.0/8 [1/0] via 203.0.113.1
O    172.16.0.0/16 [110/2] via 192.168.2.2
```

### Route Source Codes

| Code | Source | Description |
|------|--------|-------------|
| C | Connected | Directly connected network |
| L | Local | The router's own interface IP (/32) |
| S | Static | Manually configured route |
| O | OSPF | Learned via OSPF |
| E | EIGRP | Learned via EIGRP |
| R | RIP | Learned via RIP |
| B | BGP | Learned via BGP |

### Administrative Distance (AD)

AD determines which routing source is trusted most when multiple sources
know a route to the same destination.

| Route Source | AD |
|-------------|-----|
| Connected | 0 |
| Static | 1 |
| EIGRP summary | 5 |
| BGP (external) | 20 |
| EIGRP (internal) | 90 |
| OSPF | 110 |
| IS-IS | 115 |
| RIP | 120 |
| Unknown / Unreachable | 255 |

> Lower AD = more trusted.
> AD 255 = route is never used.

### Metric

Metric is used to choose between multiple routes learned from
the same routing protocol.

| Protocol | Metric Used |
|----------|------------|
| RIP | Hop count |
| OSPF | Cost (based on bandwidth) |
| EIGRP | Composite (bandwidth + delay) |
| BGP | AS path length + attributes |

> Lower metric = better route.

---

## Routing Types

### Static Routing

Manually configured by the network administrator.

```bash
R1(config)# ip route 10.0.0.0 255.255.255.0 192.168.1.2
```

| Type | Command | Description |
|------|---------|-------------|
| Static route | ip route [network] [mask] [next-hop] | Manual path to a network |
| Default route | ip route 0.0.0.0 0.0.0.0 [next-hop] | Catch-all — used when no specific match exists |
| Floating static | ip route ... [AD higher than dynamic] | Backup route — only used if dynamic route fails |

### Dynamic Routing

Routers exchange routing information automatically using a protocol.

| Protocol | Type | Algorithm | AD | Use Case |
|----------|------|-----------|-----|----------|
| RIP v2 | Distance vector | Bellman-Ford | 120 | Small legacy networks |
| EIGRP | Advanced distance vector | DUAL | 90 | Cisco environments |
| OSPF | Link state | Dijkstra (SPF) | 110 | Most common in enterprise |
| BGP | Path vector | Best path selection | 20 (eBGP) | Internet routing between ASes |

---

## Packet Forwarding Process

When a router receives a packet it follows this logic:

```
1. Strip the Layer 2 frame — read the destination IP in the Layer 3 header
2. Look up destination IP in the routing table
3. Find the longest prefix match
4. Decrement TTL by 1 — if TTL = 0, discard and send ICMP Time Exceeded
5. Determine the exit interface and next-hop IP
6. ARP for the next-hop MAC address (if not cached)
7. Build a new Layer 2 frame with new source and destination MACs
8. Forward the frame out the exit interface
```

> The IP packet payload never changes hop to hop.
> The Layer 2 frame is rebuilt at every hop with new MAC addresses.

---

## ICMP — Internet Control Message Protocol

ICMP operates at Layer 3. It is used for diagnostics and error reporting.

| Message Type | Code | Description |
|-------------|------|-------------|
| Echo Request | Type 8 | Sent by ping |
| Echo Reply | Type 0 | Response to ping |
| Destination Unreachable | Type 3 | No route to host or port closed |
| Time Exceeded | Type 11 | TTL reached 0 — used by traceroute |
| Redirect | Type 5 | Router tells host to use a better gateway |

### Key Commands

```bash
R1# ping 8.8.8.8
R1# ping 8.8.8.8 source GigabitEthernet0/0
R1# traceroute 8.8.8.8
```

---

## NAT — Network Address Translation

NAT translates private IP addresses to a public IP address at the
boundary between a private network and the internet.

| Type | Description |
|------|-------------|
| Static NAT | One private IP maps to one public IP — 1:1 |
| Dynamic NAT | Pool of public IPs — assigned dynamically |
| PAT (NAT Overload) | Many private IPs share one public IP using port numbers — most common |

> PAT is what home routers and most enterprise edge routers use.
> Also called NAT Overload or many-to-one NAT.

---

## IPv6 — Brief Overview

IPv6 is the successor to IPv4, using 128-bit addresses.

| Feature | IPv4 | IPv6 |
|---------|------|------|
| Address size | 32 bits | 128 bits |
| Notation | Dotted decimal | Colon-separated hex |
| Address space | ~4.3 billion | 340 undecillion |
| Header size | Variable (20–60 bytes) | Fixed 40 bytes |
| Fragmentation | Router or host | Host only |
| Broadcast | Yes | No — replaced by multicast |
| ARP | Yes | No — replaced by NDP |
| Configuration | Manual or DHCP | SLAAC, DHCPv6, or manual |

### IPv6 Address Types

| Type | Prefix | Description |
|------|--------|-------------|
| Global Unicast | 2000::/3 | Routable on the internet — equivalent to public IPv4 |
| Link-Local | FE80::/10 | Auto-configured — local segment only, not routed |
| Loopback | ::1/128 | Equivalent to 127.0.0.1 |
| Unique Local | FC00::/7 | Equivalent to RFC 1918 private ranges |
| Multicast | FF00::/8 | Replaces broadcast |
| Anycast | From unicast space | Sent to nearest member of a group |

---

## Layer 3 Devices

| Device | Role |
|--------|------|
| Router | Primary Layer 3 device — routes packets between networks |
| Layer 3 Switch | Switches at Layer 2 and routes at Layer 3 using SVIs or routed ports |
| Multilayer Switch | Another term for Layer 3 switch |
| Firewall | Can operate at Layer 3 and above — filters traffic based on IP |

---

## Key Cisco Commands — Layer 3

```bash
R1# show ip route                        // View routing table
R1# show ip interface brief              // View interface IPs and status
R1# show ip arp                          // View ARP table
R1# show ip protocols                    // View running routing protocols
R1# ping 192.168.1.1                     // Test reachability
R1# traceroute 192.168.1.1               // Trace path to destination
R1(config)# ip route 0.0.0.0 0.0.0.0 [next-hop]   // Default route
R1(config)# ip route [net] [mask] [next-hop]        // Static route
```

---

## Summary

- Layer 3 delivers packets between different networks using IP addresses
- IPv4 is 32-bit — written in dotted decimal, divided into network and host portions
- Subnetting divides networks into smaller segments — /30 for point-to-point, /24 for LANs
- Routers forward packets hop by hop — IP stays the same, MAC changes every hop
- Routing table is the core — connected, static, and dynamic routes
- AD determines which routing source wins — lower is more trusted
- TTL prevents infinite loops — decremented by 1 at each router hop
- ICMP handles diagnostics — ping uses echo request/reply, traceroute uses TTL expiry
- NAT translates private IPs to public — PAT is the most common form
- IPv6 uses 128-bit addresses and replaces ARP with NDP, broadcast with multicast



