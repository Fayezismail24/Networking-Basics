# MikroTik User Group Policies

This directory contains the documentation and permission mapping for MikroTik RouterOS user groups. These policies define the access levels for all administrative accounts managed within this repository.

---

## 🛠 Access Method Policies
These permissions determine **how** a user is allowed to connect to the router interface.

| Policy | Description |
| :--- | :--- |
| **local** | Allows access via the physical console (RS232/Serial) or local keyboard. |
| **telnet** | Allows remote access via the Telnet protocol (Unencrypted). |
| **ssh** | Allows remote access via Secure Shell (Encrypted). |
| **ftp** | Grants permission to upload/download files (backups, firmware) via FTP. |
| **winbox** | Enables access via the WinBox GUI desktop application. |
| **web** | Enables access via the WebFig browser interface. |
| **api / rest-api** | Allows automated scripts or external software to interact with the router. |
| **romon** | Allows connecting through the Router Management Overlay Network (RoMON). |

---

## ⚙️ Functional Permissions
These permissions determine **what** a user can actually do once they are logged in.

### System Management
* **reboot**: Permission to restart the hardware.
* **policy**: Permission to manage user accounts and edit these very policy checkboxes. (High Risk)
* **password**: Allows the user to change their own login password.
* **sensitive**: Allows viewing of "hide-sensitive" data (e.g., VPN secrets, RADIUS keys, and wireless passwords).

### Configuration & Maintenance
* **read**: Permission to view all configuration settings (Read-Only).
* **write**: Permission to modify, create, or delete configuration settings.
* **test**: Allows usage of diagnostic tools like `ping`, `traceroute`, and `bandwidth-test`.
* **sniff**: Grants access to the Packet Sniffer tool for capturing network traffic.



