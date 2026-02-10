
## 🔒 MikroTik Wireless Security Profile

**Security Profile** = a **set of security settings** applied to a wireless interface or AP.  

- Controls **how clients authenticate and encrypt traffic**.
- You can create **multiple profiles** and assign them to different SSIDs or radios.
- Allows separation of security policies per SSID or radio.

---

## ⚙️ Key Settings in Security Profile

| Setting | Description |
|---------|------------|
| **Authentication Types** | WPA, WPA2, WPA3, or none |
| **Unicast Cipher** | Encryption for **data to a single client** (AES, TKIP) |
| **Group Cipher** | Encryption for **broadcast/multicast traffic** (AES, TKIP) |
| **Management Protection** | Protects AP management frames (optional) |
| **WPA Pre-Shared Key** | Password for WPA/WPA2 personal mode |
| **Radius** | Used for WPA Enterprise (802.1X) authentication |
| **Forwarding** | Option to allow or block client-to-client traffic |
| **Mode** | WPA or WPA2 only or both |

---

## 🔑 How It Works

1. Create a **Security Profile** in MikroTik → assign password, cipher, auth type.
2. Assign profile to **AP interface / SSID**.
3. Clients connecting to that SSID use the profile → must match password + encryption.
4. Allows you to **centralize security settings** without editing individual interfaces.

---

## 🧠 Exam Notes

- **Security Profile ≠ SSID**
- One profile can be used by **multiple SSIDs**
- Default profile: usually **none** (no encryption)
- Always use **WPA2 AES** for exam recommendations

---

## 🔑 Quick Memory Trick

- **SSID = name users see**  
- **Security Profile = rules users must follow to connect**
<img width="548" height="532" alt="image" src="https://github.com/user-attachments/assets/0f16b7d9-d79e-419c-9f8a-d03472a9ce50" />

