##  Destination NAT (Port Forwarding)

While Filter Rules handle security, **NAT (Network Address Translation)** rules handle how traffic is directed to services inside the network. This configuration allows an internal server to be accessible from the internet.

### Configuration Breakdown
<img width="840" height="771" alt="image" src="https://github.com/user-attachments/assets/5895cca5-1ff7-48c6-9aa3-9f6ae2bab7c9" />


* **Chain**: `dstnat` — This chain is used for packets arriving at the router that need their destination address changed.
* **In. Interface**: `ether1-gateway` — The rule only triggers for traffic entering through the WAN/Public internet interface.
* **Protocol & Port**: `6 (tcp)` on **Port 80** — The router listens for standard HTTP web requests.
* **Action**: `dst-nat` — The router "translates" the destination IP.
* **To Addresses**: `192.168.199.200` — The private IP of the internal server where the traffic is sent.
* **To Ports**: `80` — The traffic is delivered to the server on the same port.

### Practical Application
If a user on the internet tries to access the router's Public IP on a web browser, the router automatically forwards that request to the internal server at `192.168.199.200`. This is the standard way to host web servers, mail servers, or game servers behind a firewall.
