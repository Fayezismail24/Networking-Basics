# Class B IP Address Overview

| Class Range  | Subnet Mask    | Binary                               |
|-------------|---------------|--------------------------------------|
| Start IP    | 128.0.0.0     | 11111111.11111111.00000000.00000000 |
| End IP      | 191.255.255.255 |                                      |

- The **first two bytes (16 bits)** denote the **network**.  
  - Total networks: 2¹⁶ = 65,534

- The **remaining 2 bytes (16 bits)** denote the **hosts**.  
  - Total hosts per network: 2¹⁶ − 2 = 65,534
 





| Category          | Details        |
| ----------------- | -------------- |
| Network ID        | 172.16.0.0     |
| First Usable Host | 172.16.0.1     |
| Last Usable Host  | 172.16.255.254 |
| Broadcast ID      | 172.16.255.255 |



| Category                   | Details                                                                                 |
| -------------------------- | --------------------------------------------------------------------------------------- |
| IP Address                 | 172.16.5.10/16                                                                          |
| Network Part               | 172.16                                                                                  |
| Host Part                  | 5.10                                                                                    |
| Subnet Mask                | 255.255.0.0 (/16)                                                                       |
| Same Network Examples      | 172.16.0.1<br>172.16.50.7<br>172.16.255.254                                             |
| Different Network Examples | 172.17.0.1 ❌<br>172.15.1.1 ❌                                                            |
| Key Rule                   | Same first **two octets** (172.16) + /16 → Same network → Direct communication possible |
