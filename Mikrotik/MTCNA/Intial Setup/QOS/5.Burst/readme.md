
## 🚀 Understanding Burst in Simple Queues

**Burst** is a feature that allows a user to temporarily exceed their `Max Limit` speed for a short duration. It is designed to make web browsing feel faster by providing high speed for initial page loads while restricting long-term downloads to a standard limit.

---

### ⚙️ Core Burst Parameters

| Parameter | Description |
| --- | --- |
| **Burst Limit** | The "peak" speed a user can reach during the burst period (higher than `Max Limit`). |
| **Burst Threshold** | The "on/off switch." If the average speed is below this value, the burst is allowed. |
| **Burst Time** | The window of time used to calculate the user's average speed. |
| **Max Limit** | The standard speed limit the user returns to once the burst is finished. |

<img width="577" height="123" alt="image" src="https://github.com/user-attachments/assets/585c76d2-6812-4ec2-a1ff-8fd1b53200f8" />


---

### 🔄 How the Logic Works

The router manages bursts by calculating a **Rolling Average** of the user's data usage over the specified `Burst Time`:

1. **Triggering the Burst**: If the user's average speed is **below** the `Burst Threshold`, they are granted the higher `Burst Limit`.
2. **Monitoring Usage**: Every second, the router recalculates the average speed based on the history stored during the `Burst Time`.
3. **Ending the Burst**: Once the average speed rises **above** the `Burst Threshold`, the burst stops.
4. **Enforcing the Limit**: The router then throttles the user down to the `Max Limit`.
5. **Recovery**: To "recharge" the burst, the user must stay below the threshold until their rolling average drops again.

---

### 💡 Why Use Burst?

* **Improved User Experience**: Webpages load almost instantly because they are small enough to fit within the burst window.
* **Fairness**: Heavy downloaders (like those using torrents or large file transfers) are quickly moved to their `Max Limit`, preventing them from hogging the entire pipe.

> [!TIP]
> You can verify if a user is currently "Bursting" by looking at the **Queue Color**. If the queue is green but the speed is higher than the `Max Limit`, the burst is active. If the queue stays **Red**, the user has likely exhausted their burst and is being limited.

<img width="1159" height="765" alt="image" src="https://github.com/user-attachments/assets/44b7e9d0-16a3-4d77-a516-dec3cbdb9f1d" />


 ## 🚀 Burst: Temporary Speed Increases

The **Burst** feature allows a user to temporarily exceed their **Max Limit**. This is ideal for web browsing where quick "bursts" of speed are needed to load pages fast.

---

### **Burst Parameters**

* **Burst Limit**: The maximum speed the user can reach during the burst (e.g., **4M**).
* **Burst Threshold**: The average speed value that determines when the burst should stop. If the user's average speed exceeds this (e.g., **2M**), the burst ends.
* **Burst Time**: The time period in seconds used to calculate the rolling average speed.

---

### **How it looks in WinBox**

The configuration is found under the **Burst** section of a **Simple Queue**:

* **Target**: The specific IP being limited (e.g., `192.168.199.200`).
* **Max Limit**: The standard speed limit (e.g., `256k` upload / `512k` download) that applies once the burst is over.
* **Burst settings**: These are mapped to specific upload and download columns to give you precise control.
