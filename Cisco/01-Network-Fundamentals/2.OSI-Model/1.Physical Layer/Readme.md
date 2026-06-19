
## Forms of Signals

| Signal Type       | Measurement     | Medium      |
| ----------------- | --------------- | ----------- |
| Electrical Signal | Volts (V)       | Copper      |
| Light Pulses      | Wavelength (nm) | Fiber Optic |
| Microwave Signal  | Frequency (GHz) | Wi-Fi       |

---

## Link Properties

### Bandwidth

The maximum capacity of a network medium to carry data, typically measured in **Mbps** or **Gbps**.

### Throughput

The actual amount of data successfully transmitted per second.

### Goodput

The useful application data delivered to the destination, excluding protocol overhead and retransmissions.

### Latency

The time it takes for a packet to travel from the sender to the receiver, usually measured in **milliseconds (ms)**.

---

## Troubleshooting Tips

### Application feels slow?

➡️ Check **latency** first.

### Large file transfers or backups are taking too long?

➡️ Check **throughput** and **packet loss**.

### Are network links running near capacity?

➡️ Check **bandwidth utilization** and **network congestion**.

### High bandwidth but poor performance?

➡️ Investigate:

* Latency
* Routing issues
* Retransmissions
* Packet loss

### Performance drops during peak usage?

➡️ Look for:

* Bandwidth saturation
* Traffic spikes

---

## Common Troubleshooting Tools

| Metric                | Tools                                                                     |
| --------------------- | ------------------------------------------------------------------------- |
| Latency               | Ping, Traceroute, MTR                                                     |
| Throughput            | iPerf3, Speedtest                                                         |
| Bandwidth Utilization | Interface Statistics, Monitoring Platforms, Cloud-Native Monitoring Tools |
| Deep Packet Analysis  | Wireshark                                                                 |

---

## Key Takeaway

Before attempting a fix, identify **which network metric is the actual bottleneck**. Optimizing the wrong metric often wastes time and does not solve the underlying issue.
