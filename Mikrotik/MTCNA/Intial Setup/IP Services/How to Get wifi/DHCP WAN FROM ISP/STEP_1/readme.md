```md
## Configure WAN as DHCP Client (MTCNA Basics)

This is one of the **first and most important steps** when preparing a MikroTik router to connect to the internet.  
In this step, you will configure the WAN interface to automatically receive network settings from the ISP.

---

### Step 1: Open the DHCP Client Menu

From **WinBox**:

1. Navigate to:  
   **IP → DHCP Client**

This section is used to configure interfaces that should **automatically obtain an IP address, gateway, and DNS** from an upstream network such as an ISP modem.

---

### Step 2: Add a New DHCP Client

1. Click **Add (+)**  
2. In the **Interface** field, select the interface connected to your ISP  
   - Common examples: `ether1`, `wan`, or `uplink`
3. Leave the default options enabled:
   - ✔ Add Default Route  
   - ✔ Use Peer DNS  
   - ✔ Use Peer NTP
4. Click **OK**

---

### Step 3: Verify the DHCP Client Status

After clicking **OK**, the status should change to **bound**, which confirms that the router successfully received network information from the ISP.

You can now see:
- A dynamically assigned **IP address**
- A **default gateway (0.0.0.0/0)**
- **DNS servers** provided by the ISP

---

### Result

At this point:
- The WAN interface is online
- The router knows how to reach the internet
- The MikroTik is ready for NAT and firewall configuration

This setup follows the **standard MTCNA workflow** for initial internet connectivity.
```

