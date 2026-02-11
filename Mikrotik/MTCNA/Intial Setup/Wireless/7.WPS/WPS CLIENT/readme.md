In MikroTik’s RouterOS, **WPS Client** is the mode used when your MikroTik device acts as a **Station** (a client) trying to connect to another Access Point. Instead of you manually typing in a long Wi-Fi password, the MikroTik "requests" the security credentials from the AP automatically.

---

### How WPS Client Works

* **Purpose:** It allows for convenient access to a Wi-Fi network without the need for entering a passphrase manually.
* **Role-Based:** This mode is specifically for **Station** modes.
* **Mechanism:** When you trigger WPS Client mode, the MikroTik scans for an Access Point that is currently in "WPS Pairing" mode. Once found, they exchange security keys securely.

---

### Methods of Using WPS Client

1. **Push Button Configuration (PBC):**
* You press the physical WPS button on your ISP's router (the AP).
* You then trigger the `wps-client` command on your MikroTik.
* The two devices "shake hands" and your MikroTik is automatically configured with the correct SSID and password.


2. **PIN Method:**
* The MikroTik generates a PIN or you use the PIN provided by the AP to authenticate the connection.



---

### Why Use WPS Client on a MikroTik?

* **Connecting to ISP Routers:** If you are using a MikroTik to extend a home network and you don't know (or don't want to type) the complex password on the bottom of the ISP router.
* **Temporary Setups:** Great for quickly bridging two devices without deep-diving into the Wireless Tables or Security Profiles.

---

### Comparison: WPS Client vs. WPS Accept

| Feature | **WPS Client** | **WPS Accept** |
| --- | --- | --- |
| **MikroTik's Role** | The **Station** (Guest). | The **Access Point** (Host). |
| **The Action** | Requests the password from an AP. | Gives the password to a joining device. |
| **Typical Goal** | Joining an existing Wi-Fi network. | Letting a new device join your network. |

---

### ⚠️ A Note on Persistence

When you use **WPS Client**, the MikroTik will automatically create or update a **Security Profile** with the password it receives. Even if you turn off WPS later, the device will remember that password to stay connected.

