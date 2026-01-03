
| Class Range | Subnet Mask | Binary |
|-------------|-------------|--------|
| Start IP    | 0.0.0.0     | 11111111.00000000.00000000.00000000 |
| End IP      | 127.255.255.255 |        |

- The first byte (8 bits) denotes the **network**.
  - Total networks: 2⁸ = 256

- The remaining 3 bytes (24 bits) denote the **hosts**.
  - Total hosts per network: 2²⁴ − 2  = 16,777,214







| Category           | Details          |
|-------------------|-----------------|
| Network ID        | 10.0.0.0        |
| First Usable Host | 10.0.0.1        |
| Last Usable Host  | 10.255.255.254  |
| Broadcast ID      | 10.255.255.255  |




































# IP Address Breakdown (Class A)

| Category                     | Details                                      |
|-------------------------------|---------------------------------------------|
| IP Address                    | 10.1.2.3/8                                  |
| Network Part                  | 10                                          |
| Host Part                     | 1.2.3                                       |
| Subnet Mask                   | 255.0.0.0 (/8)                              |
| Same Network Examples         | 10.0.0.1<br>10.5.20.7<br>10.255.255.254   |
| Different Network Examples    | 11.0.0.1 ❌<br>9.1.1.1 ❌                  |
| Key Rule                      | Same first octet (10) + /8 → Same network → Direct communication possible |
