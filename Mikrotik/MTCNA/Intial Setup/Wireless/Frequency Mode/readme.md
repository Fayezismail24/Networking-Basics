Alright Boss, this is **pure MikroTik wireless logic**, and people mix these up all the time. I’ll explain them **cleanly**, **practically**, and in **Markdown**, so you can reuse it for notes or exams.

```md
# MikroTik Wireless: Frequency Mode Explained

This covers:
- Regulatory Domain
- Manual TX Power
- Superchannel
- How they relate to each other
- When to use each one

---

## 1. Regulatory Domain (Country Mode)

### What it is
Regulatory Domain means:
> MikroTik follows **your country’s wireless laws**

When you set:
- Country (e.g. Lebanon, Germany, USA)
- Installation (indoor / outdoor)

The router automatically enforces:
- Allowed frequencies
- Maximum TX power
- Allowed channel widths
- DFS rules (on 5 GHz)

### What you control
- You **cannot exceed legal limits**
- TX power is **auto-limited**
- Only legal channels are available

### Pros
- Legal
- Stable
- Less interference
- Required for ISPs and enterprises

### Cons
- Limited freedom
- Lower max TX power sometimes

### When to use
- Production networks
- Client networks
- Any real-world deployment

---

## 2. Manual TX Power

### What it is
Manual TX Power lets you:
> Override automatic power control

You manually set:
- Radio TX power (dBm)
- Per-chain power (in advanced setups)

### Important truth
Higher TX power ≠ better signal

Problems with high TX power:
- More interference
- Clients can’t reply back (asymmetry)
- Worse performance
- Hidden-node issues

### Correct usage
- Use **lowest power** that gives stable signal
- Balance AP power with client power
- Use manual TX only when you **know why**

### When to use
- Fine-tuning coverage
- High-density environments
- Long-distance point-to-point links

---

## 3. Superchannel Mode

### What it is
Superchannel means:
> No country rules. No limits.

MikroTik allows:
- All frequencies (even illegal ones)
- Very high TX power
- Non-standard channels

It ignores regulatory limits completely.

### Why it exists
- Labs
- Testing
- Licensed links
- Isolated environments

### Risks
- Illegal in most countries
- Can interfere with:
  - Radar
  - Airports
  - ISPs
  - Emergency services
- Can cause serious penalties

### When to use
- Lab testing only
- Licensed spectrum
- Remote, controlled environments

❌ Never for normal Wi-Fi

---

## 4. Regulatory vs Manual TX Power

| Feature | Regulatory Domain | Manual TX Power |
|------|------------------|----------------|
| Country limits | Enforced | Still enforced |
| Max power | Auto-limited | User-selected (within limits) |
| Legal | Yes | Yes |
| Stability | High | Depends on user |

Key point:
> Manual TX Power **does not break the law** if Regulatory Domain is enabled.

---

## 5. Regulatory Domain vs Superchannel

| Feature | Regulatory Domain | Superchannel |
|------|------------------|--------------|
| Country laws | Enforced | Ignored |
| Allowed frequencies | Limited | All |
| TX power limit | Yes | No |
| Legal use | Yes | Usually no |

Key point:
> Superchannel bypasses everything.

---

## 6. Frequency Mode Summary

- **Regulatory Domain**  
  Safe, legal, automatic, recommended

- **Manual TX Power**  
  Advanced tuning, still legal

- **Superchannel**  
  Dangerous freedom, lab-only

---

## 7. Golden Rule (MTCNA mindset)

- Always start with **Regulatory Domain**
- Use **manual TX power only when necessary**
- Treat **Superchannel like a loaded weapon**

If you want next:
- Real-world examples
- Exam-style questions
- MikroTik config screenshots logic
- Or comparison with Ubiquiti / Cisco behavior

Just say the word, Boss.
```
