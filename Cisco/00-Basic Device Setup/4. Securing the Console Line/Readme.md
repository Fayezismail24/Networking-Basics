The **console line** is the physical serial port used to directly manage the device.

```bash
R1(config)# line console 0
R1(config-line)# password cisco123
R1(config-line)# login
R1(config-line)# exec-timeout 5 0        ! Logout after 5 min of inactivity
R1(config-line)# logging synchronous     ! Prevents log messages from interrupting typing
R1(config-line)# exit
```

| Command | Purpose |
|---------|---------|
| `password <password>` | Sets the console password |
| `login` | Enables password checking on login |
| `exec-timeout <min> <sec>` | Auto-logout timer (0 0 = never) |
| `logging synchronous` | Keeps CLI clean from syslog interruptions |
