## Practical Configuration Checklist

- [ ] Plan VLAN design (IDs, names, purpose)
- [ ] Create all VLANs with descriptive names
- [ ] Configure access ports for each VLAN (use ranges)
- [ ] Configure trunk to router or other switch
- [ ] Set native VLAN on trunk (avoid VLAN 1)
- [ ] Filter allowed VLANs on trunk (if needed)

- [ ] Test connectivity:
  - [ ] Within VLAN: `ping` between hosts
  - [ ] Across VLAN: Requires Layer 3 routing

- [ ] Document port assignments in running-config backup
- [ ] Copy running-config to startup-config:
