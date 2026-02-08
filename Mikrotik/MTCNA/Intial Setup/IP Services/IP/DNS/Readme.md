
# MikroTik RouterOS DNS Settings

### 1. **DNS (Domain Name System)**
   **DNS** is a service that translates domain names (e.g., `www.example.com`) into IP addresses (e.g., `192.168.1.1`). MikroTik RouterOS can act as a **DNS resolver** or a **DNS server** for the local network.

---

### 2. **Allow DNS Remote Requests**
   - **Definition**: This setting determines whether the MikroTik router will allow **remote clients** (devices outside your local network) to make DNS queries to the router.
   - **Default Setting**: By default, this option is **disabled** to prevent unauthorized access to your router’s DNS service.
   - **Use Case**: Enabling this option allows external clients to use your MikroTik router as their DNS server.

   **How to Enable/Disable "Allow DNS Remote Requests"**:
   - **WebFig/Winbox**: Go to `IP` > `DNS` and check/uncheck the box for **Allow Remote Requests**.
   - **Command Line**:
     ```bash
     /ip dns set allow-remote-requests=yes  # To enable
     /ip dns set allow-remote-requests=no   # To disable
     ```

   **Important**: Enabling this may expose your router to **DNS amplification attacks**. Use it carefully or restrict access to specific IPs.

---

### 3. **DNS Static Entries**
   - **Definition**: DNS Static Entries allow you to manually map domain names to specific IP addresses. These entries override the regular DNS resolution process.
   - **Use Case**: Useful for internal services, like `server.local` pointing to an internal IP (`192.168.1.100`).

   **How to Add DNS Static Entries**:
   - **WebFig/Winbox**: Go to `IP` > `DNS`, then select the **Static** tab and click **Add** to create a new entry.
     - **Name**: The domain name (e.g., `server.local`).
     - **Address**: The IP address to map the domain to (e.g., `192.168.1.100`).
   - **Command Line**:
     ```bash
     /ip dns static add name="server.local" address=192.168.1.100
     ```

---

### 4. **DNS Settings in MikroTik RouterOS**
   The following are the main DNS settings you can configure:

   - **Primary and Secondary DNS Servers**: The DNS servers your MikroTik router uses for resolving domain names. You can set public DNS servers (e.g., Google DNS, Cloudflare DNS) or internal DNS servers.
   - **DNS Cache**: MikroTik can cache DNS results for quicker response times on subsequent queries.
   - **DNS Timeout**: Sets the time the router waits for a DNS response before trying a different DNS server.

---

### 5. **Other Important DNS Features**
   - **DNS Forwarding**: Configure MikroTik to forward DNS requests to another DNS server when it can't resolve a domain.
   - **DNS Query Logging**: MikroTik can log DNS queries for debugging or monitoring purposes.

---

### Summary of Key DNS Features in MikroTik:
- **Allow DNS Remote Requests**: Allows remote clients to query the MikroTik DNS server.
- **DNS Static**: Creates custom mappings between domain names and IP addresses.
- **DNS Server Configuration**: Set up DNS servers, cache, and forwarding.
- **DNS Query Logging**: Enables logging of DNS requests for monitoring purposes.

---

### Example Use Case:
If you're setting up a small office network and want devices to access internal services via domain names (e.g., `mail.local` for the mail server), you would:
1. Enable **Allow DNS Remote Requests** (if needed).
2. Add a **static DNS entry** for `mail.local` pointing to `192.168.1.50`.
3. Ensure that the router is set to forward DNS queries or use its own DNS servers for public domain names.


<img width="720" height="590" alt="image" src="https://github.com/user-attachments/assets/fb6bd5a1-2e92-407c-8506-eb143c24dc4c" />

<img width="1559" height="830" alt="image" src="https://github.com/user-attachments/assets/37ccca65-0987-4d9b-a917-19cb1c95462d" />

