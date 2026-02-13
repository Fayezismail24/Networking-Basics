<img width="1489" height="518" alt="image" src="https://github.com/user-attachments/assets/fe4a4a77-8117-4c3d-90e3-ce6f135bc5c3" />


##  Lab Task: Port Forwarding to the Web Server (R2)

In this scenario, we want to allow devices from external networks (like the PC connected to **R3**) to reach the Internal Server (`192.168.0.10`) by targeting the interface of **R2**.

### Network Topology Context

* **Target Server**: `192.168.0.10`
* **R2 Entry IP**: `10.128.100.131` (The address on the link between R1 and R2)

### Configuration for R2 (Markdown)

### Destination NAT Configuration on R2

To map traffic from the backbone network to the internal server, we apply a `dstnat` rule on router **R2**.

#### 1. General Tab
* **Chain**: `dstnat`
* **Dst. Address**: `10.128.100.131` 
    *(This is the IP external traffic hits when trying to reach the server).*

  <img width="509" height="235" alt="image" src="https://github.com/user-attachments/assets/a9ad66f1-4052-447c-8327-60d89f16ac3e" />


#### 2. Action Tab
* **Action**: `dst-nat`
* **To Addresses**: `192.168.0.10`
    *(This is the private IP of the server where the traffic is ultimately sent).*
  <img width="478" height="534" alt="image" src="https://github.com/user-attachments/assets/d668379c-22a6-43aa-ade5-f329119bc9b7" />


### How it Works:
1. A packet arrives at **R2** from **R1** with a destination of `10.128.100.131`.
2. The router recognizes the `dstnat` rule.
3. It "translates" the destination address to `192.168.0.10`.
4. The packet is then routed locally to the server.



By using the **Dst. Address** of `10.128.100.131`, you are specifically telling R2 to only forward traffic that was intended for that specific interface. This is more precise than just selecting an `In-Interface`, as it ensures the traffic was correctly addressed to the gateway.

