# 🔌 Ethernet Cabling — Straight-Through vs Crossover

> Understanding **when** to use each cable type based on device TX/RX pin behavior.  
> CCNA 200-301 — Domain: Network Fundamentals

---

## 📁 Contents

| File | Topic |
|------|-------|
| [01-Pin-Overview.md](01-Pin-Overview.md) | TX/RX Pin Reference (pins 1, 2, 3, 6) |
| [02-Straight-Through.md](02-Straight-Through.md) | Straight-Through Cable — PC ↔ Switch, Router ↔ Switch |
| [03-Crossover.md](03-Crossover.md) | Crossover Cable — PC ↔ PC, Switch ↔ Switch, Router ↔ Router |
| [04-Quick-Reference.md](04-Quick-Reference.md) | Full reference table + memory trick + exam note |

---

## 🧠 Core Logic

The rule is simple:

- **Different device types** → TX of one naturally feeds RX of the other → **Straight-Through**
- **Same device types** → Both TX on the same pins → pins clash → **Crossover required**

---

## 📌 Pin Summary

```
Device    TX Pins    RX Pins
────────────────────────────
PC        1, 2       3, 6
Router    1, 2       3, 6
Switch    3, 6       1, 2
```

> **PCs and Routers share identical pin behavior.**  
> **Switches are the mirror opposite.**

---

## ⚠️ Real-World Note

Modern switches and NICs support **Auto-MDI/MDIX** — they automatically detect and correct pin polarity, making crossover cables optional in most production environments.

However, **CCNA expects you to know this logic cold** — the exam tests the underlying behavior without Auto-MDI/MDIX.
