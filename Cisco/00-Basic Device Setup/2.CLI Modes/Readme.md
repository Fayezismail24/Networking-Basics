### CLI Modes
 Mode | Prompt | How to Enter |
|------|--------|-------------|
| User EXEC | `Router>` | Default on login |
| Privileged EXEC | `Router#` | `enable` |
| Global Configuration | `Router(config)#` | `configure terminal` |
| Interface Config | `Router(config-if)#` | `interface <type> <number>` |
| Line Config | `Router(config-line)#` | `line console 0` / `line vty 0 4` |

### Navigating Modes

```bash
Router> enable                   # Enter Privileged EXEC
Router# configure terminal       # Enter Global Config
Router(config)# exit             # Go back one level
Router(config)# end              # Go directly back to Privileged EXEC
Router# disable                  # Return to User EXEC
```

---
