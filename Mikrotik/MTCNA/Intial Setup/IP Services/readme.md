### Routing Behavior Explanation

If there are two or more routes pointing to the same network, the router will always choose the smallest subnet. 

For example:

- **Destination**: 192.168.90.0/24, **Gateway**: 1.2.3.4
- **Destination**: 192.168.90.128/25, **Gateway**: 5.6.7.8

In this case, the router will choose the route for **192.168.90.128/25** (with the gateway 5.6.7.8) since it is the more specific (smaller) subnet.

### Packet Sent to: 192.168.90.135

Since 192.168.90.135 falls within the **192.168.90.128/25** range (192.168.90.128 to 192.168.90.255), the router will send the packet to **Gateway 5.6.7.8**.
