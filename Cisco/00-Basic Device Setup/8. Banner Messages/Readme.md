### Types of Banners

| Banner Type | When It Appears |
|-------------|----------------|
| `banner motd` | Message of the Day – shown to **everyone** before login |
| `banner login` | Shown **after** MOTD, just before the login prompt |
| `banner exec` | Shown after a user **successfully logs in** |

### Syntax

Use a **delimiter character** (any character not in the message) to start and end the banner.

```bash
R1(config)# banner motd #
******************************************
*  AUTHORIZED ACCESS ONLY               *
*  Unauthorized access is prohibited.   *
*  All activity is monitored and logged.*
******************************************
#
```

```bash
R1(config)# banner login $
Please enter your credentials to continue.
$
```

```bash
R1(config)# banner exec ^
Welcome, Admin. You are now in privileged mode.
^
```

> ⚠️ **Legal Note:** Always use a warning banner in production. Never use welcoming language like "Welcome!" in MOTD — it can be used against you legally if unauthorized access occurs.

---
