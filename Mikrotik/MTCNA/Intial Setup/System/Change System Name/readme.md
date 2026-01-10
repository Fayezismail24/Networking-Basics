
# System Identity (Router Name)

The system identity defines the router name shown in:
- WinBox
- CLI prompt
- Logs
- Neighbor discovery

---

## View current router name

```bash
/system identity print
````

---

## Change router name

```bash
/system identity set name=CORE-RTR-01
```

---

## Verify change

```bash
/system identity print
```

---

## Notes

* Router name should be unique inside the network
* Avoid spaces, use `-` or `_`
* Good naming helps with monitoring and logging





