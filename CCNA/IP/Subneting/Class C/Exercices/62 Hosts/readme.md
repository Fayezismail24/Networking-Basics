
```markdown
Consider the following IP address: **192.168.47.0/24**

We need to create a subnet that supports **at least 62 usable hosts**.

---

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary):

```

11111111.11111111.11111111.00000000  →  /24

```

To support **62 usable hosts**, we must borrow bits from the **host portion**.

---

### How many bits do we need?

Formula:

```

2^n − 2 ≥ required hosts

```

For 62 hosts:

```

2^6 − 2 = 62

```

✅ **We need 6 host bits**

That means we borrow:

```

8 − 6 = 1 bit

```

---

### Bit Value Table (Last Octet)

| Bit Position  | 2⁷  | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|---------------|-----|----|----|----|----|----|----|----|
| Decimal Value | 128 | 64 | 32 | 16 | 8  | 4  | 2  | 1  |

---

### New Subnet Mask

Borrowing **1 bit** from the host portion:

```

11111111.11111111.11111111.10000000

```

New subnet mask:

```

/25  →  255.255.255.128

```

---

## Step 2: Determine the Increment

The increment is the value of the borrowed bit:

```

Increment = 128

```

---

## Step 3: Determine Usable Hosts per Subnet

- Host bits: **7**
- Total usable hosts per subnet:

```

2^7 − 2 = 126 usable hosts

```

(Enough to satisfy the requirement of 62 usable hosts)

---

## Step 4: Configure the Subnets

### Subnet 1

| Category            | Address             |
|---------------------|---------------------|
| Network ID          | 192.168.47.0        |
| First Usable Host   | 192.168.47.1        |
| Last Usable Host    | 192.168.47.126      |
| Broadcast Address   | 192.168.47.127      |

### Subnet 2

| Category            | Address             |
|---------------------|---------------------|
| Network ID          | 192.168.47.128      |
| First Usable Host   | 192.168.47.129      |
| Last Usable Host    | 192.168.47.254      |
| Broadcast Address   | 192.168.47.255      |
```


* Give you a **trap subnetting question**, or
* Make you solve one and I’ll **mark it like an exam** 👀
