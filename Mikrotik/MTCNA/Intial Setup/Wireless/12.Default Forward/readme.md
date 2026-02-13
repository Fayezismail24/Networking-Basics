In MikroTik’s wireless settings, **Default Forward** is the "sibling" setting to Default Authenticate. While Authentication controls if a device can connect to the AP, **Forward** controls whether those connected devices can talk to *each other*.

If you look at the original table you uploaded, the logic for "Default Forward" works exactly the same way, but it governs **Client-to-Client communication** rather than **Client-to-AP access**.

---

## 1. Default Forward: ON (The Standard Way)

By default, this setting is **Checked ()**.

* **Behavior:** Every device connected to the same Wi-Fi interface (WLAN1) can see and communicate with every other device on that same interface.
* **Use Case:** Home or office environments where you need to print to a wireless printer, cast to a Chromecast, or share files between laptops.

## 2. Default Forward: OFF (The Guest Way)

When you **Uncheck ()** this setting, you are enabling **Client Isolation**.

* **Behavior:** Devices can talk to the Router (and the Internet), but they are invisible to one another.
* **Use Case:** Public Hotspots, Guest Wi-Fi, or Hotels. It prevents a malicious user from scanning other guests' devices for vulnerabilities.

---

### The Logic Table for Forwarding

Just like Authentication, the **Access List** can override the global "Default Forward" setting for specific devices.

| Default Forward (Global) | Access List "Forward" | Result |
| --- | --- | --- |
| **Checked ()** | ** (Yes)** | Device can talk to everyone. |
| **Checked ()** | ** (No)** | This specific device is isolated (cannot talk to others). |
| **Unchecked ()** | ** (Yes)** | This device is an "exception" and can talk to others. |
| **Unchecked ()** | ** (No)** | Device is isolated. |

---

### Why use "Default Forward = OFF"?

1. **Security:** It stops "Lateral Movement." If one guest's phone has malware, it cannot spread to other phones on the same Wi-Fi because the AP drops those packets.
2. **Bandwidth Efficiency:** In very large outdoor wireless deployments, disabling forwarding prevents unnecessary "broadcast" traffic from eating up airtime across the entire network.
3. **Privacy:** You don't want a random guest in your coffee shop accidentally seeing your "Office-Printer" or "Admin-Laptop" in their "Network Discovery" folder.

### Important Note on Multi-VLANs

"Default Forward" only controls traffic within the **same wireless interface**. If you have two different SSIDs (like `Private_WiFi` and `Guest_WiFi`) on different VLANs, the traffic between them is handled by the **IP Firewall**, not this wireless setting.

<img width="901" height="774" alt="image" src="https://github.com/user-attachments/assets/3c97a4a1-48ed-4309-82f6-2dcb91c8ce3b" />
