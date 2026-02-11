
## The MikroTik Connect List

The **Connect List** is a set of rules used by a MikroTik device when it is operating in **Station** (client) mode. 

It tells the device exactly which Access Points (APs) it is allowed to connect to, which ones to prefer, and how strong the signal must be to stay connected.

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



<img width="1185" height="453" alt="image" src="https://github.com/user-attachments/assets/3abec09e-77b9-4247-846a-60bb54288e15" />

### Real-World Example: Signal Thresholds

As you mentioned, the **Signal Range** is the most powerful tool for managing roaming. Here is how that looks in practice:

> **Rule Setup:** Set the Signal Range to `-70..120`

#### Behavior:

* **The Connection:** The device will maintain a stable connection as long as the signal strength is **-70 dBm** or better (e.g., -60 dBm, -50 dBm).
* **The Threshold:** If the signal drops to **-71 dBm**, the MikroTik will automatically disconnect. It doesn't just wait to lose the signal entirely; it proactively cuts the link.
* **The Hunt:** Once disconnected, it immediately searches for another Access Point in your Connect List that meets the required criteria.

#### Why this matters:

This prevents the **"Sticky Client"** problem. Without this rule, a device might stay "stuck" to a distant Access Point with a terrible, slow connection even if you are standing right next to a much better one.


---

### The Sequential Logic Flow

When your wireless interface is looking for a connection, it acts like a person checking off a "To-Do" list in order:

1. **Start at Rule 0:** The router checks the first entry. If an Access Point (AP) is found that matches the SSID, MAC, and signal strength (e.g., your `-70..120` range), it connects immediately.
2. **Move to Rule 1:** If Rule 0 cannot be satisfied (e.g., the AP is turned off or the signal is too weak at -75 dBm), the router ignores it and moves to Rule 1.
3. **Continue Down:** It will continue through Rule 2, 3, etc., until a match is found.
4. **The "End of List" Scenario:** If it hits the end of the list and nothing matches:
* If **Default Authenticate** is checked in your Wireless Interface settings, it will try to connect to *any* available AP that matches your SSID.
* If **Default Authenticate** is unchecked, the router will simply not connect to anything.



---

### Why this Order Matters

This top-down approach is perfect for **Failover/Backup** scenarios:

* **Rule 0 (Primary):** Your high-speed 5GHz backbone link.
* **Rule 1 (Secondary):** A slower 2.4GHz backup link or a different AP.

By putting the preferred connection at the top (Rule 0), you ensure the MikroTik always tries the "best" option first before settling for the backup.

---

### Pro-Tip for your `-70..120` Rule

Since you have two identical rules in your image (both for `wlan1` with the same signal range), the router will always try to satisfy **Rule 0** first. If Rule 0 and Rule 1 point to the same SSID, Rule 1 acts as a redundant check.

> **Important:** If you want Rule 1 to be a "fallback" with a weaker signal, you might set Rule 0 to `-70..120` and Rule 1 to `-85..120`. This tells the router: "Try for a great signal first; if you can't find one, I'll accept a weaker one."




