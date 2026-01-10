Good question. Here is the **correct way to think about it** when you have **multiple interfaces**. I’ll be direct.

---

## Key rule (don’t skip this)

👉 **Only ONE interface should be your WAN (internet-facing).**
👉 **All LAN interfaces should be bridged together.**

If you don’t separate this clearly, routing and NAT will break.

---

## Case 1: Multiple LAN interfaces (most common)

If you have:

* `ether2`
* `ether3`
* `ether4`

These should all be in **one bridge**.

### Correct setup

```bash
/interface bridge /add name=bridge
/interface bridge port /add bridge=bridge interface=ether2
/interface bridge port /add bridge=bridge interface=ether3
/interface bridge port /add bridge=bridge interface=ether4
```

Then assign **ONE IP** to the bridge (not to each interface):

```bash
/ip address /add address=192.168.0.1/24 interface=bridge
```

✅ This is correct
❌ Do NOT assign IPs to each LAN port individually

---

## Case 2: WAN interface is separate

Example:

* `ether1` = WAN
* `bridge` = LAN

Your **default route must point toward the WAN**, not LAN.

### Option A: Gateway IP known (most common)

```bash
/ip route /add gateway=192.168.0.254
```

This assumes:

* `192.168.0.254` is reachable via `ether1`

---

### Option B: Gateway via interface (useful with DHCP or unknown gateway)

```bash
/ip route /add gateway=ether1
```

RouterOS will automatically use the next-hop learned on that interface.

---

## Case 3: Multiple WAN interfaces (advanced)

If you have:

* `ether1` = ISP 1
* `ether5` = ISP 2

⚠️ Stop here unless you are intentionally doing:

* failover
* load balancing
* policy routing

In that case, **you do NOT use a single default route**.
You use **routing marks and distances**.

If this is not intentional, **you are doing it wrong**.

---

## NAT note (important if internet is involved)

Masquerade must be applied **only on the WAN interface**:

```bash
/ip firewall nat /add chain=srcnat out-interface=ether1 action=masquerade
```

❌ Never masquerade on the bridge
❌ Never masquerade on LAN interfaces

---

## Correct mental model (remember this)

* **Bridge = LAN**
* **Bridge gets ONE IP**
* **WAN interface = upstream**
* **Default route points to WAN**
* **Masquerade only on WAN**

---

## Your current guide (verdict)

Your markdown is **correct IF**:

* `bridge` = all LAN ports
* Gateway `192.168.0.254` is upstream via WAN

If not, it must be adjusted.

---


