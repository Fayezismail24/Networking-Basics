# Objective: Configure IP Address Pools for SSTP

Before enabling the SSTP (Secure Socket Tunneling Protocol) server, we must define the range of IP addresses that will be dynamically assigned to VPN interfaces. This ensures that every connecting client receives a unique IP address within a controlled, isolated subnet.

## 1. Define the IP Pool
We will create a pool named `sstp-pool` to manage a range of 50 available addresses for remote clients.

## 2. Local vs. Remote Address Logic
When configuring the PPP Profile in the next step, these addresses serve two distinct roles:

- **Local Address**: This represents the Gateway IP that the MikroTik router will assume inside the tunnel (e.g., `172.16.1.1`). It acts as the "near end" of the point-to-point link.

- **Remote Address**: This refers to the `sstp-pool` we created above. The router will pull a unique address from this range and assign it to the connecting client's virtual interface (the "far end").

> **Note**: The Local Address does not necessarily have to be a pool; it can be a single static IP (the Gateway). Only the Remote Address strictly requires a pool if you have multiple users connecting simultaneously.

<img width="438" height="278" alt="image" src="https://github.com/user-attachments/assets/f2ecc11f-71b3-4dc8-8db3-f586aa241607" />
