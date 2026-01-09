
## All Valid MikroTik CLI Combinations (Same Result)

All of the following commands do **exactly the same thing**:
they add `192.168.0.1/24` to the `bridge` interface.

---

### 1️⃣ Absolute path (most common, documentation style)

```bash
/ip address add address=192.168.0.1/24 interface=bridge
```

---

### 2️⃣ Relative path with explicit root action (your preferred style)

```bash
ip address /add address=192.168.0.1/24 interface=bridge
```

---

### 3️⃣ Inside the menu (menu-first style)

```bash
/ip address
add address=192.168.0.1/24 interface=bridge
```

---

### 4️⃣ Deep relative (only works if you are already in `/ip`)

```bash
address add address=192.168.0.1/24 interface=bridge
```

---

### 5️⃣ Fully relative (only works if you are already in `/ip address`)

```bash
add address=192.168.0.1/24 interface=bridge
```

---

## What does NOT work (important)

❌ Missing space before `/add`

```bash
ip address/add ...
```

❌ Extra spaces around `=`

```bash
address =192.168.0.1/24
```

❌ Wrong context

```bash
address add ...
```

(when not already inside `/ip`)

---

## Mental model (this makes it click)

RouterOS internally sees everything like this:

```
/ip/address/add address=192.168.0.1/24 interface=bridge
```

Spaces are just navigation shortcuts.

---

## Quick Reference Table

| Command Style             | Works | Notes                     |
| ------------------------- | ----- | ------------------------- |
| `/ip address add ...`     | ✅     | Best for docs             |
| `ip address /add ...`     | ✅     | Your preferred style      |
| `/ip address` → `add ...` | ✅     | Interactive               |
| `address add ...`         | ⚠️    | Only inside `/ip`         |
| `add ...`                 | ⚠️    | Only inside `/ip address` |




