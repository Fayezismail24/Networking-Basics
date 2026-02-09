
# TX Power and Wireless Chains (Very Simple Explanation)

This explanation is based on the slide and is written for beginners.

---

## Big Idea (One Sentence)

**TX power is shared between wireless chains, and different Wi-Fi standards handle this sharing differently.**

---

## 1. What Is TX Power?

TX power means:
> How loud the router is talking

It is measured in **dBm**.

Examples:
- 20 dBm = loud
- 10 dBm = quieter

- Higher TX power can help the signal travel farther, but it also depends on environmental factors like obstacles (walls, buildings, etc.).

---

## 2. What Is a Wireless Chain?

Think of a chain as:
> One mouth and one ear

- 1 chain → one mouth talking
- 2 chains → two mouths talking at the same time
- More chains → higher speed

---

## 3. What the Table Is Showing

The table compares:
- **802.11n** (older Wi-Fi)
- **802.11ac** (newer Wi-Fi)

It shows what happens to TX power when:
- 1 chain is enabled
- 2 chains are enabled
- 3 chains are enabled

---

## 4. 802.11n Behavior (Older Wi-Fi)

In **802.11n**, power is **added together**.

### Example (TX Power = 20 dBm):

- 1 chain  
  - Total power = 20 dBm

- 2 chains  
  - Total power = 23 dBm  
  (+3 dBm)

- 3 chains  
  - Total power = 25 dBm  
  (+5 dBm)

**More chains = louder overall signal**

---

## 5. 802.11ac Behavior (Newer Wi-Fi)

In **802.11ac**, total power is **fixed**.

### Example (TX Power = 20 dBm):

- 1 chain  
  - 20 dBm per chain

- 2 chains  
  - 17 dBm per chain  
  (-3 dBm each)

- 3 chains  
  - 15 dBm per chain  
  (-5 dBm each)

**Power is divided, not added**

---

## 6. Why This Difference Exists

- Wireless laws limit **total transmitted power**
- Newer Wi-Fi standards follow regulations more strictly
- Speed should increase using **more streams**, not more loudness

---

## 7. Important Things to Remember

- More chains increase **speed**, not **range**
- TX power you set is **total power**
- New Wi-Fi standards split power between chains
- Lower RSSI with more chains is normal

---

## 8. Simple Analogy

- One speaker → all volume goes to one
- Two speakers → volume is split
- Three speakers → volume is split more

Total loudness stays the same.

---

## Final Takeaway

> Do not expect more chains to increase signal strength.  
> Chains are for speed, TX power controls loudness.


<img width="1152" height="744" alt="image" src="https://github.com/user-attachments/assets/b755c422-189f-4621-b71d-eb70e51f22c5" />


