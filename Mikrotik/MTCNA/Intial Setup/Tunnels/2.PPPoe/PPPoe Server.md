
# Setting Up a PPPoE Server on MikroTik Router

This guide walks you through the steps to set up a **PPPoE server** on a MikroTik router, allowing you to provide PPPoE access to clients.

## 1. Log in to Your MikroTik Router
- Access the MikroTik router using **Winbox**, **WebFig**, or **SSH**.

## 2. Navigate to the PPP Section
- Once logged in, click on **PPP** in the left-hand menu.
- This will open the **PPP configuration** window, where you can manage PPPoE settings.

## 3. Create a PPPoE Server
- In the **PPP** section, click on **PPPoE Servers** (or **PPPoE Servers** tab).
- Click the **"+"** button to add a new PPPoE server.
<img width="1178" height="774" alt="image" src="https://github.com/user-attachments/assets/e16839cd-2fcc-454a-97d2-4a4d115f76a0" />


## 4. Configure PPPoE Server Settings
- **Interface**:  
  - Select the **interface** that will handle the PPPoE connections (typically connected to your LAN or gateway).
  - <img width="528" height="283" alt="image" src="https://github.com/user-attachments/assets/d52e8af1-50f0-4698-9057-692718db414f" />

- **Service Name**:  
  - **Optional**: If required, enter a **service name** for the PPPoE service (e.g., `internet-service`).
- **AC Name** (Access Concentrator Name):  
  - **Optional**: Enter a name for the **Access Concentrator**.
- **Max MTU (Maximum Transmission Unit)**:  
  - Set to **1480** (default) unless a different value is required by your setup.

## 5. Configure PPPoE Secrets (User Credentials)
- Go to **Secrets** tab in the **PPP** section.
- Click the **"+"** button to add a new PPPoE user.
  - **Name**: Enter the **username** for the client.
  - **Password**: Enter the **password** for the client.
  - **Service**: Select the **PPPoE service** this user will connect to.
  - **Profile**: Choose a **profile** (you can use the default profile or create a custom one in **PPP > Profiles**).
<img width="565" height="603" alt="image" src="https://github.com/user-attachments/assets/ab69db9a-e381-433f-8f36-8653eba8e9aa" />


## 6. Assign IP Pool (Optional but Recommended)
- Go to **IP > Pool** and create a new IP address pool that will be assigned to PPPoE clients.
  - For example, create a pool from **192.168.1.100** to **192.168.1.200**.
- Link this pool to the **PPPoE profile** under **PPP > Profiles**.

## 7. Configure NAT (Network Address Translation)
- If PPPoE clients need to access the internet, you will need to configure **NAT**:
  - Go to **IP > Firewall > NAT** and add a new rule.
  - Set **Chain** to `srcnat`, **Out. Interface** to the **internet-facing interface** (e.g., `ether1`).
  - Under **Action**, select **masquerade** to allow the clients to share the internet connection.
  
### Example NAT Rule:
```bash
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade
````

## 8. Configure PPPoE Server Profile (Optional)

* Go to **PPP > Profiles** and create or modify a **profile** for your PPPoE server.

  * Set the **local address** (router’s IP).
  * Set the **remote address** (use the IP pool for clients).
  * Adjust **rate limits** if necessary (e.g., download/upload speed limits).

## 9. Enable and Apply the Configuration

* After completing the configuration, ensure that the PPPoE server is **enabled** and **applied**.
* Your PPPoE clients can now connect using the **username** and **password** you configured in the **Secrets** section.

## 10. Test the PPPoE Server

* Connect a device or router as a PPPoE client, using the **username** and **password** from the **Secrets** section.
* The device should authenticate and receive an IP address from the pool.
* Check the **PPP > Active Connections** to verify the client is connected.

---

### Example Configuration via MikroTik Terminal:

Here’s a sample set of terminal commands to set up the PPPoE server:

```bash
# Create PPPoE server on the LAN interface
/interface pppoe-server server add service-name=PPPoE-Service interface=ether2 max-mtu=1480 max-mru=1480

# Create PPPoE user (secret)
/ppp secret add name="client1" password="password123" service=PPPoE-Service profile=default remote-address=192.168.1.100

# Create IP pool for PPPoE clients
/ip pool add name=pppoe-pool ranges=192.168.1.100-192.168.1.200

# Create NAT rule for internet access
/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade
```

---

### Summary:

* Set up the **PPPoE server** by selecting the correct **interface**, creating user **Secrets**, assigning an **IP pool**, and enabling **NAT** for internet access.
* The **PPPoE clients** will connect using the **username** and **password** configured under **Secrets**.
* Optionally, configure **profiles** to define IP addresses, rate limits, and other settings.

This Markdown format should give you a clear, step-by-step guide for setting up a **PPPoE server** on your MikroTik router. Let me know if you have any questions!
`
