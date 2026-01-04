
```markdown
Consider the following IP address: **192.168.60.0/24**

We need to create **5 subnets**.

---

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary):

```

11111111.11111111.11111111.00000000  →  /24

```

To create **5 subnets**, we must borrow bits from the **host portion**.

### How many bits do we need to borrow?

Formula:

```

2^n ≥ number of required subnets

```

For 2 subnets:

```

2^3 = 

```

✅ **We need to borrow 3  bits**

---

### Bit Value Table (Last Octet)

| Bit Position | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|--------------|----|----|----|----|----|----|----|----|
| Decimal Value|128 | 64 | 32 | 16 | 8  | 4  | 2  | 1  |

---

### New Subnet Mask

Borrowing **3 bits** from the host portion:

```

11111111.11111111.11111111.11100000

```

New subnet mask:

```

/27  →  255.255.255.224

```

---

## Step 2: Determine the Increment

The last borrowed bit has a value of **32**, so:

```

Increment = 32

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


