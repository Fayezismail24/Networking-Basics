
## 🛠️ NAT Directionality

### 1. Destination NAT (DST-NAT) = "The Inward Map"

You use this when someone from the **outside** (Internet) wants to reach something **inside** your network.

* **Logic**: The "Destination" IP on the packet is originally the router's public IP; the router changes that destination to an internal IP (like `192.168.199.200`).
* **Common Name**: Port Forwarding.
* **Your Image Context**: You are mapping incoming traffic on `ether1-gateway` port `80` to an internal server.

### 2. Source NAT (SRC-NAT) = "The Outward Mask"

You use this when someone from the **inside** (LAN) wants to go **outside** (Internet).

* **Logic**: The "Source" IP on the packet is a private IP (e.g., `192.168.0.21`); the router changes that source to its own Public IP so the Internet knows where to send the reply.
* **Common Name**: Masquerade.
* **SysAdmin Tip**: Without this, your internal devices can talk to each other, but they will never get a response from Google or Netflix because private IPs are not "routable" on the public internet.

---




## Source NAT vs. Destination NAT

Understanding the flow of traffic is essential for configuring Network Address Translation.

### Destination NAT (DST-NAT)
* **Direction**: Outside → Inside.
* **Purpose**: Allows external users to access internal services (Web servers, Cameras).
* **Action**: Changes the **Destination IP** of the incoming packet to a local IP.
* **Example**: Mapping `Public_IP:80` to `192.168.199.200:80`.

### Source NAT (SRC-NAT)
* **Direction**: Inside → Outside.
* **Purpose**: Allows internal users to browse the internet using the router's public IP.
* **Action**: Changes the **Source IP** of the outgoing packet to the router's WAN IP.
* **Example**: Using `action=masquerade` on the out-interface.


### Summary Table for your Lab

| Feature | Destination NAT (DST-NAT) | Source NAT (SRC-NAT) |
| --- | --- | --- |
| **Typical Chain** | `dstnat` | `srcnat` |
| **Traffic Direction** | Inward (Incoming) | Outward (Outgoing) |
| **Common Use** | Hosting a Server | Providing Internet to Clients |
| **Key Action** | `dst-nat` | `masquerade` or `src-nat` |
