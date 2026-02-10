ARP (Address Resolution Protocol) maps:  
- *IP address → MAC address*

So when a device knows an IP but not the MAC, it uses ARP to find it.

Normally this is *dynamic ARP*:
- Device asks: Who has 192.168.1.10?
- That device replies with its MAC
- Entry is stored temporarily and can change

---

## What is Static ARP?

*Static ARP* is a manually defined IP–MAC mapping that:
- Does not change
- Does not expire
- Ignores ARP replies for that IP

You’re basically telling the device:  
For this IP, *ONLY* use this MAC. Don’t ask, don’t learn, don’t update.

---

## Why would anyone use Static ARP?

Real reasons, not textbook ones:

### 1. Security
- Prevents ARP spoofing / ARP poisoning
- Attackers cannot pretend to be another IP

### 2. Critical devices
- Routers, firewalls, servers, gateways
- You want zero surprises

### 3. Stable networks
- Small or controlled environments
- Industrial systems, IP phones, cameras

---

## Downsides (important)

Static ARP is *not scalable*:
- If the device’s NIC changes → network breaks
- If IP or MAC changes → manual fix required
- Painful in large or dynamic networks

That’s why it’s not used everywhere.

---

## Static ARP in MikroTik (example)

On MikroTik, you’d do something like:
- IP: 192.168.1.1
- MAC: AA:BB:CC:DD:EE:FF
- Set ARP entry as *static*

Result:
- MikroTik will never learn or accept another MAC for that IP

---

## Dynamic ARP vs Static ARP (simple)

- *Dynamic ARP*: flexible, automatic, less secure  
- *Static ARP*: fixed, manual, more secure

---

## When YOU should care

Since you’re doing networking + MikroTik + real infrastructure:

*Use Static ARP for:*
- Default gateway
- Core devices

*Don’t use it for:*
- Normal users
- Laptops, phones, guest devices

<img width="813" height="553" alt="image" src="https://github.com/user-attachments/assets/2e4a1eef-c355-41dc-bd6b-78342b34d5c1" />
