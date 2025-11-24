# Network Configuration Guide: VLANs and Router-on-a-Stick (RoS)

## Overview

This document outlines the configuration steps required for setting up VLANs on a Cisco switch, assigning VLANs to access ports, and configuring inter-VLAN routing on a Cisco router using Router-on-a-Stick (RoS). This configuration will allow communication between devices on different VLANs by utilizing subinterfaces on the router. It includes the following key steps:

1. **Creating VLANs** on the switch
2. **Assigning VLANs to access ports** on the switch
3. **Configuring a trunk link** between the switch and router
4. **Creating subinterfaces on the router** to enable inter-VLAN routing

The resulting configuration will enable communication between devices on different VLANs by routing traffic through the router

<img width="1050" height="791" alt="image" src="https://github.com/user-attachments/assets/238f46c2-3323-4771-b0e6-d7963f0b9817" />

