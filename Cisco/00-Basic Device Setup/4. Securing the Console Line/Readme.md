When you initially connect to a device, you are in user EXEC mode

This mode is secured using the console

To secure user EXEC mode access, enter line console configuration mode using the line console 0 global configuration command, as shown in the example

The zero is used to represent the first (and in most cases the only) console interface. Next, specify the user EXEC mode password using the password password command. Finally, enable user EXEC access using the login command

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



<img width="467" height="462" alt="Screenshot 2026-06-14 154144" src="https://github.com/user-attachments/assets/0f922d73-38ca-432f-b558-e1d33148844a" />
