# DTP (Dynamic Trunking Protocol)

DTP, or **Dynamic Trunking Protocol**, is a Cisco proprietary protocol used to automatically negotiate the creation of trunk links between Cisco switches. It allows switches to dynamically decide whether to establish a trunk link or not, based on their configuration.

## Key Concepts:

### 1. Trunking
- A **trunk link** is a network link that carries traffic for multiple VLANs, which is essential for communication between switches that need to support multiple VLANs over a single physical connection.
- DTP helps automate the process of setting up a trunk link between two switches.

### 2. DTP Modes
There are several DTP modes that determine how the negotiation of a trunk link takes place. These are configured on the interface level and can be set using the `switchport mode` command. The main DTP modes are:

- **Dynamic Auto**: In this mode, the switch port will attempt to become a trunk port if the device on the other side of the link is set to **Dynamic Desirable** or **Trunk** mode. It does not actively initiate trunking but can respond to requests.
  
- **Dynamic Desirable**: In this mode, the switch port actively attempts to form a trunk link by sending DTP frames to the other switch. If the other side is set to **Dynamic Auto**, the trunk link will be established.

- **Trunk**: When this mode is configured, the port is forced to be a trunk port, and it will send and receive DTP frames to negotiate trunking if the remote port supports DTP.

- **Access**: In this mode, the switch port is configured as an access port and will not attempt to form a trunk link. It is strictly for devices that belong to a single VLAN.

### 3. How DTP Works
- DTP frames are sent between switches over the link to negotiate the trunking status.
- When both switches agree on trunking parameters (such as VLANs and encapsulation type), a trunk link is established.
- If one side of the link is set to **Trunk** mode and the other side is set to **Dynamic Desirable** or **Dynamic Auto**, the trunk link will automatically be negotiated.

- # DTP (Dynamic Trunking Protocol)

DTP (Dynamic Trunking Protocol) is a Cisco proprietary protocol used to automatically negotiate trunk links between switches.

## DTP Modes Summary

| **Mode**               | **Action**                                                                                         |
|------------------------|----------------------------------------------------------------------------------------------------|
| **Dynamic Auto**        | The port will respond to trunking negotiation requests but won't initiate the process.             |
| **Dynamic Desirable**   | The port actively tries to establish a trunk link with the other switch.                           |
| **Trunk**               | Forces the port to be a trunk port, regardless of the other device's settings.                     |
| **Access**              | The port is forced into access mode and will not attempt to negotiate trunking.                    |

<img width="1280" height="149" alt="image" src="https://github.com/user-attachments/assets/8137270d-a42c-4ae5-93bf-90aa6dfe9b3c" />
<img width="1285" height="149" alt="image" src="https://github.com/user-attachments/assets/1a78d13d-96a0-4933-bd84-97abc4f31d69" />
<img width="1285" height="149" alt="image" src="https://github.com/user-attachments/assets/3a823573-de69-466f-80df-98732e6ee93e" />
<img width="1288" height="149" alt="image" src="https://github.com/user-attachments/assets/11b4364f-4091-4729-b714-daffcb18cb15" />
<img width="1283" height="150" alt="image" src="https://github.com/user-attachments/assets/8e46941a-143f-4f1d-a326-650e5df47ec5" />
<img width="1282" height="154" alt="image" src="https://github.com/user-attachments/assets/e47410d2-4fe9-4072-ac7f-af6bea7f81fd" />
<img width="1287" height="149" alt="image" src="https://github.com/user-attachments/assets/99613301-0396-4d43-8b68-7af87d798735" />
<img width="1284" height="153" alt="image" src="https://github.com/user-attachments/assets/bcd86ffe-8a62-470a-b67c-0e420e45cfc3" />
















### 4. DTP Frames
- DTP frames are sent periodically to maintain the trunk link.
- These frames contain information that helps negotiate whether the port should remain in trunk mode or switch to access mode.

### 5. Trunk Encapsulation
- DTP also helps negotiate the **trunk encapsulation** type, which determines how VLAN tags are added to frames:
  - **IEEE 802.1Q**: The most common trunking standard, which adds a VLAN tag to Ethernet frames.
  - **ISL (Inter-Switch Link)**: An older Cisco proprietary trunking protocol that adds a header and trailer to the frame to support trunking. (NOT USED ANYMORE) 

### 6. Advantages of DTP
- **Automatic Trunking**: DTP automatically establishes trunk links without requiring manual configuration, reducing human error and simplifying network management.
- **Simplified VLAN Management**: Once the trunk link is established, VLAN information can flow automatically between switches, enabling the use of multiple VLANs across a network.

### 7. Disabling DTP
If you don’t want a port to negotiate trunking (for example, to avoid unexpected trunk links), you can disable DTP using the following command on the interface:

```bash
switchport nonegotiate

