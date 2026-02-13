
## Optimization: Using Address Lists

Managing security for individual IP addresses is inefficient. 
System Administrators use **Address Lists** to group multiple IPs, ranges, or domains under a single name. This keeps the firewall organized and scalable.

### Why Use Address Lists?

* **Efficiency**: One firewall rule can protect against thousands of IPs stored in a list.
* **Readability**: Rules are easier to understand (e.g., `Source: Trusted_Admins` vs. `Source: 192.168.88.5`).
* **Dynamic Security**: You can set temporary "timeouts" to block attackers automatically for a specific duration.

### How to Implement in MikroTik

1. **Define the List**: Navigate to `IP > Firewall > Address Lists`. Create a list named `Malicious_IPs` and add the target addresses.
2. **Apply to Filter**: In your **Filter Rule**, instead of putting an IP in the *General* tab, go to the **Advanced** tab and select your list in the `Src. Address List` field.

---

### Static vs. Dynamic Lists

| Type | How it Works | Use Case |
| --- | --- | --- |
| **Static** | Manually entered by the admin. | Safe-listing your home IP or office subnet. |
| **Dynamic** | Added automatically by the router via a script or trigger. | **Brute Force Defense**: Automatically adding IPs that fail SSH login 3 times. |
| **DNS-Based** | You enter a domain (e.g., `google.com`); the router resolves the IPs. | Blocking or bypassing specific websites without tracking their IP changes. |

---

### SysAdmin Best Practices

A professional firewall configuration usually includes these standard lists:

* **`Admin_Access`**: Contains the IPs of the IT team. Only these IPs should have `ACCEPT` rules for Port 22 (SSH) and 8291 (WinBox).
* **`Blacklist`**: A list of IPs set to `DROP` globally.
* **`Bypass_Auth`**: Devices like printers or servers that don't need to go through a login portal.




