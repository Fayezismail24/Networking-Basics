In MikroTik networking, **Torch** is a essential real-time monitoring tool used to see exactly what is happening on your interfaces at any given moment. It is primarily used for troubleshooting and verifying that your firewall and queue rules are working correctly.

---

## 🔦 How Torch Works

Think of Torch like a "live feed" for your router's ports. It breaks down traffic based on several criteria so you can identify "bandwidth hogs" or connection issues.

### Key Actions in the Tool:

* **Set Interface:** You must choose which physical or virtual port you want to monitor (e.g., `ether2-master-local`).
* **Set Filters:** You can narrow down the results by entering a specific **Src. Address** (like a laptop's IP) to see only that device's traffic.
* **Observe Traffic:** Once you click **Start**, the bottom pane displays live data, including protocols, destination addresses, and current Tx/Rx (upload/download) rates.

---

## 🔗 Connecting the Concepts

Now that we've covered **Connections**, **Queues**, and **Torch**, here is how they all fit together in a workflow:

### 1. The Connection State

The router sees a packet and identifies its state. For example, a **New** packet starts a web request. Once the server responds, it becomes **Established**.

### 2. The Simple Queue

The router checks its **Simple Queue** list. It sees that the IP `192.168.0.55` has a **Max Limit** of **3M** (3Mbps) for both upload and download. It begins throttling the **Established** connection to ensure it doesn't exceed this limit.

### 3. Verification with Torch

If the user complains that their internet is slow, you open **Torch**. You filter by their IP (`192.168.0.55`) and observe the **Tx/Rx Rate**. If you see the speed flatlining exactly at **3.0 Mbps**, you know your **Simple Queue** is working perfectly.

---

### 🛠️ Pro-Tip for Troubleshooting

> [!TIP]
> Use Torch to find **Invalid** connections. If you see a lot of traffic in Torch that doesn't have a clear destination or is using strange ports, you can use the connection states in your firewall to drop those **Invalid** packets and save CPU power.
