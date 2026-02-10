
## 📡 MikroTik Frequency Mode Detailed

| Mode | Description | Use Case / Notes | Risks / Special Info |
|------|------------|-----------------|--------------------|
| **Regulatory** | Auto-selects only frequencies **allowed by the country/regulatory domain**. | Default and recommended mode. AP or client automatically follows country rules (channels, TX power, DFS). | Safe, legal, avoids radar interference. Cannot use channels outside country limits. |
| **Manual Tx Power** | You **manually select a frequency/channel** and can adjust TX power. | Useful for **point-to-point links**, avoiding interference, or crowded areas. Gives more control for optimization. | Must ensure frequency is allowed by country rules. Wrong settings can cause interference or poor connection. |
| **Superchannel** | Lets you use **any frequency**, even outside regulatory limits (ignores country rules). | Lab/testing environments, special RF setups, experimenting with restricted channels. | Illegal in most countries. Can interfere with radar, emergency systems. Not for production. |

---

### 🔑 Additional Notes for MTCNA Exam

1. **Regulatory Mode**
   - Always safe for exams unless the question says otherwise.
   - Automatically handles DFS and CAC timing.
   - Usually used in wireless AP deployment.

2. **Manual Tx Power Mode**
   - Allows precise **channel selection** and **power adjustment**.
   - Frequently used in **point-to-point wireless links** to optimize range and performance.
   - Can be combined with **specific frequency width** (20/40/80 MHz) to control throughput.


``
###  Superchannel

The **Superchannel** feature in MikroTik RouterOS extends the wireless frequency range beyond standard regulatory limits, allowing for **channel bonding** and **higher throughput**. It enables MikroTik devices to use **unused frequencies** and **wider channel widths** (e.g., 40 MHz, 80 MHz, 160 MHz) for improved performance, especially in **long-distance wireless links** or **high-density environments**.

#### Key points:
- **Frequency Range Extension**: Operate on frequencies outside the typical regulatory domain.
- **Channel Aggregation**: Combine multiple channels for increased bandwidth.
- **Dynamic Frequency Usage**: Select non-overlapping frequencies for better performance.
- **Regulatory Compliance**: Ensure compliance with local laws before enabling.
- **Supported Devices**: Available on compatible MikroTik wireless devices (e.g., RouterBOARD, SXTsq).
  
Make sure to check compatibility and local regulations before enabling the Superchannel feature.


---

### 🧠 Quick Exam Memory Trick

- Regulatory → Auto, safe, legal  
- Manual Tx Power → You choose frequency and power  
- Superchannel → Ignore rules, risky, test/lab only  



