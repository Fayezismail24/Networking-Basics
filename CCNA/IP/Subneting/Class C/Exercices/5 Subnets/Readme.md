To create **5 subnets** from a **192.168.60.0/24** network, we need to borrow bits and modify the subnet mask accordingly. Here's how you can break it down and correct the Markdown:

### Steps:

* **Step 1**: Borrow 3 bits to create 5 subnets.
* **Step 2**: Calculate the increment.
* **Step 3**: Calculate usable hosts per subnet.
* **Step 4**: List all subnets.

Here's the corrected **Markdown** with **5 subnets**:

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

For 5 subnets:
```

2^3 = 8

```
✅ **We need to borrow 3 bits** (since `2^3 = 8`, which is the smallest power of 2 greater than or equal to 5).

---

### Bit Value Table (Last Octet)

| Bit Position | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|--------------|----|----|----|----|----|----|----|----|
| Decimal Value| 128 | 64 | 32 | 16 | 8  | 4  | 2  | 1  |

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

- Remaining host bits: **5**
- Total hosts per subnet:
```

2^5 − 2 = 32 − 2 = 30 usable hosts

```

---

## Step 4: Configure the Subnets

### Subnet 1

| Category          | Address           |
|------------------|-------------------|
| Network ID        | 192.168.60.0      |
| First Usable Host | 192.168.60.1      |
| Last Usable Host  | 192.168.60.30     |
| Broadcast Address | 192.168.60.31     |

### Subnet 2

| Category          | Address           |
|------------------|-------------------|
| Network ID        | 192.168.60.32     |
| First Usable Host | 192.168.60.33     |
| Last Usable Host  | 192.168.60.62     |
| Broadcast Address | 192.168.60.63     |

### Subnet 3

| Category          | Address           |
|------------------|-------------------|
| Network ID        | 192.168.60.64     |
| First Usable Host | 192.168.60.65     |
| Last Usable Host  | 192.168.60.94     |
| Broadcast Address | 192.168.60.95     |

### Subnet 4

| Category          | Address           |
|------------------|-------------------|
| Network ID        | 192.168.60.96     |
| First Usable Host | 192.168.60.97     |
| Last Usable Host  | 192.168.60.126    |
| Broadcast Address | 192.168.60.127    |

### Subnet 5

| Category          | Address           |
|------------------|-------------------|
| Network ID        | 192.168.60.128    |
| First Usable Host | 192.168.60.129    |
| Last Usable Host  | 192.168.60.158    |
| Broadcast Address | 192.168.60.159    |
```

