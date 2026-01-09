
# MikroTik IP Addressing & Troubleshooting Walkthrough

This walkthrough takes you from a **broken or confusing default MikroTik setup** to a **fully working home LAN configuration**.

It focuses on:

* Understanding why connectivity fails
* Moving away from the default `192.168.88.1` subnet
* Correctly assigning IP addresses and configuring DHCP on a MikroTik router

This guide assumes you are using **RouterOS via the Terminal** (WinBox, SSH, or Console).

---

## Network Goal

By the end of this guide, you should have:

* Router LAN IP set to `192.168.0.1/24`
* Clients receiving IP addresses automatically via DHCP
* All LAN ports operating through a single bridge interface

---

## Phase 1: Fixing the “No Route” / 100% Packet Loss Issue

If you try to `ping` another device or a website and receive **100% packet loss** or a **no route to host** error, the issue is almost always related to Layer 1 (physical) or Layer 3 (IP addressing).

### Step 1: Check IP Address Status

Run the following command:

```bash
/ip address print
```

Look at the **flags** on the far left.

| Flag          | Meaning                                              |
| ------------- | ---------------------------------------------------- |
| `I` (Invalid) | Interface is down, disabled, or has no physical link |
| `A` (Active)  | Interface is up and functioning correctly            |

If the IP address shows **Invalid**, routing will not work regardless of other settings.

---

### Step 2: Verify the Physical Layer

Ensure that:

* The Ethernet cable is plugged in
* The port is a member of the **bridge**
* The port link LED is on

If the cable is unplugged or the port is not part of the bridge, the IP address will remain **Invalid**.

---

## Phase 2: Configuring Your Home Subnet (192.168.0.0/24)

By default, MikroTik routers use the `192.168.88.1` subnet. This section replaces it with a custom home subnet.

### Step 1: Assign the New LAN IP Address

Always assign LAN IP addresses to the **bridge interface**, not to individual Ethernet ports.

```bash
/ip address add address=192.168.0.1/24 interface=bridge
```

This ensures all LAN ports (ether2, ether3, etc.) operate within the same network.

---

### Step 2: Remove the Default IP Address

Leaving the default IP can cause routing conflicts.

```bash
/ip address remove [find address="192.168.88.1/24"]
```

At this point, the router’s LAN IP is officially `192.168.0.1`.

---

### Step 3: Configure DHCP for LAN Clients

This allows laptops, phones, and other devices to obtain IP addresses automatically.

```bash
/ip pool add name=dhcp-pool ranges=192.168.0.10-192.168.0.254
/ip dhcp-server add name=lan-dhcp interface=bridge address-pool=dhcp-pool
/ip dhcp-server network add address=192.168.0.0/24 gateway=192.168.0.1 dns-server=8.8.8.8
```

After this configuration:

* Clients should receive IP addresses in the `192.168.0.x` range
* The default gateway will be `192.168.0.1`

---

## Phase 3: MikroTik Terminal Productivity Tips

These shortcuts help keep your workflow clean and prevent mistakes.

| Shortcut         | Description                                             |
| ---------------- | ------------------------------------------------------- |
| `Tab`            | Auto-completes commands (press twice to list options)   |
| `Ctrl + C`       | Stops a running command such as `ping`                  |
| `..`             | Moves up one menu level                                 |
| `/`              | Returns to the root menu                                |
| `safe-mode` (F1) | Automatically reverts changes if the connection is lost |

**Always use Safe Mode when changing IP addresses.**

---

## Final Checklist

Before troubleshooting routing or firewall rules, verify the following:

* [ ] Ethernet cable is connected and link light is on
* [ ] IP address status is **Active**, not Invalid
* [ ] IP address is assigned to the **bridge**
* [ ] DHCP server matches the configured subnet
* [ ] Client has received an IP in the `192.168.0.x` range

---

## Next Steps

This configuration only establishes **local network connectivity**.

To access the internet, you still need:

* NAT (masquerade)
* A properly configured WAN interface
* Basic firewall rules





Say the word, Boss.
