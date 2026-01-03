| Class Range | Subnet Mask | Binary |
|-------------|-------------|--------|
| Start IP    | 0.0.0.0     | 11111111.00000000.00000000.00000000 |
| End IP      | 127.255.255.255 |        |

- The first byte (8 bits) denotes the **network**.
  - Total networks: 2⁸ = 256

- The remaining 3 bytes (24 bits) denote the **hosts**.
  - Total hosts per network: 2²⁴ = 16,777,216


🌐 IP Address Breakdown (Class A)   📌 IP Address  10.1.2.3/8

🧩 Address Structure

🟦 Network part → 10      🟩 Host part → 1.2.3 📘 Because the subnet mask is /8 (255.0.0.0):



Only the first octet defines the network


Any IP starting with 10.x.x.x belongs to the same network



✅ SAME Network (Ping ✔️)
10.0.0.1
10.5.20.7
10.255.255.254



❌ DIFFERENT Network (Ping ✖️)
11.0.0.1   ❌
9.1.1.1    ❌



🔑 Key Rule

Same first octet (10) + same subnet mask (/8)
➡️ Same network
➡️ Direct communication (no router needed)
