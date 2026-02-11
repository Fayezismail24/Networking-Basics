## WPS Accept in MikroTik

In MikroTik's RouterOS, **WPS Accept** is a feature used when the device is acting as an **Access Point (AP)**. It is designed to allow new wireless clients to connect to your network quickly and conveniently without the need to manually enter a complex passphrase.

### How WPS Accept Works

* **Convenience:** It simplifies the onboarding process for guest devices or peripherals (like printers) by bypassing manual password entry.
* **Role-Based:** This specific mode is used for the **AP side** of a connection.
* **Triggering:** When activated, the MikroTik AP enters a "listening" state for a short period, during which a client device can pair with it.

---

### Methods of WPS Accept

There are two primary ways to use WPS Accept within RouterOS:

1. **Virtual Push Button (PBC):**
* You trigger the `wps-push-button` command or click the button in WinBox.
* The AP will accept connections from any client that also has its WPS button pressed within the timeout window.


2. **PIN Method:**
* The client provides a specific PIN, which is then entered into the MikroTik's WPS menu to authorize the connection.



---

### Comparison: WPS Accept vs. WPS Client

| Feature | **WPS Accept** | **WPS Client** |
| --- | --- | --- |
| **Device Role** | The MikroTik is the **Access Point**. | The MikroTik is the **Station** (Client). |
| **Action** | It "Accepts" a new device into the network. | It "Requests" to join another router's network. |
| **Typical Use** | Letting a phone or printer join your Wi-Fi. | Connecting a MikroTik bridge to a home ISP router. |

---

> ### ⚠️ Security Note
> 
> 
> While WPS Accept is convenient, it can be a security risk. PIN-based WPS is susceptible to "brute-force" attacks. It is generally recommended to use the **Push Button (PBC)** method only when needed and keep WPS disabled otherwise to protect your network.

