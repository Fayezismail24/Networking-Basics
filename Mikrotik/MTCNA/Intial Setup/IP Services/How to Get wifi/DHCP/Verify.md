

---

# Verifying MikroTik Configuration via CLI (MTCNA Style)

This guide walks through verifying your MikroTik setup using the **Command Line Interface (CLI)**.
You will check:

* Interfaces and bridge
* IP addressing
* DHCP server operation
* End-to-end connectivity

---

## 1. Verify Interface and Bridge Status

Ensure the bridge exists and the correct interfaces are attached.

### Check Bridges

```bash
/interface bridge /print
```

**Look for:**

* A bridge named `LAN`
* `R` (Running) flag enabled

---

### Check Bridge Ports

```bash
/interface bridge port /print
```

**Look for:**

* `ether2` (and other LAN ports) assigned to the `LAN` bridge

---

### Check Physical Interfaces

```bash
/interface /print
```

**Look for:**

* `ether1` (WAN) and `ether2` (LAN) both showing `R` (Running)
* If `ether2` is not running, the Windows machine is not physically detected

---

## 2. Verify IP Addressing

Confirm WAN uses DHCP and LAN has a static IP.

### Check DHCP Client (WAN)

```bash
/ip dhcp-client /print
```

**Look for:**

* `status=bound`
* Interface set to `ether1`

---

### Check Static IP (LAN)

```bash
/ip address /print
```

**Look for:**

* Static IP (example: `192.168.88.1/24`)
* Assigned to the **LAN bridge**, not directly to `ether2`

---

## 3. Verify DHCP Server Operation

Ensure the router can distribute IP addresses to LAN clients.

### Check DHCP Server

```bash
/ip dhcp-server /print
```

**Look for:**

* Server enabled and running on `LAN`
* No red text (red indicates configuration errors, usually IP mismatch)

---

### Check DHCP Network Settings

```bash
/ip dhcp-server network /print
```

**Look for:**

* Correct `gateway`
* Correct `dns-server` values for clients

---

### Check Active DHCP Leases

```bash
/ip dhcp-server lease /print
```

**Look for:**

* Windows machine MAC address
* Assigned IP with `status=bound`

---

## 4. Test Connectivity

Verify that traffic flows correctly.

### Test Internet (WAN)

```bash
ping 8.8.8.8
```

Confirms ISP connectivity.

---

### Test LAN Client

```bash
ping <Windows_IP>
```

Confirms LAN communication.

---

### Check Discovered Devices

```bash
/ip neighbor /print
```

Shows devices detected via MNDP.
Windows may appear if Network Discovery is enabled.

---

## 5. Verify NAT (Internet Access for LAN)

If clients get an IP but have **no internet**, check NAT.

### Check NAT Rules

```bash
/ip firewall nat /print
```

**You should have a masquerade rule for the WAN interface.**

### Add NAT Masquerade Rule (If Missing)

```bash
/ip firewall nat /add chain=srcnat out-interface=ether1 action=masquerade
```

---

## Summary Checklist

* Bridge `LAN` exists and is running
* `ether2` is part of the bridge
* WAN DHCP client is bound
* LAN IP is on the bridge
* DHCP server is active on LAN
* NAT masquerade is configured on WAN

---

If you want, next we can:

* Turn this into a **lab diagram**
* Split it into **WAN vs LAN verification**
* Or convert it into a **GitHub repo folder structure**
