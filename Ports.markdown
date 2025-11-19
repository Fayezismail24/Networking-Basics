Skip to content
Navigation Menu
Fayezismail24
Networking-Basics

Type / to search
Code
Issues
Pull requests
Actions
Projects
Wiki
Security
Insights
Settings
Files
Go to file
CCNA-Configuration
Nmap.md
README.md
Networking-Basics
/
Name your file...
in
main

Edit

Preview
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
101
102
103
104
105
106
107
108
109
110
111
112
113
114
115
116
117
118
119
120
121
122
123
124
125
126
127
128
129
# 🔌 Common Ports and What They Do

A clean reference list of the most common networking ports and their functions.

---

## 🔹 Ports 0 to 20
| Port | Service | Description |
|------|---------|-------------|
| **20** | FTP Data | File transfers |
| **21** | FTP Control | Login and control |
| **22** | SSH | Secure remote login |
| **23** | Telnet | Unencrypted remote login |
| **25** | SMTP | Email transfer |

---

## 🔹 Ports 30 to 70
| Port | Service | Description |
|------|---------|-------------|
| **53** | DNS | Domain to IP resolution |
| **67** | DHCP Server | Assigns IP addresses |
| **68** | DHCP Client | Receives IP |
| **69** | TFTP | Simple file transfer |

---

## 🔹 Ports 80 to 110
| Port | Service | Description |
|------|---------|-------------|
| **80** | HTTP | Web traffic |
| **110** | POP3 | Email download |

---

## 🔹 Ports 111 to 161
| Port | Service | Description |
|------|---------|-------------|
| **123** | NTP | Time sync |
| **135** | RPC | Windows services |
| **137** | NetBIOS-NS | Windows name service |
| **138** | NetBIOS-DGM | File sharing traffic |
| **139** | NetBIOS-SSN | SMB file sharing |
| **143** | IMAP | Email retrieval |
| **161** | SNMP | Network monitoring |

---

## 🔹 Ports 389 to 443
| Port | Service | Description |
|------|---------|-------------|
| **389** | LDAP | Directory services |
| **443** | HTTPS | Secure web |

---

## 🔹 Ports 445 to 587
| Port | Service | Description |
|------|---------|-------------|
| **445** | SMB | Windows file sharing |
| **514** | Syslog | Device logs |
| **515** | LPD | Printer service |
| **543** | Kerberos | Authentication |
| **587** | SMTP Submission | Authenticated email |

---

## 🔹 Ports 631 to 993
| Port | Service | Description |
|------|---------|-------------|
| **631** | IPP | Modern printing |
| **636** | LDAPS | Secure LDAP |
| **989** | FTPS Data | Secure FTP data |
| **990** | FTPS Control | Secure FTP login |
| **993** | IMAPS | Secure IMAP |

---

## 🔹 Ports 995 to 3389
| Port | Service | Description |
|------|---------|-------------|
| **995** | POP3S | Secure POP3 |
| **1433** | MSSQL | SQL Server |
| **1521** | Oracle DB | Oracle SQL |
| **1723** | PPTP | VPN |
| **2049** | NFS | Linux file sharing |
| **2082** | cPanel | Hosting panel |
| **2083** | cPanel SSL | Secure cPanel |
| **2181** | Zookeeper | Distributed systems |
| **3306** | MySQL | Database |
| **3389** | RDP | Remote Desktop |

---

## 🔹 Ports 4000 to 6379
| Port | Service | Description |
|------|---------|-------------|
| **4369** | EPMD | Erlang services |
| **5000** | UPnP | Device discovery |
| **5432** | PostgreSQL | Database |
| **5672** | RabbitMQ | Message queue |
| **5900** | VNC | Remote GUI |
| **5985** | WinRM HTTP | Remote PowerShell |
| **5986** | WinRM HTTPS | Secure PowerShell |
| **6379** | Redis | In-memory DB |

---

## 🔹 Ports 8000 to 9000
| Port | Service | Description |
|------|---------|-------------|
| **8080** | HTTP-alt | Proxy or alt web |
| **8081** | Admin panels | Web admin |
| **8443** | HTTPS-alt | Secure admin |
| **8888** | Dev servers | Tools |
| **9000** | SonarQube | Dev tools |

---

## 🔹 Ports 9000 to 10000
| Port | Service | Description |
|------|---------|-------------|
| **9090** | Web dashboards | Monitoring |
| **9200** | Elasticsearch | Search engine |
| **9300** | ES Cluster | Node communication |
| **10000** | Webmin | Server administration |

---

 