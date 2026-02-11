
## The MikroTik Connect List

The **Connect List** is a set of rules used by a MikroTik device when it is operating in **Station** (client) mode. It tells the device exactly which Access Points (APs) it is allowed to connect to, which ones to prefer, and how strong the signal must be to stay connected.

### Key Configuration Fields

| Field | Description |
| --- | --- |
| **Interface** | The physical wireless card this rule applies to (e.g., `wlan1`). |
| **MAC Address** | The specific BSSID of the AP. If left blank, it matches any AP with the correct SSID. |
| **Connect SSID** | The name of the Wi-Fi network you want to join. |
| **Signal Range** | The "Sweet Spot." Example: `-70..120`. If the signal is worse than -70, the device won't connect (or will drop). |
| **Security Profile** | Which password/encryption profile to use for this specific AP. |

---

### Why Use a Connect List?

1. **Strict Roaming Control:** In a warehouse or large office, you can prevent a device from "sticking" to a weak AP far away by setting a `Signal Range`. Once the signal drops below your threshold, the MikroTik will automatically look for a stronger AP in the list.
2. **Redundancy (Failover):** You can list a "Primary" AP at the top and a "Backup" AP below it. If the first one fails, the device immediately moves to the second entry.
3. **Security Pinning:** By specifying the **MAC Address** of your AP, you ensure your device won't connect to a "rogue" or fake router that happens to have the same Wi-Fi name.

---

### Connect List vs. Access List

> **The Golden Rule:** The **Connect List** is for the guest (Client), while the **Access List** is for the host (AP).

* **Connect List:** "Which house am I allowed to visit?"
* **Access List:** "Which guests am I letting into my house?"

---

### Simple Logic Flow

When a MikroTik wireless interface starts up, it follows this logic:

1. **Check the Connect List:** It looks at the first entry (top of the list).
2. **Verify Criteria:** Does the AP's SSID match? Is the MAC address correct? Is the signal strength within the defined range?
3. **Attempt Connection:** If all criteria are met, it connects.
4. **Fallback:** If the first entry doesn't match or the signal is too weak, it moves to the second entry, and so on.
5. **Default:** If nothing in the list matches, it will only connect to an AP if **"Default Authenticate"** is checked in the Wireless Interface settings.

---

**Would you like me to generate the Terminal commands (`/interface wireless connect-list`) so you can copy-paste a specific rule into your router?**
