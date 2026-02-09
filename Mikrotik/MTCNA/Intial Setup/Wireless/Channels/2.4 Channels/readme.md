<img width="1150" height="853" alt="image" src="https://github.com/user-attachments/assets/04ba4c31-16d7-4943-adfd-f6e16e353e2e" />




# 2.4 GHz Wi-Fi Channels Explained (Based on the Image)

This explanation covers how 2.4 GHz Wi-Fi channels work, why they overlap, and how to use them correctly in real networks (especially MikroTik).

---

## 1. What is the 2.4 GHz Band?

The **2.4 GHz band** is a frequency range used by Wi-Fi and many other technologies.

**Characteristics:**
- Long range
- Good wall penetration
- Lower speeds compared to 5 GHz
- Very crowded (Wi-Fi, Bluetooth, microwaves, cordless phones)

This band is divided into multiple **channels**.

---

## 2. What Are Wi-Fi Channels?

A **channel** is a small slice of frequency inside the 2.4 GHz band.

From the image:
- Channels range from **1 to 13** (channel 14 exists only in Japan)
- Each channel has a **center frequency**

Examples:
- Channel 1 → 2412 MHz  
- Channel 6 → 2437 MHz  
- Channel 11 → 2462 MHz  

The numbers shown at the top of the image represent these center frequencies.

---

## 3. Channel Width (Why Overlap Happens)

Each 2.4 GHz Wi-Fi channel is **22 MHz wide**.

But:
- Channel numbers are only **5 MHz apart**

### Result:
Channels **overlap heavily**.

Examples:
- Channel 1 overlaps with channels 2–5
- Channel 6 overlaps with channels 4, 5, 7, 8
- Channel 11 overlaps with channels 9, 10, 12

This overlap is visualized in the image as overlapping “hills”.

---

## 4. Why Channels 1, 6, and 11 Are Special

Channels **1, 6, and 11** are spaced far enough apart that their 22 MHz widths **do not overlap**.

That’s why the slide states:
- **3 non-overlapping channels (1, 6, 11)**

Using only these channels avoids **adjacent-channel interference**.

---

## 5. Interference Explained

Interference does **not** mean no internet. It causes:
- Slower speeds
- Higher latency
- More packet retries
- Unstable connections

### Types of interference:
- **Co-channel interference**: same channel (manageable)
- **Adjacent-channel interference**: overlapping channels (very bad)

Adjacent-channel interference is the main reason random channels like 3, 4, 8 should be avoided.

---

## 6. “3 APs Can Occupy the Same Area” Explained

Because there are only **3 clean channels**, you can safely deploy:

- AP 1 → Channel 1  
- AP 2 → Channel 6  
- AP 3 → Channel 11  

All in the same area **without interfering**.

Adding a 4th AP means reusing a channel, which reduces performance.

---

## 7. Country Regulations

Channel availability depends on country rules:

- Most of the world: **Channels 1–13**
- USA: **Channels 1–11**
- Japan: **Channel 14** (legacy use)

In MikroTik:
- Always set the correct **Country** and **Regulatory Domain**

---

## 8. Best Practices (Especially for MikroTik)

For 2.4 GHz networks:
- Do **not** use Auto channel in crowded areas
- Use only **1, 6, or 11**
- Set channel width to **20 MHz**
- Avoid **40 MHz** on 2.4 GHz
- Reduce TX power instead of increasing it

---

## 9. Key Takeaway

- 2.4 GHz has **13 channels**
- Only **3 are usable without overlap**
- Overlapping channels cause serious performance issues
- Proper channel planning is mandatory

Think of 2.4 GHz like:
- 13 painted lanes
- Only 3 real usable ones
- Everyone else crashes into each other

That’s why modern networks prefer **5 GHz**, but 2.4 GHz remains important for range and compatibility.
