### **MikroTik RouterOS: Feature Classification**

| **Category** | **Default / Standard Functions** | **Advanced  Packages** |
| --- | --- | --- |
| **System** | Core configuration, device management, and identity. | User Manager (RADIUS), Container, Rose Storage. |
| **Routing** | Static routing, RIP, OSPF, and basic BGP. | MPLS, advanced BGP, and Routing Filters. |
| **Wireless** | 802.11 a/b/g/n/ac/ax support and CAPsMAN. | LTE/5G support, Wave2, and LoRa. |
| **Security** | Firewall (Filter, NAT, Mangle, Raw), and basic IPSec. | Advanced VPNs (WireGuard, OpenVPN, ZeroTier). |
| **IP Services** | DHCP Server/Client, DNS Cache, and ARP. | Radius client, Web Proxy, and TR-069. |
| **PPP** | PPPoE, PPTP, L2TP, and SSTP tunnels. | Traffic Flow (NetFlow) and sophisticated accounting. |
| **Monitoring** | Simple SNMP and local logging. | **The Dude** (Network monitoring server), Kid Control. |
| **Management** | Winbox, WebFig (WWW), SSH, and Telnet. | API and specialized Web management tools. |



| **Package Name**    | **Type**       | **Contents / Key Features**                                                                 |
|---------------------|----------------|--------------------------------------------------------------------------------------------|
| system              | Default        | Core functions: Bridging, IP, Firewall, NAT, Bandwidth-test, Neighbors.                    |
| advanced-tools      | Extra          | Includes Ip-scan, Netwatch, Wake-on-LAN, and SMS tool.                                     |
| dhcp                | Default        | All DHCP server and client capabilities.                                                   |
| ppp                 | Default        | Tunneling protocols: PPPoE, PPTP, L2TP, SSTP, and OVPN.                                  |
| routing             | Default        | Dynamic routing protocols like OSPF, BGP, and RIP.                                         |
| wireless            | Default        | Support for 802.11 wireless interfaces and CAPsMAN.                                         |
| user-manager        | Extra          | RADIUS server for Hotspot, PPP, and Wireless authentication.                              |
| dude                | Extra          | The Dude network monitoring server and visualization tool.                                |
| gps                 | Extra          | Support for GPS device data and location tracking.                                        |
| lte                 | Extra/Default  | Support for cellular modems and LTE interfaces.                                            |
| ups                 | Extra          | Monitoring and control for Uninterruptible Power Supplies via USB/Serial.                  |
| iot                 | Extra          | Support for LoRa, Bluetooth, and IoT-specific protocols (ROS v7).                          |
| container           | Extra          | Allows running Docker-style containers on supported hardware (ROS v7).                     |

