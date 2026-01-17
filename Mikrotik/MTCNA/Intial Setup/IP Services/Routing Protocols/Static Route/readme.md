



# MikroTik Static Routing Lab 🌐

This project demonstrates the configuration of manual static routes between two MikroTik routers to bridge communication between isolated subnets.

## 📋 Topology Details

| Device | Interface | IP Address | Purpose |
| --- | --- | --- | --- |
| **Router A** | ether1 | `192.168.3.1/24` | Link to Router B |
| **Router A** | ether2 | `192.168.1.1/24` | Local Gateway |
| **Router B** | ether1 | `192.168.3.2/24` | Link to Router A |
| **Router B** | ether2 | `192.168.2.1/24` | Local Gateway |

---

## ⚙️ Configuration (Terminal)

### 1. Router A Configuration

To reach the `192.168.2.0` network, Router A must send traffic to Router B's interconnect IP.

```routeros
# Set interface IPs
/ip address add address=192.168.3.1/24 interface=ether1
/ip address add address=192.168.1.1/24 interface=ether2

# Add the Static Route
/ip route add dst-address=192.168.2.0/24 gateway=192.168.3.2 comment="Route to LAN 2"

```

### 2. Router B Configuration

Router B needs a return path to reach the `192.168.1.0` network.

```routeros
# Set interface IPs
/ip address add address=192.168.3.2/24 interface=ether1
/ip address add address=192.168.2.1/24 interface=ether2

# Add the Static Route
/ip route add dst-address=192.168.1.0/24 gateway=192.168.3.1 comment="Route to LAN 1"

```

---

## ✅ Verification

Use these commands to verify the routing table and end-to-end connectivity:

* **View Routing Table**: `/ip route print` (Verify the `AS` flag is present)
* **Ping Test**: `/ping 192.168.2.2` (Pinging PC-B from Router A)
* **Traceroute**: `/tool traceroute 192.168.2.2`

---

### 💡 Markdown Tip for GitHub

For a table to render correctly, ensure there is a **blank line** above the table. If it still looks like plain text, check that you haven't missed any pipe `|` characters or the alignment row `| :--- |`.

Would you like me to add a section for **Firewall Filter Rules** to ensure the traffic isn't dropped by the default MikroTik configuration?
