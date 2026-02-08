## What is ARP = Reply-Only?

*Reply-only* means:
- The router will *NOT* answer ARP requests
- It will *ONLY* reply if the IP–MAC pair already exists in its ARP table

In simple words:  
*No ARP entry → no communication*

---

## Normal ARP (enabled)

- Client asks: Who has 192.168.1.1?
- Router replies automatically
- Router learns IP–MAC dynamically

Easy, open, less secure.

---

## Reply-Only ARP behavior

With *reply-only*:
- Router ignores unknown ARP requests
- Router only communicates with *pre-approved devices*
- Devices must be manually added (static ARP or via DHCP lease)

Think of it like a *bouncer at the door*:  
No name on the list → you don’t get in.

---

## Why use Reply-Only?

1. Stops ARP spoofing  
2. Blocks unknown devices  
3. Forces IP–MAC binding  

*Common use cases:*
- Hotspots
- ISP customer networks
- IP cameras
- Secure office LANs

---

## How devices are allowed in Reply-Only

Two ways:

### 1. Static ARP entry
- You manually add IP + MAC

### 2. DHCP lease with ARP binding
- DHCP gives IP
- MikroTik auto-adds ARP entry
- Still controlled and safe

---

## What breaks if you forget this?

If you enable *reply-only* and:
- Forget to add ARP entries

Results:
- Clients get no internet
- Even ping fails
- People think the network is dead

Classic mistake.

---

## Static ARP vs Reply-Only (don’t confuse them)

- *Static ARP*: an entry type  
- *Reply-only*: an interface rule  

They work together, not the same thing.

---

## Quick example

You set:
- Interface ARP = reply-only
- Client IP: 192.168.1.10
- Client MAC: AA:BB:CC:DD:EE:FF

If that entry exists → works  
If not → blocked silently

---

## When you should use it

*Use it when:*
- You want tight control
- You know all devices

*Avoid it when:*
- Network is large
- Devices change often
- You want plug-and-play

---

