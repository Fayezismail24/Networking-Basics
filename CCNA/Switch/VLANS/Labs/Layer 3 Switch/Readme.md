# VLAN and Inter-VLAN Routing Lab

## 1. Lab Overview

This lab demonstrates VLAN segmentation and inter-VLAN routing using:

- 1 Multi-Layer Switch (L3)
- 2 Layer 2 Access Switches (S1 and S2)
- 6 PCs

The L3 switch handles routing between VLANs, and the L2 switches handle access layer switching.

---

## 2. VLAN and IP Scheme

| VLAN | Subnet | Devices |
|------|--------|---------|
| VLAN 10 | 192.168.10.0/24 | PC0, PC3 |
| VLAN 20 | 192.168.20.0/24 | PC1, PC4 |
| VLAN 30 | 192.168.30.0/24 | PC2, PC5 |

Each VLAN uses an SVI on the L3 switch as its gateway.

---

## 3. Device Roles

### **Multi-Layer Switch (L3)**
- Provides gateway IPs for VLANs.
- Performs routing between VLAN 10, 20, and 30.
- Connected to both L2 switches using trunk links.
- IP routing is enabled.

### **Layer 2 Switches (S1 and S2)**
- Forward traffic within VLANs.
- Provide access ports for PCs.
- Uplink to the L3 switch using trunk ports.

### **PCs**
Each PC has:
- A static IP based on its VLAN subnet.
- A default gateway matching its VLAN SVI.
- An access port on the correct VLAN.

---

## 4. Expected Behavior

- PCs in the same VLAN communicate directly.
- PCs in different VLANs communicate through the L3 switch.
- All six PCs should be able to ping each other.

---

## 5. Lab Objectives

- Understand VLAN segmentation.
- Practice assigning access and trunk ports.
- Learn how Layer 3 switching enables routing between VLANs.
- Verify successful end-to-end connectivity.


