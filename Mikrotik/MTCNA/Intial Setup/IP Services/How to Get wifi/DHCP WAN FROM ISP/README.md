```md
## MikroTik WAN Setup as a DHCP Client

Configuring your MikroTik WAN (Wide Area Network) interface as a **DHCP Client** is the most common and simplest way to connect your router to the internet.

In practical terms, this allows your MikroTik to automatically request network details from your Internet Service Provider (ISP). Below is a clear explanation of why this method is used and what happens in the background.

---

### 1. Automatic IP Address Assignment

Most home and small business ISPs do not provide a fixed IP address. Instead, they assign IPs dynamically from a shared pool. When DHCP Client is enabled, your MikroTik automatically receives:

- **Public IP Address**  
  The router’s address on the internet.

- **Subnet Mask**  
  Defines the size and boundaries of the assigned network.

---

### 2. Default Gateway Learning

Having an IP address alone is not enough. The router also needs to know where to send traffic destined for the internet.

The DHCP Client automatically learns the ISP gateway address and creates a **default route (0.0.0.0/0)**. This tells the router that any traffic not meant for the local network should be forwarded to that gateway.

---

### 3. DNS Server Configuration

To access websites using domain names like `google.com`, DNS servers are required to translate names into IP addresses.

The DHCP Client can automatically obtain the ISP’s **DNS server addresses**, removing the need for manual configuration.

---

### 4. Plug-and-Play Reliability

If the ISP changes its gateway, DNS servers, or internal network settings, the DHCP Client adapts automatically.

With a static configuration, any such change would break connectivity until you manually update the settings.

---

### When should you avoid using a DHCP Client?

You typically would not use DHCP Client if:

- Your ISP provides a **Static IP address**
- Your connection uses **PPPoE** with a username and password
- The MikroTik is acting only as a **switch or access point**, not as an internet gateway


INTERNET
          |
          | (Public IP assigned by ISP via DHCP)
          v
+-----------------------+
|    MikroTik Router    |
|                       |
|  [ WAN Interface ]    | <--- DHCP Client lives here
|          |            |
|      [ NAT ]          | <--- Translates Public IP to Local IP
|          |            |
|  [ LAN Interface ]    | <--- Often a "Bridge" of ports
+-----------------------+
          |
          | (Private IPs: 192.168.1.x)
          v
   +------+------+
   |      |      |
  [PC]  [Phone] [TV]




