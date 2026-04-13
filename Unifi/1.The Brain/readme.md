
The Brain — UniFi Network Application

## What is the UniFi Ecosystem?

UniFi is a line of networking products made by **Ubiquiti Networks**.  
The product lineup includes:

- **USG / UDM** — Routers & gateways (handle routing, firewall, NAT)
- **UniFi Switches** — Managed switches (VLANs, PoE)
- **UniFi Access Points** — WiFi devices (UAP series)
- **UniFi Protect / Access / Talk** — Cameras, door access, VoIP (separate apps)

All of these devices are "dumb" on their own — they wait for instructions.  
That's where the brain comes in.

---

## The Brain: UniFi Network Application (Controller)

The **UniFi Network Application** is a software platform that:

- **Adopts** UniFi devices (USG, APs, switches) into one managed network
- Provides a **single dashboard** to configure everything
- Handles **provisioning** — pushes configuration to each device
- Stores **statistics, logs, and topology maps**

> Without the Controller, UniFi devices run in a limited standalone mode  
> and cannot be fully configured or coordinated together.

---

## How It Works

```
[ UniFi Network Application ]
           │
    ┌──────┴──────┐
   [USG]        [AP]
  Router      WiFi Device
```

1. You install the Network Application on a PC, server, or Cloud Key
2. Devices on the same network are **discovered automatically**
3. You **adopt** each device — it gets provisioned by the Controller
4. From that point, all config changes go through the Controller

---

## Key Concept: Adoption

**Adoption** = the process of a UniFi device registering itself  
under a specific Controller instance.

- Before adoption: device is in factory/default state
- After adoption: device is fully managed, config is pushed from Controller
- If you reset a device: it needs to be **re-adopted**

---

## Does the Controller Need to Run 24/7?

**No** — for a basic home/office setup.

- The network runs fine without the Controller active
- You only need it open to **make changes** or **view statistics**
- For always-on stats and auto-updates, run it on a dedicated machine or Cloud Key

---

## Installation Options

| Option | Best For |
|---|---|
| Windows / Mac PC | Home lab, small office |
| Linux server / VM | Always-on, production |
| Raspberry Pi | Low-power always-on |
| UniFi Cloud Key | Dedicated plug-and-play hardware |
| UniFi Dream Machine | All-in-one (controller built-in) |

