| **Status**     | **Meaning**                                              | **What It Tells You**                       | **Safety Level**                |             |
| -------------- | -------------------------------------------------------- | ------------------------------------------- | ------------------------------- | ----------- |
| **open**       | A service is actively listening on the port              | The application is reachable and responding | Low safety                      |             |
| **closed**     | Port is reachable but no service is listening            | Device is visible but the port is not used  | Medium safety                   |             |
| **filtered**   | Firewall or filter is blocking Nmap from seeing the port | Port is hidden and not giving info          | High safety                     |             |
| **unfiltered** | Nmap can reach the port but cannot determine its state   | Usually caused by unusual firewall behavior | Depends                         |             |
| **open         | filtered**                                               | Nmap cannot decide whether open or filtered | Common in UDP scans             | Medium–High |
| **closed       | filtered**                                               | Nmap cannot determine if closed or filtered | Happens due to ICMP rate limits | Medium–High |
