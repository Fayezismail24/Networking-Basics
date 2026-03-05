# Hexadecimal for Networking

## 📌 Why Hex Matters in Networking

Every MAC address and IPv6 address is written in hexadecimal. Switches and routers don't show you raw binary — they use hex as a shorthand. Understanding hex lets you read MAC addresses, IPv6, and Wireshark captures fluently.

```
What YOU see:        FF:AA:00:4B:2C:11       (MAC Address)
What it really is:   1111 1111 : 1010 1010 : 0000 0000 ...  (Binary)

What YOU see:        2001:0DB8::FF00:42:8329  (IPv6 Address)
What it really is:   128 bits of binary, written in hex for readability
```

---

## 🔢 Number Systems Overview

| System | Base | Digits Used | Used In |
|---|---|---|---|
| Binary | Base-2 | 0, 1 | IP addresses, subnet masks |
| Decimal | Base-10 | 0–9 | Human-readable IPs |
| Hexadecimal | Base-16 | 0–9, A–F | MAC addresses, IPv6 |

---

## 🧱 Hex Basics

### What is a Hex Digit?
A **hex digit** is a single character from 0–9 or A–F. It represents 4 binary bits (1 nibble).

```
1 hex digit  = 4 bits  (1 nibble)
2 hex digits = 8 bits  (1 byte / octet)
6 hex digits = 24 bits (3 bytes)
12 hex digits = 48 bits (MAC address)
32 hex digits = 128 bits (IPv6 address)
```

### The Hex Table (memorize this)

| Decimal | Hex | Binary |
|---|---|---|
| 0 | 0 | 0000 |
| 1 | 1 | 0001 |
| 2 | 2 | 0010 |
| 3 | 3 | 0011 |
| 4 | 4 | 0100 |
| 5 | 5 | 0101 |
| 6 | 6 | 0110 |
| 7 | 7 | 0111 |
| 8 | 8 | 1000 |
| 9 | 9 | 1001 |
| 10 | A | 1010 |
| 11 | B | 1011 |
| 12 | C | 1100 |
| 13 | D | 1101 |
| 14 | E | 1110 |
| 15 | F | 1111 |

> 💡 **Memory trick:** 0–9 stay the same. A=10, B=11, C=12, D=13, E=14, F=15.

---

## 🔄 Binary to Hex Conversion

### Method: Split binary into groups of 4 bits, convert each group using the table

**Example: Convert 11000000 to hex**

```
 1100  |  0000
─────────────────
  ?    |   ?

1100 = 8+4 = 12 = C
0000 = 0

 1100  |  0000
   C   |   0

Result: C0 ✅
```

**Example: Convert 10101000 to hex**

```
 1010  |  1000
─────────────────
  ?    |   ?

1010 = 8+2 = 10 = A
1000 = 8

 1010  |  1000
   A   |   8

Result: A8 ✅
```

---

## 🔄 Hex to Binary Conversion

### Method: Convert each hex digit to exactly 4 bits using the table

**Example: Convert FF to binary**

```
  F    |   F
─────────────────
  ?    |   ?

F = 15 = 1111
F = 15 = 1111

  F    |   F
 1111  |  1111

Result: 11111111 ✅
```

**Example: Convert AC to binary**

```
  A    |   C
─────────────────
  ?    |   ?

A = 10 = 1010
C = 12 = 1100

  A    |   C
 1010  |  1100

Result: 10101100 = 172 ✅
```

---

## 🔄 Hex to Decimal Conversion

### Method: Multiply each hex digit by its positional value (16ⁿ) and add

**Positional values (right to left):**
```
Position:   ...  3      2      1      0
Value:      ... 4096   256    16      1
```

**Example: Convert C0 to decimal**

```
C = 12,  position 1 → 12 × 16 = 192
0 =  0,  position 0 →  0 ×  1 =   0

192 + 0 = 192 ✅
```

**Example: Convert A8 to decimal**

```
A = 10,  position 1 → 10 × 16 = 160
8 =  8,  position 0 →  8 ×  1 =   8

160 + 8 = 168 ✅
```

---

## 🖥️ MAC Addresses in Hex

A MAC address is **48 bits = 6 bytes = 12 hex digits**, written in pairs separated by colons or hyphens.

```
00 : 1A : 2B : 3C : 4D : 5E
──────────┬──────  ──────┬──────
     OUI (first 3 bytes)  Device ID (last 3 bytes)
     = Manufacturer ID    = Unique to device
```

**Example — reading a MAC address:**
```
MAC:    00  : 1A  : 2B  : 3C  : 4D  : 5E
Binary: 00000000 00011010 00101011 00111100 01001101 01011110
```

> 💡 **OUI lookup:** The first 3 bytes identify the manufacturer. `00:1A:2B` might be Cisco, `F8:FF:C2` might be Apple.

---



**Shortening rules:**
- Remove leading zeros in each group: `0DB8` → `DB8`
- Replace one or more consecutive all-zero groups with `::` (only once)

```
Full:      2001:0DB8:0000:0000:0000:FF00:0042:8329
Shortened: 2001:DB8::FF00:42:8329
```

---

## 🔁 Common Hex Values in Networking (Memorize These)

| Hex | Binary | Decimal | Where You'll See It |
|---|---|---|---|
| 00 | 00000000 | 0 | Empty octet |
| 0A | 00001010 | 10 | 10.x.x.x (Class A) |
| 80 | 10000000 | 128 | /1 subnet mask octet |
| AC | 10101100 | 172 | 172.x.x.x (Class B private) |
| C0 | 11000000 | 192 | 192.x.x.x (Class C private) |
| A8 | 10101000 | 168 | 192.168.x.x |
| FF | 11111111 | 255 | Broadcast / full subnet mask octet |
| FE | 11111110 | 254 | /31 subnet mask last octet |

---

## 🧪 Practice Conversions

Try these before checking the answers:

**Binary → Hex**
1. 11110000 = ?
2. 00001111 = ?
3. 10101010 = ?
4. 11111111 = ?

**Hex → Binary**
1. 0F = ?
2. AA = ?
3. F0 = ?
4. 1A = ?

**Hex → Decimal**
1. FF = ?
2. C0 = ?
3. 0A = ?

<details>
<summary>✅ Click to reveal answers</summary>

**Binary → Hex**
1. 11110000 = F0
2. 00001111 = 0F
3. 10101010 = AA
4. 11111111 = FF

**Hex → Binary**
1. 0F = 00001111
2. AA = 10101010
3. F0 = 11110000
4. 1A = 00011010

**Hex → Decimal**
1. FF = 255
2. C0 = 192
3. 0A = 10

</details>

---

## ❓ CCNA Exam Practice Questions

**Q1:** What is FF in binary?  
**A:** 11111111

**Q2:** What is 11000000 in hex?  
**A:** C0

**Q3:** How many hex digits are in a MAC address?  
**A:** 12 hex digits (6 bytes)

**Q4:** What does the first half of a MAC address represent?  
**A:** The OUI — identifies the manufacturer

**Q5:** Convert hex A8 to decimal.  
**A:** (10 × 16) + 8 = 168

**Q6:** How many bits does one hex digit represent?  
**A:** 4 bits (1 nibble)

---


