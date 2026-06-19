Boss, **CSMA/CD** absolutely belongs in a Data Link Layer repository because it's a Layer 2 media access method.

You can add a section like this:

## CSMA/CD (Carrier Sense Multiple Access with Collision Detection)

CSMA/CD is a media access control method used in **half-duplex Ethernet networks** to manage how devices share a common transmission medium.

### How CSMA/CD Works

1. **Carrier Sense**: A device listens to the network before transmitting.
2. **Multiple Access**: Multiple devices can use the same network medium.
3. **Collision Detection**: If two devices transmit simultaneously, a collision occurs.
4. **Jam Signal**: The devices send a jam signal to notify others of the collision.
5. **Backoff**: Each device waits a random amount of time before attempting to retransmit.

### Example

```text
PC A ----- Hub ----- PC B

PC A transmits
PC B transmits at the same time
↓
Collision occurs
↓
Both devices stop and retry later
```

### Where is CSMA/CD Used?

* Legacy Ethernet hubs
* Half-duplex Ethernet networks

### Where is CSMA/CD NOT Used?

* Modern switched Ethernet networks
* Full-duplex Ethernet connections

In modern Ethernet, switches provide dedicated collision domains, eliminating collisions and making CSMA/CD unnecessary.

### CSMA/CD vs CSMA/CA

| Feature            | CSMA/CD                  | CSMA/CA               |
| ------------------ | ------------------------ | --------------------- |
| Full Name          | Collision Detection      | Collision Avoidance   |
| Used In            | Ethernet (legacy)        | Wi-Fi                 |
| Handles Collisions | Detects after they occur | Tries to prevent them |
| Common Today       | Rare                     | Very common           |

**CCNA exam tip:** Know that **CSMA/CD is associated with old hub-based Ethernet networks**, while **Wi-Fi uses CSMA/CA** because wireless devices cannot reliably detect collisions while transmitting.
