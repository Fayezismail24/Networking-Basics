##  1.**Vlan  Configuration**


###  **Creating VLANs**

Switch> `enable`

Switch# `configure terminal`

Switch(config)# `vlan 10`

Switch(config-vlan)# `name Sales`

Switch(config-vlan)# `exit`

Switch(config)#interface `fastEthernet 0/1`

Switch(config-if)#switchport mode `access` 

Switch(config-if)#switchport access `vlan 100`









