# Legacy Inter-VLAN Routing Setup

## Overview
This repository contains a basic configuration for **Inter-VLAN Routing** using the **Router-on-a-Stick** method. The configuration facilitates routing between two VLANs (VLAN 10 and VLAN 20) through a single physical interface on a router. The setup demonstrates a typical small network scenario where multiple VLANs are configured on a switch, and routing is provided by a router using subinterfaces.

## Network Diagram


### Devices Used:
- **Router (Router0)**: Performs the inter-VLAN routing via Router-on-a-Stick configuration
- **Switch (Switch0)**: Switch configured with multiple VLANs
- **PC0**: A computer in VLAN 10 (IP: 192.168.1.1/24)
- **PC1**: A computer in VLAN 20 (IP: 192.168.2.1/24)

## VLANs Configuration
- **VLAN 10**: Assigned to PC0 with subnet `192.168.1.0/24`
- **VLAN 20**: Assigned to PC1 with subnet `192.168.2.0/24`

## Router-on-a-Stick Configuration

The router uses a single physical interface (`GigabitEthernet0/1`) to route between the two VLANs. Subinterfaces are configured for each VLAN as follows:

1. **Router Configuration**:

    - Create subinterfaces for each VLAN:
      ```bash
      interface GigabitEthernet0/1.10
       encapsulation dot1Q 10
       ip address 192.168.1.254 255.255.255.0
       
      interface GigabitEthernet0/1.20
       encapsulation dot1Q 20
       ip address 192.168.2.254 255.255.255.0
      ```

2. **Switch Configuration**:

    - Configure VLANs on the switch:
      ```bash
      vlan 10
       name HR
      vlan 20
       name IT
      ```

    - Configure the trunk port on the switch:
      ```bash
      interface GigabitEthernet0/1
       switchport mode trunk
       switchport trunk encapsulation dot1Q
      ```

3. **PC Configuration**:

    - **PC0** (VLAN 10):
      - IP Address: `192.168.1.1/24`
      - Default Gateway: `192.168.1.254`

    - **PC1** (VLAN 20):
      - IP Address: `192.168.2.1/24`
      - Default Gateway: `192.168.2.254`

## Verification

1. **Ping Test**:
    - From **PC0**, ping **PC1** (192.168.2.1)
    - From **PC1**, ping **PC0** (192.168.1.1)
   
2. **Show Commands**:
    - On the router, verify the subinterface configurations:
      ```bash
      show ip interface brief
      ```

    - On the switch, verify VLANs and trunking:
      ```bash
      show vlan brief
      show interfaces trunk
      ```

## Conclusion
This setup demonstrates basic **Router-on-a-Stick** routing between two VLANs, which allows devices in different VLANs to communicate. This configuration is ideal for small to medium-sized networks where a dedicated Layer 3 switch is not available

## License
This project is for **educational purposes** only. It serves as a personal reference for revisiting CCNA topics when needed
