## 1) Station Bridge (Wireless Bridge)

### What people usually mean

* Two devices connected wirelessly
* Traffic passes at Layer 2 (MAC addresses pass)

### How it is actually built

* One side: **AP Bridge**
* Other side: **Station Bridge**
* Often uses **WDS** or **4-address mode**
 ### Note 
* ❌ Always Disbale the DCHP SERVER
* ❌ No NAT Rule is Needed here 

### Use case

* Point-to-point wireless link acting like an Ethernet cable

<img width="1257" height="714" alt="image" src="https://github.com/user-attachments/assets/5ebc1882-4deb-4f58-a7da-d69e8f93974c" />





---

## 2) Station Mode

### What it is

* Standard Wi-Fi client mode

### What it does

* Connects to **one** access point
* Works at **Layer 3**
* Does **not** pass MAC addresses

### Limitations

* Not suitable for bridging networks
* Broadcasts, ARP, and DHCP do not pass transparently

### Use case

* Internet access only
* Client-like behavior

### Think of it as

* A phone or laptop connecting to Wi-Fi

<img width="1024" height="1024" alt="station-mode" src="https://github.com/user-attachments/assets/8dba2925-3306-4686-a5d7-eff413ed9de8" />

---

## 3) AP Bridge (Access Point Bridge)

### What it is

* Wireless access point mode that supports **Layer 2 bridging**
* The **AP side** of a wireless bridge setup
* Required when using **Station Bridge** on the other side

### What it does

* Accepts multiple wireless clients
* Passes MAC addresses when paired with Station Bridge or WDS
* Allows wireless interfaces to be added to a normal bridge

### How it works

* AP Bridge ↔ Station Bridge = **true Layer 2 link**
* Behaves like a wireless switch
* DHCP, ARP, and broadcasts pass normally

### Requirements

* Usually **MikroTik ↔ MikroTik**
* Same wireless standards and security
* Often uses **4-address mode** or **WDS**

### Use cases

* Point-to-point links
* Point-to-multipoint wireless distribution
* Replacing Ethernet cables wirelessly
* Extending the same subnet over wireless

### When NOT to use

* With normal Wi-Fi clients only (phones, laptops)
* If Layer 2 transparency is not needed

### Think of it as

* A wireless switch port talking to Station Bridge devices

### Quick summary

* AP Bridge = server side
* Station Bridge = client side
* Together = real wireless bridge

---

## 4) Station Pseudobridge

### What it is

* A workaround mode allowing a station to connect to an AP when **true Station Bridge is not supported**
* Commonly used with **non-MikroTik APs**

### How it works

* Connects like a normal station
* MikroTik **spoofs MAC addresses** for devices behind it
* Appears to the AP mostly as a single device

### Key limitations

* ❌ Not a real Layer 2 bridge
* ❌ MAC-based protocols may fail
* ❌ Some applications may not work correctly
* ❌ Possible ARP and broadcast issues

### When to use

* You must connect multiple devices
* The AP does not support Station Bridge
* As a **last-resort solution**

### When NOT to use

* ISP or enterprise networks
* When you control both sides of the link

### Quick summary

* Station Bridge → real bridge (MikroTik ↔ MikroTik)
* Station Pseudobridge → fake bridge (compatibility mode)

---

## Quick Comparison Table
| Mode            | OSI Layer | Connects To | Passes MAC | Typical Use         |
|-----------------|-----------|-------------|------------|---------------------|
| Station Mode    | L3        | One AP      | No         | Internet access     |
| Station Bridge  | L2        | One AP      | Yes        | Network extension   |


---

## Common Mistakes to Avoid

* Station Bridge does **not** connect to multiple APs
* It does **not** collect Wi-Fi from different sources
* Load balancing requires routing, not wireless bridge modes

---

## Summary

* **Bridge** joins interfaces locally
* **Station** is a normal Wi-Fi client
* **Station Bridge** extends a network at Layer 2
* **Wireless bridge** is a design concept, not a mode


