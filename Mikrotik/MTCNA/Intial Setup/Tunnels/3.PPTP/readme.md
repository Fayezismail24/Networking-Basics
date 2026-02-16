
# PPTP (Point-to-Point Tunneling Protocol)

**PPTP (Point-to-Point Tunneling Protocol)** is an old **VPN protocol** used to create secure connections over a public network like the internet. It was developed by **Microsoft** and is still supported by many devices, but it is considered **obsolete and insecure**.

## Key Features:
- **Tunneling Protocol**: Encapsulates data for transmission over the internet using **PPP** (Point-to-Point Protocol).
- **Encryption**: Uses **MPPE** (Microsoft Point-to-Point Encryption), which is considered weak by modern standards.
- **Authentication**: Supports **PAP** and **CHAP** methods for user authentication.
- **Compatibility**: Supported by most operating systems and devices, making it easy to set up.

## Security Weaknesses:
- **Weak Encryption**: MPPE encryption is easily cracked with modern tools.
- **No Perfect Forward Secrecy**: Older sessions can be decrypted if a key is compromised.
- **Deprecated**: Microsoft has deprecated PPTP in favor of more secure protocols like **L2TP/IPsec** and **SSTP**.

## Usage:
- **Legacy Systems**: Still used for compatibility with older systems.
- **Low-Security Needs**: Suitable for simple setups where high security is not a concern.

## Alternatives:
- **L2TP/IPsec**: Offers better security and encryption.
- **OpenVPN**: Highly secure and open-source, recommended for most use cases.
- **SSTP**: Uses SSL/TLS encryption, offering better security than PPTP.

**Conclusion**: While PPTP is easy to set up and compatible with many devices, it is not recommended for modern VPN connections due to its known security flaws.


Exam  Note :
PPTP USES port : 
1723 TCP 
47 IP Protocol
NAT Helper used to help PPTP in NAT'D area 
