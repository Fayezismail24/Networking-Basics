
````md
# Minimal MikroTik IP Change (Default IP → New IP + Gateway)

### 1. View existing IP addresses (optional but recommended)

```bash
/ip address /print
````

---

### 2. Remove the default MikroTik IP (192.168.88.1)

```bash
/ip address /remove [find address="192.168.88.1/24"]
```

---

### 3. Assign the new LAN IP to the bridge

```bash
/ip address /add address=192.168.0.1/24 interface=bridge
```

This IP will be the **default gateway for LAN devices**.

---

### 4. Set the default gateway for the MikroTik router

Replace `192.168.0.254` with the actual gateway IP of your upstream network (the next hop toward the internet):

```bash
/ip route /add gateway=192.168.0.254
```

---

### Result

* Router LAN IP: `192.168.0.1`
* Default gateway for clients: `192.168.0.1`
* MikroTik router default route points to: `192.168.0.254`
* Default MikroTik subnet fully removed

That’s it.
No DHCP, no NAT, no firewall. Just **IP + gateway done correctly**.




