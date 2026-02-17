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

### **Key Takeaways for MTCNA Candidates**

* **The "Bundle":** In modern RouterOS versions (v7+), most "Advanced" features are now integrated into the main `routeros` bundle, but some (like **The Dude** or **User Manager**) still require separate `.npk` file installations depending on your hardware architecture.
* **Winbox vs. WWW:** These aren't just "services"; they are part of the System packages that allow you to interact with the router.
