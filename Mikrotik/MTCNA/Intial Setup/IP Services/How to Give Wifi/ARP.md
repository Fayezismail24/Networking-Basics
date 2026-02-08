
# Static ARP in MikroTik RouterOS

### 1. **What is Static ARP?**
**Static ARP (Address Resolution Protocol)** is a method used to manually map an **IP address** to a **MAC address** in a network. This mapping is **fixed** and does not change unless manually updated. Static ARP is useful in situations where you want to ensure that a specific IP address always resolves to a particular MAC address.

---

### 2. **How ARP Works**
- **ARP (Address Resolution Protocol)** is used by devices in a network to map an **IP address** to a **MAC address** (hardware address) so they can communicate over the network.
- By default, ARP entries are **dynamic**, meaning the router or device automatically learns and updates the mapping between IP and MAC addresses as needed.
- **Static ARP** entries are manually configured, making them **permanent** and unchanging unless updated manually.

---

### 3. **Use Cases for Static ARP**
- **Security**: Prevent **ARP spoofing** or **ARP poisoning** attacks, where malicious devices send false ARP messages to associate a fake MAC address with a legitimate IP address.
- **Network Stability**: Ensures that important devices, such as **servers**, **gateways**, and other critical network equipment, always have consistent **IP-to-MAC mappings**.
- **Fixed Network Topology**: Ensures that devices like **printers**, **cameras**, or **switches** always have the same IP and MAC mapping, which can improve network management.

---

### 4. **How to Set Static ARP in MikroTik RouterOS**

1. **Log in to the Router** via **Winbox**, **WebFig**, or **CLI**.
   
2. **Navigate to ARP Settings**:
   - In **Winbox** or **WebFig**, go to `IP` > `ARP`.
   
3. **Add a Static ARP Entry**:
   - Click the **"Add"** button to create a new ARP entry.
   - In the fields:
     - **IP Address**: Enter the **IP address** you want to associate with a specific MAC address.
     - **MAC Address**: Enter the **MAC address** of the device you want to statically bind the IP to.
     - **Interface**: Select the interface where the device is connected (e.g., Ether1, Wi-Fi, etc.).
     - **Type**: Set the **Type** to **static** to make it a permanent entry.

4. **Command Line**:
   To add a static ARP entry using CLI, run the following command:
   ```bash
   /ip arp add address=192.168.1.100 mac-address=00:1A:2B:3C:4D:5E interface=ether1
````

* **address**: The IP address you want to bind.
* **mac-address**: The MAC address to which the IP should resolve.
* **interface**: The interface the device is connected to (e.g., Ether1, Wi-Fi).

5. **Confirm Static ARP Entry**:
   To check if the static ARP entry has been added, use:

   ```bash
   /ip arp print
   ```

---

### 5. **Benefits of Static ARP**

* **Security**: Prevents **ARP spoofing/poisoning** attacks, ensuring the integrity of IP-to-MAC mappings.
* **Stability**: Guarantees that critical network devices (e.g., servers, gateways) have a consistent and predictable IP-MAC mapping.
* **Predictability**: Reduces the chances of **IP conflicts** or miscommunication in networks with known devices.

---

### 6. **Drawbacks of Static ARP**

* **Manual Management**: Static ARP entries require manual updates if devices' MAC addresses change (e.g., after a hardware upgrade).
* **Scalability**: In large networks, managing static ARP entries can be cumbersome.
* **Lack of Flexibility**: Static ARP entries do not adjust dynamically to network topology changes.

---

### 7. **Static ARP vs Dynamic ARP**

* **Dynamic ARP**: Automatically updates the ARP table with new IP-to-MAC mappings as devices communicate on the network.
* **Static ARP**: The mapping is **fixed** and must be manually entered, offering more control over network communication.

---

### 8. **Conclusion**

Static ARP is an important tool for ensuring **stable** and **secure network communication**. By associating specific IP addresses with fixed MAC addresses, you can prevent ARP attacks and ensure critical devices are always reachable. However, static ARP can be difficult to manage in large networks due to its manual nature.

Let me know if you need help with setting up or troubleshooting static ARP on your MikroTik router!

```

This **Markdown** format should render cleanly in any Markdown editor or viewer. Let me know if you'd like further adjustments!
```

