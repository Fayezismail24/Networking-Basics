# Binary for Networking 

## 📌 Why Binary & Hex Matter in Networking

Every IP address, MAC address, and subnet mask is just a number. Routers and switches don't see `192.168.1.1` — they see `11000000.10101000.00000001.00000001`. Understanding binary and hex is the **foundation of subnetting, IP addressing, and VLANs**.

```
What YOU see:        192.168.1.1
What the router sees: 11000000.10101000.00000001.00000001

What YOU see:        FF:AA:00:4B:2C:11  (MAC Address)
What the switch sees: 1111 1111 : 1010 1010 : 0000 0000 ...
```

---

## 🔢 Number Systems Overview

| System | Base | Digits Used | Used In |
|---|---|---|---|
| Binary | Base-2 | 0, 1 | IP addresses, subnet masks |
| Decimal | Base-10 | 0–9 | Human-readable IPs |
| Hexadecimal | Base-16 | 0–9, A–F | MAC addresses, IPv6 |

---

## 🧱 Binary Basics

### What is a Bit?
A **bit** is a single binary digit — either `0` or `1`. Everything in networking is built from bits.

```
1 bit  = 0 or 1
4 bits = 1 nibble
8 bits = 1 byte (octet)
```

### IPv4 is 32 bits — 4 Octets

```
192      .    168     .     1      .     1
11000000 . 10101000 . 00000001 . 00000001
 8 bits      8 bits     8 bits     8 bits
```

---

## 🔄 Decimal to Binary Conversion

### The Power of 2 Table (memorize this)

| Bit Position | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 |
|---|---|---|---|---|---|---|---|---|
| Value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

> 💡 **Memory trick:** 128, 64, 32, 16, 8, 4, 2, 1 — each is half of the one before it.

### Method: Go left to right — if the value fits, subtract it and write 1, if not write 0

**Example: Convert 192 to binary**

```
 128   64   32   16    8    4    2    1
─────────────────────────────────────────
  ?

192 - 128 = 64  → fits → write 1,  carry 64
 64 -  64 =  0  → fits → write 1,  carry 0
  0 -  32       → doesn't fit → write 0
  0 -  16       → doesn't fit → write 0
  0 -   8       → doesn't fit → write 0
  0 -   4       → doesn't fit → write 0
  0 -   2       → doesn't fit → write 0
  0 -   1       → doesn't fit → write 0

 128   64   32   16    8    4    2    1
   1    1    0    0    0    0    0    0

Result: 11000000 = 192 ✅
```

**Example: Convert 172 to binary**

```
 128   64   32   16    8    4    2    1
─────────────────────────────────────────
172 - 128 = 44  → fits → write 1,  carry 44
 44 -  64       → doesn't fit → write 0
 44 -  32 = 12  → fits → write 1,  carry 12
 12 -  16       → doesn't fit → write 0
 12 -   8 =  4  → fits → write 1,  carry 4
  4 -   4 =  0  → fits → write 1,  carry 0
  0 -   2       → doesn't fit → write 0
  0 -   1       → doesn't fit → write 0

 128   64   32   16    8    4    2    1
   1    0    1    0    1    1    0    0

Result: 10101100 = 172 ✅
```

---

## 🔄 Binary to Decimal Conversion

### Method: Add up the values where the bit is 1

**Example: Convert 11000000 to decimal**

```
Bit values: 128  64  32  16  8  4  2  1
Binary:       1   1   0   0  0  0  0  0

128 + 64 = 192 ✅
```

**Example: Convert 10101000 to decimal**

```
Bit values: 128  64  32  16  8  4  2  1
Binary:       1   0   1   0  1  0  0  0

128 + 32 + 8 = 168 ✅
```

---



## 🧪 Practice Conversions

Try these before checking the answers:

**Decimal → Binary**
1. 10 = ?
2. 255 = ?
3. 128 = ?
4. 200 = ?

**Binary → Decimal**
1. 00001010 = ?
2. 11111111 = ?
3. 11001000 = ?
4. 10000000 = ?



<details>
<summary>✅ Click to reveal answers</summary>

**Decimal → Binary**
1. 10 = 00001010
2. 255 = 11111111
3. 128 = 10000000
4. 200 = 11001000

**Binary → Decimal**
1. 00001010 = 10
2. 11111111 = 255
3. 11001000 = 200
4. 10000000 = 128



</details>

---



## ❓ CCNA Exam Practice Questions

**Q1:** What is 192 in binary?  
**A:** 11000000

**Q2:** What is 11111111 in decimal?  
**A:** 255



**Q5:** Convert 10000000 to decimal.  
**A:** 128

**Q6:** How many bits are in an IPv4 address?  
**A:** 32 bits (4 octets of 8 bits each)

---


