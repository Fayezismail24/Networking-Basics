# Class B IP Address Overview

| Class Range  | Subnet Mask    | Binary                               |
|-------------|---------------|--------------------------------------|
| Start IP    | 128.0.0.0     | 11111111.11111111.00000000.00000000 |
| End IP      | 191.255.255.255 |                                      |

- The **first two bytes (16 bits)** denote the **network**.  
  - Total networks: 2¹⁶ = 16,384  

- The **remaining 2 bytes (16 bits)** denote the **hosts**.  
  - Total hosts per network: 2¹⁶ − 2 = 65,534
 





| Category          | Details        |
| ----------------- | -------------- |
| Network ID        | 172.16.0.0     |
| First Usable Host | 172.16.0.1     |
| Last Usable Host  | 172.16.255.254 |
| Broadcast ID      | 172.16.255.255 |
