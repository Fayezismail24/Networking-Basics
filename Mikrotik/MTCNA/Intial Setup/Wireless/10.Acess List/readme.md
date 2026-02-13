
# 📖 The MikroTik MTCNA Handbook: Wireless & Firewall


---

<a id="ch1"></a>

## 📘 Chapter 1: The Wireless Access List

In MikroTik RouterOS, the **Access List** is the counterpart to the Connect List. While the Connect List is for the client to choose which AP they connect to, the **Access List is for the Access Point (AP)** to control which clients are allowed to connect.

<a id="ch1-1"></a>

### 1.1 Core Functions

The Access List acts as a "Gatekeeper" for your wireless network.

* **Authentication Control**: Explicitly allow or deny specific devices.
* **Signal Strength Limits**: Set a range (e.g., `-75..120`). If a client's signal is too weak (below -80 dBm), the AP will drop them to save airtime.
* **Private Passkeys**: Assign unique security keys to specific MAC addresses.

<a id="ch1-2"></a>

### 1.2 Key Configuration Fields

| Field | Description |
| --- | --- |
| **MAC Address** | Unique hardware ID of the client device. |
| **Interface** | Which wireless card (`wlan1`) the rule applies to. |
| **Authentication** | Checked = Allowed; Unchecked = Blocked. |
| **Forwarding** | If unchecked, clients cannot talk to each other (Client Isolation). |

<a id="ch1-3"></a>

### 1.3 Access List vs. Connect List

> **The Golden Rule**: The **Access List** is used by the Host (AP) to manage guests, whereas the **Connect List** is used by the Guest (Station) to choose a host.

<a id="ch1-4"></a>

### 1.4 The "Default Authenticate" Setting

Located in the Wireless Interface settings:

* **Checked**: Anyone with the password can join (unless blacklisted in the Access List).
* **Unchecked**: **Only** devices in the Access List can join (Whitelist mode).

---

<a id="ch2"></a>

## 📘 Chapter 2: Time-Based Access Control

<a id="ch2-1"></a>

### 2.1 The Time & Duration Fields

* **Time**: Start time for the rule (e.g., `09:00:00`).
* **Duration**: How long the rule stays active (e.g., `08:00:00`).

<a id="ch2-2"></a>

### 2.2 Days of the Week Selection

Toggle specific days (Mon–Sun). If a packet arrives on a day not selected, the rule is ignored.

<a id="ch2-3"></a>

### 2.3 Case Study: Work Hours Only

* **Goal**: Allow access Mon–Fri, 9 AM to 5 PM.
* **Config**: Time=`09:00:00`, Duration=`08:00:00`, Days=`mon-fri`.

---

<a id="ch3"></a>

## 📘 Chapter 3: Firewall Logic & Flow

<a id="ch3-1"></a>

### 3.1 Top-to-Bottom Processing

The router reads rules starting at **Index 0**. Once a packet matches a rule, the router performs the action and stops looking further.

<a id="ch3-2"></a>

### 3.2 The Match & Ignore Cycle

If a packet doesn't match a rule's criteria (like the wrong Time or Day), the router **ignores** that rule and moves to the next.

<a id="ch3-3"></a>

### 3.3 Example: The Homework Filter

1. **Rule 0 (Drop)**: Block YouTube | Time: 08:00–15:00 | Days: Mon–Fri
2. **Rule 1 (Accept)**: Allow All Traffic

* *Monday at 10 AM:* Matches Rule 0 → **Dropped**.
* *Saturday at 10 AM:* Fails Rule 0 → Moves to Rule 1 → **Accepted**.

---

<a id="ch4"></a>

## 📘 Chapter 4: Implementation Strategies

<a id="ch4-1"></a>

### 4.1 Weekend Blocking (Simple vs. Strict)

* **Simple Block**: One rule to `drop` traffic on `sat, sun`.
* **Strict White-list**: One rule to `accept` on `mon-fri`, followed by a second rule to `drop` everything else.

<a id="ch4-2"></a>

### 4.2 Terminal/CLI Configuration

```bash
/ip firewall filter
add action=drop chain=forward days=sat,sun time=0s-1d comment="Weekend Block"

```

<a id="ch4-3"></a>

### 4.3 The Importance of the System Clock

Always verify your time settings with `/system clock print`. If the router thinks it is 1970, your Tuesday might be treated as a Sunday!

---

