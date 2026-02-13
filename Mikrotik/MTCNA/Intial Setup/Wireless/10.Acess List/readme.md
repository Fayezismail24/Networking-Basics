In MikroTik RouterOS, the **Access List** is the counterpart to the Connect List.

While the Connect List is for the client to which AP they can connect to , the **Access List is for the Access Point (AP)** to control which clients are allowed to connect.

---

### Core Functions of the Access List

The Access List acts as a "Gatekeeper" for your wireless network. It allows you to create specific rules for individual client devices based on their MAC addresses.

* **Authentication Control**: You can explicitly allow or deny specific devices from connecting to your AP.
* **Signal Strength Limits**: You can set a minimum and maximum signal range for clients. If a client's signal is too weak (e.g., below -80 dBm), the AP will reject or drop them to maintain overall network performance.
* **Time-Based Access**: You can configure rules to allow a device to connect only during specific times of the day.
* **Private Passkeys**: You can assign a unique security key to a specific MAC address, even if the rest of the network uses a different password.

---

### Key Configuration Fields

| Field | Description |
| --- | --- |
| **MAC Address** | The unique hardware ID of the client device (e.g., a phone or laptop). |
| **Interface** | Which wireless card (`wlan1`, `wlan2`) the rule applies to. |
| **Signal Strength Range** | The range (e.g., `-75..120`) a client must stay within to remain connected. |
| **Authentication** | A checkbox that determines if the device is allowed (`checked`) or blocked (`unchecked`). |
| **Forwarding** | Determines if the client is allowed to communicate with other wireless clients on the same AP. |

---

### Access List vs. Connect List

> **The Golden Rule**: The **Access List** is used by the Host (AP) to manage guests, whereas the **Connect List** is used by the Guest (Station) to choose a host.

* **Access List**: "I am the AP. I will only let Phone A join if its signal is stronger than -70 dBm."
* **Connect List**: "I am the Station. I will only connect to Router B if it is available."

---

### The "Default Authenticate" Setting

In your Wireless Interface settings, there is a checkbox called **Default Authenticate**.

* **If Checked**: Any client with the correct password can connect, unless they are specifically blocked in the Access List.
* **If Unchecked**: **Only** devices explicitly listed in your Access List can connect. This is a very high-security configuration.


<img width="756" height="550" alt="image" src="https://github.com/user-attachments/assets/dc149214-7263-4d36-af11-e78ef1ebab31" />



| Field                     | Description                                                                                    |
| ------------------------- | ---------------------------------------------------------------------------------------------- |
| **MAC Address**           | The unique hardware ID of the client device (e.g., a phone or laptop).                         |
| **Interface**             | Which wireless card (`wlan1`, `wlan2`) the rule applies to.                                    |
| **Signal Strength Range** | The range (e.g., `-75..120`) a client must stay within to remain connected.                    |
| **Authentication**        | A checkbox that determines if the device is allowed (`checked`) or blocked (`unchecked`).      |
| **Forwarding**            | Determines if the client is allowed to communicate with other wireless clients on the same AP. |
| **Client Tx Limit**       | Limits the maximum transmission power (Tx) for client devices.                                 |
| **AP Tx Limit**           | Limits the maximum transmission power (Tx) for the AP.                                         |

Here is the formatted Markdown version for your GitHub repository or documentation. This structure aligns with the **MikroTik RouterOS** firewall and access rule logic often found in MTCNA training.

---

## 🕒 Time Configuration for Access Rules

In MikroTik RouterOS, you can restrict access based on specific schedules using the **Time** attributes within a rule. This is commonly used for parental controls, office hours, or scheduled maintenance.

### 1. Time Field

* **Time:** Specifies the exact **start time** for the access rule to become active.
* *Format:* `HH:MM:SS`
* *Example:* `00:00:00` (Midnight) or `09:00:00` (9:00 AM).


* **Duration:** Defines how long the rule remains active once the start time is reached.
* *Format:* `Dd HH:MM:SS`
* *Example:* `1d 00:00:00` means the rule stays active for a full 24-hour cycle.



### 2. Days Selection

Directly below the time fields, you can toggle specific days of the week to apply the rule.

| Weekday | Description |
| --- | --- |
| **Mon - Fri** | Standard work week scheduling. |
| **Sat - Sun** | Weekend-only restrictions or special access. |

---

### 💡 Example: Work Hours Only Access

To create a rule that only allows internet access during a standard Monday to Friday work week (9:00 AM to 5:00 PM), you would configure the parameters as follows:

* **Time:** `09:00:00`
* **Duration:** `08:00:00`
* **Days:** Checked: `mon, tue, wed, thu, fri` | Unchecked: `sat, sun`

> **Note:** If a rule's time parameters are not met, the router will ignore that specific rule and move to the next one in the list.




In MikroTik RouterOS (and networking in general), the **"Next Rule"** logic is the most important concept to master for the MTCNA. It refers to the **Top-to-Bottom processing** of a list.

Here is the breakdown of that last line for your documentation:

---

### 🚦 Understanding "Top-to-Bottom" Logic

When a packet of data enters the router, it doesn't look at all your rules at once. Instead, it starts at **Rule #0** and works its way down.

#### 1. The Match Phase

For every rule in the list, the router asks: *"Does this packet match the conditions (IP, Port, Protocol, and **Time**)?"*

* If the current time is **Saturday** and your rule is set for **Mon-Fri**, the router says **"No Match."**

#### 2. The "Ignore" Action

If the rule doesn't match (because of the time restriction), the router simply **ignores** that rule. It doesn't stop or block the packet yet; it just moves to the next rule in the sequence.

#### 3. The Fallthrough

The packet "falls through" to the next line. If you have no other rules, the packet will eventually hit the **Default Action** (which is usually to "Accept" in the Forward chain unless you’ve created a "Drop All" rule at the very bottom).

---

### 📝 Example Scenario: "The Homework Filter"

Imagine you have these three rules in order:

1. **Rule 0 (Drop):** Block YouTube | **Time:** 08:00–15:00 | **Days:** Mon–Fri
2. **Rule 1 (Accept):** Allow All Traffic

**If it is Monday at 10:00 AM:**

* The packet hits Rule 0. It matches the time and day.
* **Result:** The packet is **Dropped**. The router stops looking at any more rules.

**If it is Saturday at 10:00 AM:**

* The packet hits Rule 0. It **does NOT match** the days.
* **Result:** The router **ignores** Rule 0 and moves to Rule 1.
* Rule 1 matches everything.
* **Result:** The packet is **Accepted**.

---

### ⚠️ Common MTCNA Mistake

Students often forget that if they want to block something during a specific time, they **must** have a rule below it that allows traffic during other times, or they must understand the "Default Policy."

> **Rule of Thumb:** If a rule is "Time Sensitive," it is only "Alive" during those hours. When those hours end, that rule effectively disappears from the list until the next day.

**Would you like me to show you how to use the "Extra" tab in WinBox to see exactly when a rule is active or inactive?**




In MikroTik RouterOS, managing access based on the day of the week is a classic **MTCNA** lab scenario. To achieve the "Allow Mon-Fri / Block Sat-Sun" logic, you have two primary ways to configure the firewall.

---

## Method 1: The "Simple Block" (Recommended)

In this method, you assume that traffic is generally allowed, but you want to create a specific "wall" for the weekend.

### Rule Logic:

* **Action:** `drop`
* **Days:** `sat`, `sun`
* **Time:** `00:00:00` - `23:59:59` (All day)

**How it works:** On Monday through Friday, this rule is **inactive**. Packets will "fall through" this rule and hit the default accept policy. On Saturday morning at 00:00:00, the rule "wakes up" and starts dropping all packets that hit it until Sunday night.

---

## Method 2: The "Strict White-list" (Two Rules)

This is used if your router is set to a "Drop everything by default" policy. This is more secure but requires more configuration.

### Rule A: The Permission

* **Action:** `accept`
* **Days:** `mon`, `tue`, `wed`, `thu`, `fri`
* **Purpose:** This opens a "gate" specifically for workdays.

### Rule B: The Cleanup (The Hammer)

* **Action:** `drop`
* **Days:** (Leave all boxes unchecked—this means "all days")
* **Purpose:** This catches any packet that didn't match Rule A (meaning packets from Saturday and Sunday).

---

## 🛠️ Configuration via Terminal (CLI)

For your GitHub documentation, here are the commands to implement **Method 1**:

```bash
# Create a rule that blocks traffic only on weekends
/ip firewall filter
add action=drop chain=forward comment="Block Weekend Access" \
    days=sat,sun time=0s-1d protocol=tcp

```

---

## ⚠️ Important MTCNA Concept: "Packet Matching"

Remember the **Last Line** logic we discussed:

* **On Friday:** The packet looks at the "Weekend Block" rule. The router says: *"The day is Friday, but this rule is for Sat/Sun. NO MATCH."* The packet moves to the next rule and is allowed.
* **On Saturday:** The packet looks at the rule. The router says: *"The day is Saturday. This rule is for Sat/Sun. MATCH!"* The packet is immediately **Dropped**.

> **Pro Tip:** Always check your **System Clock** (`/system clock print`). If your router's date is set incorrectly (e.g., it thinks today is 1970), your time-based rules will block the wrong days!

**Would you like me to show you how to synchronize your router's clock using NTP so these rules always run on time?**
