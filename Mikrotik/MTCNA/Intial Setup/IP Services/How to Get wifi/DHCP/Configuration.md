

```bash
# 1) WAN – DHCP Client on ether1
/ip dhcp-client
/add interface=ether1 disabled=no

# 2) LAN Bridge
/interface bridge
/add name=LAN

# 3) Add LAN ports to bridge
/interface bridge port
/add bridge=LAN interface=ether2
/add bridge=LAN interface=wlan1
/add bridge=LAN interface=wlan2

# 4) Assign IP address to LAN bridge
/ip address
/add address=192.168.10.1/24 interface=LAN

# 5) DHCP Address Pool
/ip pool
/add name=LAN_POOL ranges=192.168.10.10-192.168.10.254

# 6) DHCP Network
/ip dhcp-server network
/add address=192.168.10.0/24 gateway=192.168.10.1 dns-server=192.168.10.1

# 7) DHCP Server on LAN bridge
/ip dhcp-server
/add name=LAN_DHCP interface=LAN address-pool=LAN_POOL disabled=no

# 8) DNS Configuration
/ip dns
/set allow-remote-requests=yes servers=8.8.8.8,1.1.1.1

# 9) NAT (Masquerade for Internet Access)
/ip firewall nat
/add chain=srcnat out-interface=ether1 action=masquerade
```

---

## ✔ What this config gives you

* ether1 gets internet automatically
* ether2 + wlan1 + wlan2 are one LAN
* LAN clients get IPs via DHCP
* DNS works for clients
* Internet access works (NAT included)

---

