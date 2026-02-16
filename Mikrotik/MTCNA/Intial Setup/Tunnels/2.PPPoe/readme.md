# PPPoE (Point-to-Point Protocol over Ethernet)

## What is PPPoE?
**PPPoE (Point-to-Point Protocol over Ethernet)** is a **Layer 2 protocol** used primarily for **accessing the internet** over **Ethernet networks**. It combines the **Point-to-Point Protocol (PPP)** with **Ethernet**, allowing ISPs to control access to the network and authenticate users.

## Key Features of PPPoE:
- **Authentication**: 
  - PPPoE supports **PAP (Password Authentication Protocol)** and **CHAP (Challenge Handshake Authentication Protocol)** to verify the identity of the user.
  
- **Encryption**:
  - Although PPPoE itself doesn't provide encryption, the **PPP** part can be configured with **encryption** options such as **MPPE (Microsoft Point-to-Point Encryption)** to ensure secure transmission of data.
  
- **Compression**:
  - PPPoE can support **compression techniques**, such as **MPPC (Microsoft Point-to-Point Compression)**, to reduce data sizes and improve transmission efficiency.

## PPPoE and IP Address Assignment:
- PPPoE is used to dynamically **assign IP addresses** to users. When a user connects, the **ISP assigns an IP address** dynamically to the client.
- This approach allows the ISP to **manage IP address space efficiently** by leasing IP addresses to users as needed.

## Common Uses of PPPoE:
- **DSL and Fiber Optic Internet Connections**: PPPoE is commonly used for **DSL (Digital Subscriber Line)** and **fiber optic** connections, enabling the ISP to authenticate users and assign IP addresses.
- **Residential and Small Business Access**: Many home and small business internet connections use PPPoE for cost-effective connectivity and easy management by the ISP.

## How PPPoE Works:
1. **Establishing the Connection**: The user device (e.g., router or computer) sends a PPPoE discovery packet to locate the PPPoE server. The server responds with a unique session ID.
2. **Authentication and Session Establishment**: Once the session ID is established, the client authenticates using the credentials provided by the ISP (username and password).
3. **Data Transmission**: After authentication, the connection is established, and data can be transmitted. The ISP assigns an IP address to the client, either dynamically or statically.

## PPPoE in RouterOS:
- **RouterOS**, developed by MikroTik, supports PPPoE configurations, allowing administrators to create PPPoE servers and manage client connections.
- It also supports **PPPoE client functionality**, enabling devices to connect to PPPoE-based ISPs and configure settings like authentication, encryption, and IP assignment.
```
