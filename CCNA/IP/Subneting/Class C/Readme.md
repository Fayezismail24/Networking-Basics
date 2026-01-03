# Class C IP Address Overview

| Class Range  | Subnet Mask    | Binary                               |
|-------------|---------------|--------------------------------------|
| Start IP    | 192.0.0.0     | 11111111.11111111.11111111.00000000 |
| End IP      | 223.255.255.255 |                                      |

- The **first three octets (24 bits)** denote the **network**.  
  - Total networks: 2²⁴ = 16,777,216

- The **remaining 1 octet (8 bits)** denotes the **hosts**.  
  - Total usable hosts per network: 2⁸ − 2 = 254

| Category          | Details        |
| ----------------- | -------------- |
| Network ID        | 192.168.1.0    |
| First Usable Host | 192.168.1.1    |
| Last Usable Host  | 192.168.1.254  |
| Broadcast ID      | 192.168.1.255  |



| Category                   | Details                                                                                 |
| -------------------------- | --------------------------------------------------------------------------------------- |
| IP Address                 | 192.168.1.10/24                                                                         |
| Network Part               | 192.168                                                                                  |
| Host Part                  | 1.10                                                                                     |
| Subnet Mask                | 255.255.255.0 (/24)                                                                      |
| Same Network Examples      | 192.168.1.1<br>192.168.1.50<br>192.168.1.254                                             |
| Different Network Examples | 192.168.2.1 ❌<br>192.167.1.1 ❌                                                         |
| Key Rule                   | Same first **three octets** (192.168.1) + /24 → Same network → Direct communication possible |
