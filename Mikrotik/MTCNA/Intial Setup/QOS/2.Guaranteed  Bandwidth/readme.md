
# Limit At in MikroTik Simple Queue

In MikroTik's **Sile Queue** configuration, the **Limit At** field is used to define the **guaranteed minimum bandwidth** for the queue. Here's a breakdown of its usage:

## Limit At Fields
<img width="829" height="475" alt="image" src="https://github.com/user-attachments/assets/1771d680-1caf-4d56-bd75-60e34664d6cd" />


1. **Target Upload (Limit At - Upload):**
   - This field defines the **minimum upload speed** that will be allocated to the queue. It sets the **guaranteed upload rate** for the traffic controlled by this queue. 
   - Example: If you set the **Limit At** upload to `2 Mbps`, the queue will always guarantee at least `2 Mbps` of upload bandwidth. If the network is not congested, the queue can use more bandwidth, but it will never fall below this limit.

2. **Target Download (Limit At - Download):**
   - This field works similarly but for **download traffic**. It defines the **minimum download speed** that will be guaranteed for the traffic controlled by the queue.
   - Example: If you set the **Limit At** download to `10 Mbps`, the queue will always guarantee at least `10 Mbps` of download bandwidth. If the network is not congested, the queue can use more bandwidth, but it will never fall below this limit.

## How Limit At Works

- The **Limit At** value ensures that a **specific amount of bandwidth is always allocated** to the queue, regardless of the overall network traffic or congestion.
- It **guarantees** that the queue will **not fall below the specified upload or download limits**.

   - If there is **low network traffic**, the Simple Queue can use **more bandwidth** than the **Limit At** value, but the **Limit At** ensures that this **minimum bandwidth** is always available.
   - If the network becomes congested or other queues require bandwidth, the **Limit At** value ensures that this queue gets at least the specified amount.

## Example Use Case

Let’s say you want to guarantee at least `2 Mbps` upload and `10 Mbps` download to a specific user on your network:

- **Limit At - Upload**: Set to `2 Mbps` (this ensures that the user gets at least 2 Mbps upload speed).
- **Limit At - Download**: Set to `10 Mbps` (this ensures that the user gets at least 10 Mbps download speed).

Even during times of network congestion, this user will always receive at least `2 Mbps` upload and `10 Mbps` download, as long as the network allows.

## Difference Between Limit At and Max Limit

- **Limit At** guarantees a **minimum speed**, whereas **Max Limit** sets a **maximum speed**.
- Example: A **Max Limit** of `10 Mbps` and a **Limit At** of `2 Mbps` means the user will always get **at least 2 Mbps** but can potentially use up to `10 Mbps` depending on network conditions.

## Summary

- **Limit At** is used to ensure that a queue always has access to a certain **minimum bandwidth**, ensuring that critical traffic (like VoIP or streaming) gets sufficient resources regardless of network load.




<img width="1035" height="453" alt="image" src="https://github.com/user-attachments/assets/183d3a11-4559-4859-9fa3-b7fe5f87c041" />

