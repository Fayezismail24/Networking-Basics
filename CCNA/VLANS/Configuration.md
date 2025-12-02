##  **Vlan  Configuration**


###  **Creating VLANs**

Switch> `enable`

Switch# `configure terminal`

Switch(config)# `vlan 10`

Switch(config-vlan)# `name Sales`

Switch(config-vlan)# `exit`


##  **Assign Vlan To Interaface**

Switch(config)#interface `fastEthernet 0/1`

Switch(config-if)#switchport mode `access` 

Switch(config-if)#switchport access `vlan 100`

**Assign Trunk To Interaface**
---

Switch(config)#interface `fastEthernet 0/2`

Switch(config-if)# switchport mode `trunk`

Switch(config-if)# switchport trunk `allowed vlan 10,20`

Switch(config-if)# exit



**Layer 3 Switch SVI**
---

Switch(config)# `vlan 10`

Switch(config-vlan)# `name Sales`


Switch(config)#interface `vlan 10`

S1(config-if)#ip address `192.168.10.1 255.255.255.0`














