
## 📡 What is Channel Frequency?

**Channel frequency** is the exact radio frequency (in MHz) that a wireless channel uses inside a band (2.4 GHz or 5 GHz).

Each Wi-Fi channel = a **center frequency**.

---

## 📶 2.4 GHz Channel Frequencies

- Channel spacing: **5 MHz**
- Channel width: **20 MHz**
- Result: channels **overlap**

| Channel | Center Frequency (MHz) |
|-------|------------------------|
| 1 | 2412 |
| 2 | 2417 |
| 3 | 2422 |
| 4 | 2427 |
| 5 | 2432 |
| 6 | 2437 |
| 7 | 2442 |
| 8 | 2447 |
| 9 | 2452 |
| 10 | 2457 |
| 11 | 2462 |
| 12 | 2467 |
| 13 | 2472 |

### Non-Overlapping Channels
- **1 – 6 – 11**
- This is why MikroTik best practice uses these only

---

## 📶 5 GHz Channel Frequencies

- Channel spacing: **20 MHz**
- Channels **do not overlap** (when using 20 MHz width)

| Channel | Center Frequency (MHz) |
|--------|------------------------|
| 36 | 5180 |
| 40 | 5200 |
| 44 | 5220 |
| 48 | 5240 |
| 52 | 5260 |
| 56 | 5280 |
| 60 | 5300 |
| 64 | 5320 |
| 100 | 5500 |
| 104 | 5520 |
| 108 | 5540 |
| 112 | 5560 |
| 116 | 5580 |
| 120 | 5600 |
| 124 | 5620 |
| 128 | 5640 |
| 132 | 5660 |
| 136 | 5680 |
| 140 | 5700 |

---

## 📏 Channel Width vs Frequency

| Channel Width | Frequency Usage |
|--------------|----------------|
| 20 MHz | 1 channel |
| 40 MHz | 2 bonded channels |
| 80 MHz | 4 bonded channels |
| 160 MHz | 8 bonded channels |

- Wider channel = higher speed
- Wider channel = more interference

---

## 🧠 MikroTik Exam Notes

- Channel = **center frequency**
- 2.4 GHz overlaps → use **1, 6, 11**
- 5 GHz cleaner → more usable channels
- Wrong channel frequency = poor signal & low CCQ

---

## 🔑 One-Line Memory Trick
Channel = **where** you transmit  
Frequency = **exact MHz of that channel**


