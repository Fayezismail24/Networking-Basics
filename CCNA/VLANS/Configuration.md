##  **Vlan  Configuration**


###  **Creating VLANs**
---


Switch(config)# `vlan 10`

Switch(config-vlan)# `name Sales`

Switch(config-vlan)# `exit`


##  **Assign Vlan To Interaface**
---

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

MLS(config)# `vlan 10`

MLS(config-vlan)# `name Sales`


MLS(config)#interface `vlan 10`

MLS(config-if)#ip address `192.168.10.1 255.255.255.0`

MLS(config)# `ip routing`




**Router on a Stick**
---

Router(config)#interface `gigabitEthernet 0/1`

Router(config-subif)`no shutdown`

Router(config)#interface gigabitEthernet `0/1.10`

Router(config-subif)`#encapsulation dot1Q 10`

Router(config-subif)#ip address `192.168.1.1 255.255.255.0`
















