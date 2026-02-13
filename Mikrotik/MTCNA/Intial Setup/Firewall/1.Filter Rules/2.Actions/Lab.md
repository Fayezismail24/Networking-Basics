

# Lab: Firewall Filter Actions — DROP vs. REJECT

This lab demonstrates the practical differences between the **DROP** and **REJECT** actions within a MikroTik firewall environment.

## 1. Initial Configuration

To test these actions, we create a filter rule in the `input` chain to intercept ICMP (Ping) traffic from a specific source.

* **Chain**: `input`
* **Src. Address**: `192.168.0.21`
* **Protocol**: `1 (icmp)`

---

## 2. Testing the DROP Action

In this scenario, the firewall is configured to silently discard packets.

### Configuration

* **Action**: `drop`

* <img width="306" height="27" alt="image" src="https://github.com/user-attachments/assets/b4ed7e83-c736-431b-9987-31ae7df97ed3" />


### Result

* **Observed Behavior**: The sender receives a `Request timed out`.
* <img width="536" height="68" alt="image" src="https://github.com/user-attachments/assets/56b3a1bd-d1b2-43b8-a133-76b2c3bae444" />

* **Analysis**: The router drops the packet without any notification. The sender must wait for the full timeout duration before giving up.

---

## 3. Testing the REJECT Action

In this scenario, the firewall is configured to refuse the packet and send an explicit error message back to the source.

### Configuration

* **Action**: `reject`
* <img width="346" height="196" alt="image" src="https://github.com/user-attachments/assets/cc3b0d25-0783-4890-929d-4d1c3571814c" />

* **Reject With**: `icmp-host-unreachable`

### Result

* **Observed Behavior**: The sender immediately receives a `Reply from 192.168.0.15: Destination host unreachable`.
* <img width="667" height="83" alt="image" src="https://github.com/user-attachments/assets/c78e78eb-3f3f-4a0e-96b3-ffef58cf7ff8" />

* **Analysis**: Unlike DROP, REJECT provides instant feedback. This is useful for internal troubleshooting as it confirms the router is active but explicitly denying the request.

---

## Comparison Summary

| Feature | DROP | REJECT |
| --- | --- | --- |
| **Sender Experience** | `Request timed out` | `Destination host unreachable` |
| **Response Time** | High (waits for timeout) | Instant |
| **Visibility** | Stealthy (silent) | Informative |
