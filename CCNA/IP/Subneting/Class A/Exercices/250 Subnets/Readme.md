
```markdown
Consider the following IP address: **10.0.0.0/8**

We need to create **250 subnets**.

---

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary):

```

11111111.00000000.00000000.00000000  → /8

```

To create **250 subnets**, we must borrow bits from the **host portion**.

---

### How many bits do we need?

Formula:

```

2^n ≥ required subnets

```

For 250 subnets:

```

2^8 = 256 ≥ 250

```

✅ **We need to borrow 8 bits** from the host portion.

---

### How many networks can we create?

Number of networks = 2^(borrowed bits)  

```

2^8 = 256 networks

```

✅ **We can create up to 256 subnets** from this /8 network.

---

### New Subnet Mask

Borrowing **8 bits** from the host portion:

```

11111111.11111111.00000000.00000000

```

New subnet mask:

```

/16 → 255.255.0.0

```

---

## Step 2: Determine the Increment

The increment is the value of the **last borrowed bit** (in the second octet):

```

Increment = 1 in second octet → 256 in third and fourth octet range

```

---

## Step 3: Determine Usable Hosts per Subnet

- Host bits: **16**  
- Total usable hosts per subnet:

```

2^16 − 2 = 65,534 usable hosts

```

---

## Step 4: Configure the Subnets (First 10 Examples)

| Subnet # | Network ID   | First Host   | Last Host    | Broadcast Address |
|-----------|--------------|--------------|--------------|-----------------|
| 1         | 10.0.0.0     | 10.0.0.1     | 10.0.255.254 | 10.0.255.255    |
| 2         | 10.1.0.0     | 10.1.0.1     | 10.1.255.254 | 10.1.255.255    |
| 3         | 10.2.0.0     | 10.2.0.1     | 10.2.255.254 | 10.2.255.255    |
| 4         | 10.3.0.0     | 10.3.0.1     | 10.3.255.254 | 10.3.255.255    |
| 5         | 10.4.0.0     | 10.4.0.1     | 10.4.255.254 | 10.4.255.255    |
| 6         | 10.5.0.0     | 10.5.0.1     | 10.5.255.254 | 10.5.255.255    |
| 7         | 10.6.0.0     | 10.6.0.1     | 10.6.255.254 | 10.6.255.255    |
| 8         | 10.7.0.0     | 10.7.0.1     | 10.7.255.254 | 10.7.255.255    |
| 9         | 10.8.0.0     | 10.8.0.1     | 10.8.255.254 | 10.8.255.255    |
| 10        | 10.9.0.0     | 10.9.0.1     | 10.9.255.254 | 10.9.255.255    |

---

✅ **Notes:**  
- Each /16 subnet has 65,534 usable hosts.  
- Borrowing 8 bits from the host portion creates **256 subnets**, enough to cover the 250 required.  
- Increment = 1 in the second octet → each new subnet starts with the next number in the second octet.

```


