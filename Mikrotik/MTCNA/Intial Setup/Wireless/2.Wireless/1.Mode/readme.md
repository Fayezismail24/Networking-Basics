

## 1) Bridge (Normal Bridge – NOT a wireless mode)

*What it is*
- A virtual interface that joins multiple interfaces together
- Can include Ethernet ports and wireless interfaces

*What it does*
- Makes all added interfaces behave as one network
- Single DHCP server and one subnet

*Example*
- ether1 + ether2 + wlan1 → bridge
- Any connected device gets an IP from the same DHCP pool

*Think of it as*
- Glue that sticks interfaces together

---

## 2) Wireless Bridge (Concept, not a real mode)

*Important*
- This is NOT an actual MikroTik wireless mode
- It’s a commonly used term

*What people usually mean*
- Two devices connected wirelessly
- Traffic passes at Layer 2 (MAC addresses pass)

*How it is actually built*
- One side: AP Bridge
- Other side: Station Bridge
- Often uses WDS or 4-address mode

*Use case*
- Point-to-point wireless link acting like an Ethernet cable

---

## 3) Station

*What it is*
- Standard Wi-Fi client mode

*What it does*
- Connects to ONE access point
- Works at Layer 3
- Does NOT pass MAC addresses

*Limitations*
- Not suitable for bridging networks
- Broadcasts, ARP, and DHCP do not pass transparently

*Use case*
- Internet access only
- Client-like behavior

*Think of it as*
- A phone or laptop connecting to Wi-Fi

---

## 4) Station Bridge

*What it really does*
- Connects to ONE access point only
- Works at Layer 2
- Passes MAC addresses

*Requirements*
- Access point must support bridging
- Usually requires AP Bridge, WDS, or 4-address mode

*What it does NOT do*
- Does NOT connect to multiple access points
- Does NOT aggregate or load-balance Wi-Fi links

*Use case*
- Point-to-point or point-to-multipoint links
- Extending a LAN over wireless
- Replacing an Ethernet cable

*Example*
- Main router → AP Bridge
- Remote router → Station Bridge
- Remote LAN behaves as if it’s connected by cable

*Think of it as*
- A wireless Ethernet cable

---

## Quick Comparison Table

| Mode | OSI Layer | Connects To | Passes MAC | Typical Use |
|----|----|----|----|----|
| Bridge | L2 | Interfaces | Yes | Combine ports |
| Station | L3 | One AP | No | Internet access |
| Station Bridge | L2 | One AP | Yes | Network extension |
| Wireless bridge | L2 | AP ↔ Station Bridge | Yes | Cable replacement |

---

## Common Mistakes to Avoid

- Station Bridge does *not* connect to multiple APs
- It does *not* collect Wi-Fi from different sources
- Load balancing requires routing, not wireless bridge modes

## Summary

- *Bridge* joins interfaces locally
- *Station* is a normal Wi-Fi client
- *Station Bridge* extends a network at Layer 2
- *Wireless bridge* is a design concept, not a mode

Got you, Boss 👍
Here’s the **added section in Markdown**, ready to drop into your MikroTik wireless types notes.


## Station Pseudobridge

**What it is**
- A workaround mode that allows a **station** to connect to an AP **when true Station Bridge is not supported**
- Commonly used when connecting a MikroTik station to **non-MikroTik APs**

**How it works**
- The station connects wirelessly like a normal client
- MikroTik **fakes (spoofs) MAC addresses** so multiple devices behind it can pass traffic
- To the AP, it mostly looks like **one device**, not a real bridge

**Key limitations**
- ❌ Not a real Layer 2 bridge
- ❌ MAC-based protocols may break
- ❌ Some applications may not work correctly
- ❌ Can cause issues with ARP and broadcasts

**When to use**
- When you **must connect multiple devices**
- And the AP **does NOT support Station Bridge**
- As a **last-resort solution**

**When NOT to use**
- In professional or ISP-grade networks
- When you control both sides and can use **Station Bridge**

**Quick summary**
- Station Bridge → real bridge (MikroTik to MikroTik)
- Station Pseudobridge → fake bridge (compatibility mode)
```
