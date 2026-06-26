
# Wiring Network Devices — Straight-Through vs Crossover Cables

## Overview

When connecting two network devices using copper UTP cables, the wiring
order on each end determines whether the cable works or not.
There are two types:

- **Straight-through** — both ends wired the same way (T568B to T568B)
- **Crossover** — ends wired differently (T568A to T568B)

The rule is simple:
- Same device type → crossover
- Different device types → straight-through

---

## T568A vs T568B Pin Order

| Pin | T568A | T568B |
|-----|-------|-------|
| 1 | White/Green | White/Orange |
| 2 | Green | Orange |
| 3 | White/Orange | White/Green |
| 4 | Blue | Blue |
| 5 | White/Blue | White/Blue |
| 6 | Orange | Green |
| 7 | White/Brown | White/Brown |
| 8 | Brown | Brown |

> T568B is the most common standard used in production environments.
> T568A is sometimes used in government or older installations.
> Never mix standards on the same cable end.

---

## Straight-Through Cable

### Wiring

Both ends follow the same standard — T568B on both sides.

```
End A (T568B)          End B (T568B)
Pin 1 ────────────── Pin 1
Pin 2 ────────────── Pin 2
Pin 3 ────────────── Pin 3
Pin 6 ────────────── Pin 6
```

### When to Use

| Device A | Device B | Cable |
|----------|----------|-------|
| PC / Laptop | Switch | Straight-through |
| PC / Laptop | Hub | Straight-through |
| Router | Switch | Straight-through |
| Router | Hub | Straight-through |
| Access Point | Switch | Straight-through |
| IP Camera | Switch | Straight-through |
| VoIP Phone | Switch | Straight-through |

> Rule: different device types = straight-through.

---

## Crossover Cable

### Wiring

One end is T568A, the other end is T568B.
This crosses the TX pins of one device into the RX pins of the other.

```
End A (T568A)          End B (T568B)
Pin 1 (TX+) ────────── Pin 3 (RX+)
Pin 2 (TX-) ────────── Pin 6 (RX-)
Pin 3 (RX+) ────────── Pin 1 (TX+)
Pin 6 (RX-) ────────── Pin 2 (TX-)
```

### When to Use

| Device A | Device B | Cable |
|----------|----------|-------|
| Switch | Switch | Crossover |
| Switch | Hub | Crossover |
| Hub | Hub | Crossover |
| Router | Router | Crossover |
| PC | PC (direct) | Crossover |
| Router | PC (direct) | Crossover |

> Rule: same device type = crossover.

---

## TX and RX Pin Logic

Understanding why crossover cables work requires knowing which pins
each device uses to transmit (TX) and receive (RX).

| Device Type | TX Pins | RX Pins |
|-------------|---------|---------|
| PC / Router (MDI) | 1, 2 | 3, 6 |
| Switch / Hub (MDI-X) | 3, 6 | 1, 2 |

- A PC transmits on pins 1 and 2
- A switch receives on pins 1 and 2
- They are opposite → straight-through works

- A PC transmits on pins 1 and 2
- Another PC also transmits on pins 1 and 2
- They collide → crossover is needed to flip TX into RX

---

## Auto-MDI/MDIX

Modern switches, routers, and NICs support **Auto-MDI/MDIX**.
The device electronically detects the cable type and adjusts internally.

| Feature | Detail |
|---------|--------|
| What it does | Automatically crosses or un-crosses TX/RX pairs |
| Where it is | Most devices made after ~2005 |
| Result | Either cable type works — straight-through or crossover |
| Cisco support | All modern Catalyst and ISR devices support it |

> Auto-MDI/MDIX makes crossover cables mostly obsolete in modern networks.
> However, CCNA requires you to know the manual rules — exam questions
> will test you on which cable to use without assuming Auto-MDI/MDIX.

---

## Quick Decision Chart

```
Are you connecting two devices of the SAME type?
        │
        ├── YES → Crossover cable
        │         (Switch↔Switch, PC↔PC, Router↔Router)
        │
        └── NO  → Straight-through cable
                  (PC↔Switch, Router↔Switch, AP↔Switch)
```

---

## Common Mistakes

| Mistake | Result |
|---------|--------|
| Using straight-through between two switches | No link or duplex issues |
| Using crossover between PC and switch | No link (unless Auto-MDI/MDIX saves it) |
| Mixing T568A and T568B randomly | Incorrect pin mapping, no connectivity |
| Using Cat5 for Gigabit | Works for 1Gbps but no headroom — use Cat5e minimum |
| Forgetting pins 4, 5, 7, 8 matter for PoE | PoE uses all 4 pairs — bad crimp = no power |

---

## PoE Note (Power over Ethernet)

Standard PoE (802.3af/at) uses all 8 pins across 4 pairs.
A poorly crimped cable may pass data but fail to deliver power to a PoE device
such as a UniFi AP, IP camera, or VoIP phone.

| PoE Standard | Power Delivered | Pairs Used |
|--------------|-----------------|------------|
| 802.3af (PoE) | 15.4W | 2 pairs |
| 802.3at (PoE+) | 30W | 2 pairs |
| 802.3bt (PoE++) | 60–90W | 4 pairs |

> Always use Cat5e or higher for PoE. Always crimp all 8 pins correctly.

---

## Summary

| Cable Type | End A | End B | Use Case |
|------------|-------|-------|----------|
| Straight-through | T568B | T568B | Different device types |
| Crossover | T568A | T568B | Same device types |

- Pins 1, 2 = TX on MDI devices (PC, Router)
- Pins 3, 6 = RX on MDI devices
- Crossover flips TX into RX between same device types
- Auto-MDI/MDIX handles this automatically on modern hardware
- Know the manual rules for the CCNA exam regardless
