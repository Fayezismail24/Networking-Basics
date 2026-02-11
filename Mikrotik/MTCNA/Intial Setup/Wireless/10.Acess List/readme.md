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


