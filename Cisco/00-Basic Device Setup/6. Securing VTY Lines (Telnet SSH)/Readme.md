VTY lines handle remote access (Telnet/SSH). There are typically 16 lines (0–15).

### Telnet (less secure)

```bash
R1(config)# line vty 0 15
R1(config-line)# password cisco123
R1(config-line)# login
R1(config-line)# exec-timeout 10 0
R1(config-line)# exit
```

### SSH (recommended over Telnet)

SSH encrypts the session. To enable SSH:

```bash
! Step 1 – Set a domain name (required for key generation)
R1(config)# ip domain-name example.com

! Step 2 – Generate RSA keys (minimum 1024 bits, 2048 recommended)
R1(config)# crypto key generate rsa modulus 2048

! Step 3 – Create a local user
R1(config)# username admin secret Str0ng@Pass!

! Step 4 – Configure VTY to use SSH and local login
R1(config)# line vty 0 15
R1(config-line)# transport input ssh        ! Allow SSH only (blocks Telnet)
R1(config-line)# login local               ! Use local username/password database
R1(config-line)# exec-timeout 10 0
R1(config-line)# exit

! Step 5 – Enforce SSH version 2
R1(config)# ip ssh version 2
```

---


https://www.youtube.com/watch?v=BdP1h-trq_Y
