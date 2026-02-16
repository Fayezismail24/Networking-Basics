

# Point-to-Point Protocol (PPP)

- **Point-to-Point Protocol (PPP)** is used to establish a tunnel (direct connection) between two nodes.

## 1. Core Functions of PPP

PPP isn't just about moving data; it’s about managing the connection. It performs three critical roles:

* **Authentication:** Ensures only authorized users can connect.
* *PAP (Password Authentication Protocol):* Sends passwords in plain text (less secure).
* *CHAP (Challenge Handshake Authentication Protocol):* Uses a 3-way handshake to verify identity without sending the password over the link.


* **Compression:** Shrinks data packets to increase throughput on slower links.
* **Encryption:** Scrambles data (often using **MPPE** - Microsoft Point-to-Point Encryption) so it cannot be read if intercepted.

---

## 2. Common PPP Implementations in MikroTik

MikroTik's **RouterOS** uses PPP as the foundation for several different "tunnels."

| Protocol | Description | Usage Case |
| --- | --- | --- |
| **PPPoE** | PPP over Ethernet | The standard for ISPs to deliver internet to homes (requires a username/pass). |
| **PPTP** | Point-to-Point Tunneling Protocol | Fast and easy to set up, but considered **insecure** by modern standards. |
| **L2TP** | Layer 2 Tunneling Protocol | Usually combined with **IPsec** for high-security office-to-office links. |
| **SSTP** | Secure Socket Tunneling Protocol | Uses TCP Port 443 (HTTPS), making it excellent for bypassing strict firewalls. |
| **OVPN** | OpenVPN | A highly flexible, open-source tunneling standard supported by MikroTik. |

---

## 3. How it Works in RouterOS

In the MikroTik GUI (WinBox), the PPP menu is divided into several logical sections:

1. **Profiles:** These are "templates." You define things like DNS servers, local/remote IP addresses, and rate limits (bandwidth) here.
2. **Secrets:** This is your user database. Every "Secret" is a unique **Username** and **Password** assigned to a specific Profile.
3. **Interfaces:** This is where you enable the actual server (e.g., clicking "PPPoE Server" to turn it on).
4. **Active Connections:** A real-time list showing exactly who is currently logged into your router via PPP.

---

## 4. Why Use Tunnels?


* It allows **Private IP** communication over the **Public Internet**.
* It provides a layer of **Management**: You can kick users off, limit their speed, or change their access rights instantly through the PPP Secret.

 **Note:** When configuring PPP on MikroTik, always ensure your **Firewall** allows the specific port for the protocol you chose (e.g., TCP 1723 for PPTP or UDP 1701 for L2TP).

