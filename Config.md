# Basic Cisco Commands for Routers and Switches

## 1. **Accessing the device**
- **Console Access**:
  - Connect using a terminal emulator (like PuTTY or Tera Term) via the console cable
  - Use the default settings (9600 baud rate, no parity, 8 data bits, 1 stop bit)

- **SSH Access**:
  - Ensure SSH is configured on the router or switch
  - Command: `ssh username@ip_address`

## 2. **Basic Commands for Router/Switch**

### 2.1. **Entering Privileged EXEC Mode**
- **Command**: `enable`

- **Purpose**: To enter privileged EXEC mode (full access)

### 2.2. **Exiting to User EXEC Mode**
- **Command**: `disable`
- **Purpose**: To exit from privileged EXEC mode to user EXEC mode

### 2.3. **View Device Configuration**
- **Command**: `R1#show running-config`
- **Purpose**: Displays the current configuration of the device

### 2.4. **Save Configuration**
- **Command**: `copy running-config startup-config`
- **Purpose**: Saves the running configuration to the startup configuration

### 2.5. **Show Interface Status**
- **Command**: `show ip interface brief`
-  **Command**: `R1#show ip interface brief`
- **Purpose**: Displays a brief overview of the device's interfaces, including their IP addresses and statuses

### 2.6. **Check Routing Table**
- **Command**: `show ip route`
- **Command**: `R1#show ip route`
- **Purpose**: Displays the routing table of the device

### 2.7. **Check ARP Table**
- **Command**: `show arp`
- **Purpose**: Displays the Address Resolution Protocol (ARP) table

### 2.8. **Check Interface Configuration**
- **Command**: `show interface gigabitEthernet 0/1`
- **Purpose**: Displays detailed information about a specific interface

### 2.9. **Clear Interface Counter**
- **Command**: `clear counters`
- **Purpose**: Resets the interface counters

### 2.10. **Set Hostname**
- **Command**: `hostname [name]`
- **Purpose**: Sets the hostname of the router/switch

### 2.11. **Set IP Address**
- **Command**: ip address  `[ip address] [subnet mask]`

-**Router(config)#** interface GigabitEthernet0/1

-**Router(config-if)#** `ip address 192.168.30.1 255.255.255.0`

-**Purpose:** `Assigns an IP address to an interface`

## 3. **Basic Commands for Router/Switch Configuration**

### 3.1. **Enter Global Configuration Mode**
- **Command**: `configure terminal`
- **Purpose**: Enters global configuration mode where you can configure the device

### 3.3. **Enable an Interface**
- **Command**: `no shutdown`
- **Purpose**: Activates the specified interface (in case it is administratively down)

### 3.4. **Disable an Interface**
  Router(config)# interface GigabitEthernet0/1
- **Command**: `shutdown`
- **Purpose**: Deactivates the specified interface (in case it is administratively up)

### 3.5. **View Interface Status**
- **Command**: `show interface [interface_name]`
- Example: `show interface GigabitEthernet0/1`
- **Purpose**: Displays detailed statistics and status of a specific interface (including errors, traffic, etc.).
