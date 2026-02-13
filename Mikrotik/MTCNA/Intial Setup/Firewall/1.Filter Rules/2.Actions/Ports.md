Common SysAdmin Port Reference

As a System Administrator, you will apply these **DROP/REJECT** actions to these common ports to secure your infrastructure:

| Category | Port | Protocol | Service | SysAdmin Context |
| :--- | :--- | :--- | :--- | :--- |
| **Management** | **22** | TCP | **SSH** | Secure CLI access to Linux/MikroTik. |
| | **8291** | TCP | **WinBox** | MikroTik's GUI management port. |
| | **3389** | TCP | **RDP** | Remote Desktop for Windows Servers. |
| **Web** | **80 / 443** | TCP | **HTTP/S** | Web interfaces for management or sites. |
| **Network** | **53** | UDP/TCP | **DNS** | Resolving domain names to IP addresses. |
| | **67 / 68** | UDP | **DHCP** | Assigning IP addresses to local clients. |
| **Database** | **3306** | TCP | **MySQL** | Database traffic (Usually REJECTED on LAN). |
| | **5432** | TCP | **PostgreSQL**| Database traffic. |
| **Monitoring** | **161** | UDP | **SNMP** | Monitoring router health and stats.
