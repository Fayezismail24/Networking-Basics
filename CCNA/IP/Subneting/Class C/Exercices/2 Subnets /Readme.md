Here is the **fully fixed, clean, and correct version**, properly formatted in **Markdown**, with logical flow, corrected IPs, and no syntax errors. You can copy–paste this as-is 👇

```markdown
Consider the following IP address: **192.168.0.1/24**

We need to create **2 subnets**.

---

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary):

```

11111111.11111111.11111111.00000000  →  /24

```

To create **2 subnets**, we must borrow bits from the **host portion**.

### How many bits do we need to borrow?

Formula:

```

2^n ≥ number of required subnets

```

For 2 subnets:

```

2^1 = 2

```

✅ **We need to borrow 1 bit**

---

### Bit Value Table (Last Octet)

| Bit Position | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|--------------|----|----|----|----|----|----|----|----|
| Decimal Value|128 | 64 | 32 | 16 | 8  | 4  | 2  | 1  |

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

The first borrowed bit has a value of **128**, so:

```

Increment = 128

```

---

## Step 3: Determine Usable Hosts per Subnet

- Remaining host bits: **7**
- Total hosts per subnet:

```

2^7 − 2 = 128 − 2 = 126 usable hosts

```

---

## Step 4: Configure the Subnets

### Subnet 1

| Category          | Address           |
|------------------|-------------------|
| Network ID        | 192.168.0.0       |
| First Usable Host | 192.168.0.1       |
| Last Usable Host  | 192.168.0.126     |
| Broadcast Address | 192.168.0.127     |

### Subnet 2

| Category          | Address           |
|------------------|-------------------|
| Network ID        | 192.168.0.128     |
| First Usable Host | 192.168.0.129     |
| Last Usable Host  | 192.168.0.254     |
| Broadcast Address | 192.168.0.255     |
```


