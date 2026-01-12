

```md
# MikroTik Basic WAN + LAN Setup (Bridge, DHCP, DNS)

This guide explains a **clean and correct MikroTik setup** with:
- One WAN interface
- One LAN bridge (wired + wireless)
- DHCP and DNS for LAN clients

---

## Before We Start: What Do We Need and Why?

If you are new to networking, don’t worry.  
We only need **three basic ideas** to make a home or small office network work:

- A **DHCP Client**
- A **Bridge**
- A **DHCP Server**

Think of the router as a **middleman** between the internet and your devices.

---

### 1️⃣ DHCP Client (Getting Internet)

A **DHCP Client** is used when a device needs to **receive an IP address automatically**.

In this setup:
- The MikroTik router connects to the internet through **ether1**
- The router does not know the internet IP by itself
- So it asks the ISP router or modem for an IP

Simple idea:
- **DHCP Client = asking for an IP**

Used on:
- **WAN (ether1)**
- Never on LAN

---

### 2️⃣ Bridge (Putting LAN Ports Together)

A **Bridge** is like a **network switch inside the router**.

Why we need it:
- We have multiple LAN interfaces:
  - ether2 (cable)
  - wlan1 (WiFi)
  - wlan2 (WiFi)
- We want all of them to behave as **one network**

Simple idea:
- **Bridge = group ports together**

After bridging:
- A phone on WiFi
- A PC on cable  
can talk to each other and use the same network.

---

### 3️⃣ DHCP Server (Giving IPs to Devices)

A **DHCP Server** does the opposite of a DHCP Client.

It:
- Gives IP addresses to devices
- Tells them:
  - Their IP address
  - Their gateway (the router)
  - Their DNS

Simple idea:
- **DHCP Server = giving IPs**

Used on:
- **LAN (bridge)**

---

### One Simple Rule to Remember

- **WAN asks for IP** → DHCP Client
- **LAN gives IP** → DHCP Server

If you understand this rule, networking will make sense.

---

## Network Roles (Important)

- **ether1 = WAN (upstream / internet)**
- **ether2 = LAN**
- **wlan1 + wlan2 = LAN**
- **LAN = bridge on ether2 + wlan1 + wlan2**

---

## 1️⃣ DHCP Client on ether1 (WAN)

### Configuration
```bash
/ip dhcp-client /add interface=ether1 disabled=no
````

---

## 2️⃣ Create LAN Bridge (ether2 + wlan1 + wlan2)

```bash
/interface bridge /add name=LAN
/interface bridge port /add bridge=LAN interface=ether2
/interface bridge port /add bridge=LAN interface=wlan1
/interface bridge port /add bridge=LAN interface=wlan2
```

---

## 3️⃣ Assign IP Address to LAN Bridge

```bash
/ip address /add address=192.168.10.1/24 interface=LAN
```

---

## 4️⃣ DHCP Server on LAN Bridge

```bash
/ip dhcp-server /setup
```

Values:

```
Interface: LAN
Network: 192.168.10.0/24
Gateway: 192.168.10.1
Pool: 192.168.10.10-192.168.10.254
DNS: 192.168.10.1
```

---

## 5️⃣ DNS Configuration

```bash
/ip dns /set allow-remote-requests=yes
```

Optional:

```bash
/ip dns /set servers=8.8.8.8,1.1.1.1
```

---

## 🧠 Final Network Topology

```
INTERNET / ISP
      |
   [ ether1 ]
   DHCP CLIENT
      |
  ┌── MikroTik ──┐
  |               |
[ LAN Bridge ] ← 192.168.10.1
  |      |      |
ether2  wlan1  wlan2
  |
LAN Clients (DHCP)
```

---

## ⚠️ Important Rule (Exam & Real Life)

* WAN **asks** for IP
* LAN **gives** IP

Putting a DHCP Client on LAN breaks network logic.


