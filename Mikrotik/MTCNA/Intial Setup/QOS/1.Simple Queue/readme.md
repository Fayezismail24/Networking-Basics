In MikroTik’s WinBox, a **Simple Queue** is used to manage bandwidth for specific users or devices , subnet  The configuration in the image below  image shows a hard speed limit applied to a single IP address.

---

### 🚦 Queue Configuration Breakdown

<img width="766" height="428" alt="image" src="https://github.com/user-attachments/assets/115f5512-6a80-447e-9d6b-091477ae658d" />

* **Name (`3M Limit`):** A custom label used to identify this specific rule in the queue list.
* **Target (`192.168.0.55`):** The specific device on the network that this rule applies to. Any traffic coming from or going to this IP will be throttled.
* **Max Limit (Upload/Download):**
* **Target Upload (`3M`):** Restricts the device from sending data faster than **3 Megabits per second (Mbps)**.
* **Target Download (`3M`):** Restricts the device from receiving data faster than **3 Megabits per second (Mbps)**.



---

### 🔍 How It Works with Connections

Since we previously discussed **Connection States**, it's important to know how they interact with this queue:

1. When a **New** connection is opened by `192.168.0.55`, the router identifies it.
2. As the connection becomes **Established**, the router continuously measures the data rate.
3. If the speed exceeds 3 Mbps, the router "drops" or delays packets to keep the user within the limit.

---

### ⚠️ Note on Performance

> [!TIP]
> **Simple Queues** are processed in order from top to bottom. If you have many users, ensure your most important rules (or those with specific IPs) are at the top of the list to ensure they are applied correctly.
