# Class C IP Address Overview

| Class Range  | Subnet Mask    | Binary                               |
|-------------|---------------|--------------------------------------|
| Start IP    | 192.0.0.0     | 11111111.11111111.11111111.00000000 |
| End IP      | 223.255.255.255 |                                      |

- The **first three octets (24 bits)** denote the **network**.  
  - Total networks: 2²⁴ = 16,777,216

- The **remaining 1 octet (8 bits)** denotes the **hosts**.  
  - Total usable hosts per network: 2⁸ − 2 = 254

