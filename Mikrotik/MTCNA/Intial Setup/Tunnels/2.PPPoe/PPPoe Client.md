# PPPoE Client Configuration on MikroTik (Client Side)

To configure a **PPPoE client** on a MikroTik router, follow these mandatory steps:

## 1. Navigate to PPP Section
- Go to **PPP** in the left menu of your MikroTik 

## 2. Add a New PPPoE Client
- Click the **"+"** button and select **PPPoE Client** to create a new PPPoE client interface.

## 3. Configure Basic PPPoE Client Settings
In the configuration window for the **PPPoE Client**, configure the following fields:

### Mandatory Fields:

- **Name**:  
  - Choose a name for the PPPoE interface (e.g., `PPPoE-client`).
  
- **Interface**:  
  - Choose the **physical interface** (Ethernet port) connected to the **PPPoE server** (usually the interface connected to the **internet** or **modem**, e.g., `ether1`, `ether2`, etc.).

- **Service Name**:  
  - This is **optional**. If the ISP requires a specific **service name**, enter it here. Otherwise,

- **Username**:  
  - Enter the **username** provided by your ISP for the PPPoE connection.

- **Password**:  
  - Enter the **password** associated with the provided **username**.
 
  - <img width="757" height="547" alt="image" src="https://github.com/user-attachments/assets/31d8f7c6-9d0d-4ab5-9d44-e70f0e243fec" />


### Optional but Important:

- **AC Name**:  
  - The **Access Concentrator Name** is **optional**. If your ISP provides it, enter it here; otherwise, leave it blank.

- **Profile**:  
  - Select a **PPPoE profile**. The default profile is usually fine, but you can customize the profile under **PPP > Profiles** if you need specific encryption or compression settings.

## 4. Optional Settings (Important for Routing & DNS)

- **Add Default Route**:  
  - **Enable this** to automatically add a default route to the router’s routing table when the PPPoE client connects. This is necessary for routing internet traffic through the PPPoE connection.

- **Use Peer DNS**:  
  - **Enable this** to allow the router to automatically use the DNS servers provided by the PPPoE server (usually provided by your ISP).

- **Dial on Demand**:  
  - **Enable this** if you want the PPPoE connection to dial and connect automatically when traffic is detected (useful for dial-up connections).

## 5. Configure Keepalive Timeout
- **Keepalive Timeout** is set to **60 seconds** by default. This defines how often the router checks for a valid PPPoE connection. You can adjust this value, but **60 seconds** is usually sufficient.

## 6. Enable and Apply
- After filling in the mandatory fields and any optional settings, click **Apply** and then **OK** to save the configuration.

## 7. Check PPPoE Status
- Go to **PPP** > **Interfaces**.
- The **PPPoE-client** interface should show up in the list. Once connected, it should show a **"Connected"** status.
- If the status is **"Disconnected"**, check the logs for any errors or verify your credentials.

## 8. Test Connectivity
- To verify the connection, go to **New Terminal** and use the **ping** command to check if you have internet access:
  ```bash
  ping 8.8.8.8

This pings Google's DNS (8.8.8.8) to confirm that the router has internet access.

## Example Configuration via Command Line

Here’s an example of how you would configure the PPPoE client via the MikroTik terminal:

```bash
/interface pppoe-client add name=PPPoE-client interface=ether1 user=your-username password=your-password add-default-route=yes use-peer-dns=yes
```

### Summary of Mandatory Configuration Fields:

1. **Name**: Assign a name for the PPPoE client interface.
2. **Interface**: Select the correct interface connected to the ISP's PPPoE server.
3. **Username**: Enter the PPPoE username provided by your ISP.
4. **Password**: Enter the corresponding password.
5. **Service Name**: (Optional) Enter if the ISP requires it.
6. **Add Default Route**: Enable to ensure proper routing of traffic.
7. **Use Peer DNS**: Enable to use DNS settings from the PPPoE server.

These steps ensure that the PPPoE client can successfully connect to the ISP and allow the router to route internet traffic.

Let me know if you need more details or clarification!

```

This Markdown format provides a detailed, easy-to-follow guide on configuring the **PPPoE client** on your MikroTik router. Let me know if you need any further help!
```

