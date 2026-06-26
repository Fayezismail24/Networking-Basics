# Physical Layer (OSI Layer 1)

## What is the Physical Layer?

The Physical Layer is the first and lowest layer of the OSI model.
It is responsible for transmitting raw bits (0s and 1s) over a physical medium
between devices. It does not care about what the data means — it only
handles how bits are electrically, optically, or wirelessly sent from point A to point B.

---

## Responsibilities

- Bit transmission (0s and 1s)
- Defining voltage levels, signal timing, and bit rate
- Defining physical connectors and cable types
- Encoding and signaling
- Synchronization of bits between sender and receiver

---

## Transmission Media

### Copper (Electrical)

| Type | Standard | Max Speed | Max Distance |
|------|----------|-----------|--------------|
| UTP Cat5e | 1000BASE-T | 1 Gbps | 100m |
| UTP Cat6 | 1000BASE-T | 1 Gbps | 100m |
| UTP Cat6a | 10GBASE-T | 10 Gbps | 100m |
| Coaxial | — | Legacy | Varies |

> UTP = Unshielded Twisted Pair. Most common in LAN environments.

### Fiber Optic (Light)

| Type | Core Size | Distance | Use Case |
|------|-----------|----------|----------|
| SMF (Single-Mode) | 8–10 µm | Up to 100km+ | WAN, ISP backbone |
| MMF OM3 | 50 µm | Up to 300m | Data center |
| MMF OM4 | 50 µm | Up to 400m | Data center |
| MMF OM5 | 50 µm | Up to 400m+ | High-density data center |

> SMF uses a laser light source. MMF uses LED. SMF = long distance, MMF = short distance.

### Wireless (Radio Frequency)

| Standard | Frequency | Max Speed | Notes |
|----------|-----------|-----------|-------|
| 802.11n (Wi-Fi 4) | 2.4 / 5 GHz | 600 Mbps | Legacy, still common |
| 802.11ac (Wi-Fi 5) | 5 GHz | 3.5 Gbps | Most deployed standard |
| 802.11ax (Wi-Fi 6) | 2.4 / 5 / 6 GHz | 9.6 Gbps | Current standard |

---

## Connectors

| Connector | Used With | Notes |
|-----------|-----------|-------|
| RJ-45 | UTP copper | Standard LAN connector |
| LC | Fiber optic | Small form factor, common in data centers |
| SC | Fiber optic | Push-pull, older installations |
| SFP / SFP+ | Fiber or copper | Pluggable transceiver on switches/routers |

---

## Cable Wiring Standards

| Standard | Pair Order | Used For |
|----------|------------|----------|
| T568A | Green first | Some older installs |
| T568B | Orange first | Most common in production |

### Straight-Through vs Crossover

| Cable Type | Wiring | Used Between |
|------------|--------|--------------|
| Straight-through | T568B both ends | Different device types (PC ↔ Switch) |
| Crossover | T568A one end, T568B other | Same device types (Switch ↔ Switch) |

> Modern devices support **Auto-MDI/MDIX** — they detect and adjust automatically,
> making crossover cables mostly obsolete.

---



## Key Terms

| Term | Definition |
|------|------------|
| Bit rate | Number of bits transmitted per second (bps) |
| Bandwidth | Maximum capacity of the medium |
| Latency | Delay from source to destination |
| Attenuation | Signal loss over distance |
| Noise / EMI | Interference that corrupts the signal |
| Duplex | Half = one direction at a time, Full = both simultaneously |

---

## Layer 1 Devices

| Device | Role |
|--------|------|
| Hub | Repeats signal to all ports — no intelligence, Layer 1 only |
| Repeater | Regenerates and extends signal |
| Modem | Modulates/demodulates signal between digital and analog |
| Access Point | Converts wired signal to wireless (RF) |

> Switches operate at Layer 2, not Layer 1 — they read MAC addresses.
> Hubs are Layer 1 — they blindly repeat bits.

---


