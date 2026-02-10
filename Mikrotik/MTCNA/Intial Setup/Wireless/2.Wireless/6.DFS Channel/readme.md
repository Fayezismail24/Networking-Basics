
## 📡 DFS Channels (Dynamic Frequency Selection)

**DFS channels** are special **5 GHz channels** that Wi-Fi devices can use **only if radar is not detected**.  

- Purpose: Avoid interference with **radar systems** (weather, military, airports).  
- Not all channels in 5 GHz band are DFS channels.

---

## ⚙️ How DFS Works

1. MikroTik scans the DFS channel before transmitting.
2. If radar signal is detected:
   - The radio must **stop transmitting** on that channel immediately.
   - Switch to another allowed channel.
3. If no radar is detected:
   - Device can use the channel normally.
4. After switching, there is a **CAC (Channel Availability Check) time**:
   - Usually **60 seconds**, during which the AP listens for radar.

---

## 🗂️ DFS Channels (Common in MikroTik)

| Channel | Center Frequency (MHz) |
|---------|-----------------------|
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

> Note: Channels **36, 40, 44, 48** are **non-DFS**, safe to use without radar restrictions.

---

## 🔑 MikroTik & Exam Notes

- DFS channels → higher number, 5 GHz only  
- Can **increase available spectrum**  
- Must **scan for radar before use**  
- CAC = AP waits before allowing clients  

---

## 🧠 Quick Memory Trick

- **Low 5 GHz channels (36–48)** → No radar → safe  
- **High 5 GHz channels (52–140)** → DFS → radar check  

<img width="639" height="190" alt="image" src="https://github.com/user-attachments/assets/146b2bee-1be3-4eed-9f4f-724df381079b" />
