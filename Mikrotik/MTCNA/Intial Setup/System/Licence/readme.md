<img width="859" height="395" alt="image" src="https://github.com/user-attachments/assets/0140b17e-3d24-4556-bed5-4cf624048b12" />




# MikroTik RouterOS License Overview

**RouterOS licensing** refers to the system MikroTik uses to manage the features, capabilities, and performance of their devices based on the license level. Each MikroTik router runs **RouterOS**, and the license defines the available functionalities on the device.

## 1. License Levels
MikroTik offers different **license levels** depending on the hardware and features required. These license levels determine:
- **Router features** (e.g., supported interfaces, VPN, etc.)
- **Hardware limits** (e.g., throughput, number of users, etc.)
- **Allowed features** (e.g., hotspot functionality, VLAN, routing protocols).

The most common RouterOS license levels are:

| License Level | Features | Use Case |
|----------------|----------|----------|
| **Level 1** | Basic features, limited interfaces and speed | Small home or office routers |
| **Level 3** | More advanced features, supports basic routing and VPN | Small to medium-sized businesses |
| **Level 5** | Full feature set, including advanced routing protocols and high throughput | Business or enterprise-level setups |
| **Level 6** | Maximum capacity for large networks, full enterprise features | High-performance environments |

### Key Features by License Level:
- **Level 1**: Limited routing features and few interfaces.
- **Level 3**: More advanced routing protocols, VPN support.
- **Level 5**: Full routing features, support for large networks, complex configurations.
- **Level 6**: High-performance features for enterprise-level use.

## 2. How License Levels Affect Devices
Each MikroTik router has a specific license tied to its hardware, which determines:
- **Number of interfaces**: The router can support a certain number of Ethernet ports, wireless interfaces, etc.
- **Maximum throughput**: Higher license levels allow higher-speed connections.
- **Advanced features**: Support for complex routing, VPNs, and more.

## 3. License Upgrades
You can **upgrade your license** if you need additional features:
- **Upgrading** involves purchasing a higher license and applying it to your device.
- You may need to upgrade as your network expands or if you require more advanced functionality.

## 4. How to View Your License
To check your current license:
- **Winbox**: Go to **System** > **License**.
- **WebFig**: Go to **System** > **License**.
- **CLI**:
  ```bash
  /system license print

This will show your current RouterOS license level and features.

## 5. Backup and Restore

You can back up your license configuration:

* Backup files can be used to restore the exact configuration, including the license, in case of failure or migration to another device.

## 6. License Activation

* When you first set up a MikroTik device, the license is typically pre-installed.
* You can manually activate or transfer licenses if needed, by entering the license key provided.

## 7. License Limitations

* **Device-Specific**: The license is tied to the device's **MAC address** and cannot be transferred easily between devices.
* **No Downgrades**: Once a license is upgraded, it cannot be reverted to a lower level.

## 8. License Purchase

MikroTik licenses can be purchased:

* From **authorized resellers**.
* Directly from **MikroTik's website**.
* After purchasing, you receive a license key which you can apply to your router.

## Conclusion

RouterOS licensing is essential for determining the capabilities of your MikroTik router. Based on your needs, you can choose the appropriate license level and upgrade as your network requirements grow.

```

This is the corrected version of the RouterOS licensing explanation in **Markdown** format. It should now render properly in any Markdown viewer. Let me know if you need any further adjustments!
```
