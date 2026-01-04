Perfect, Boss. Let’s organize this **properly in Markdown**, with the full subnetting explanation like your previous style. I’ll assume you want the **increment, subnet mask, usable hosts, and broadcast** for all 6 subnets.

```markdown
Consider the following IP address: **172.16.0.0/16**

We need to create **6 subnets**.

---

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary):

```

11111111.11111111.00000000.00000000  → /16

```

We need **6 subnets**, so we must borrow bits from the **host portion**.

---

### How many bits do we need?

Formula:

```

2^n ≥ required subnets

```

For 6 subnets:

```

2^3 = 8  ≥ 6

```

✅ **We need to borrow 3 bits**

---

### New Subnet Mask

Borrowing **3 bits** from the host portion (3 bits of the 3rd octet):

```

11111111.11111111.11100000.00000000

```

New subnet mask:

```

/19  →  255.255.224.0

```

---

### Step 2: Determine the Increment

The increment is the value of the **first borrowed bit** in the 3rd octet:

```

Increment = 32

```

---

### Step 3: Determine Usable Hosts per Subnet

- Host bits: **13** (32 − 19 = 13)  
- Total usable hosts per subnet:

```

2^13 − 2 = 8192 − 2 = 8190 usable hosts

```

---

## Step 4: Configure the Subnets

| Subnet # | Network ID      | First Host      | Last Host       | Broadcast Address |
|-----------|----------------|----------------|----------------|-----------------|
| 1         | 172.16.0.0     | 172.16.0.1     | 172.16.31.254  | 172.16.31.255   |
| 2         | 172.16.32.0    | 172.16.32.1    | 172.16.63.254  | 172.16.63.255   |
| 3         | 172.16.64.0    | 172.16.64.1    | 172.16.95.254  | 172.16.95.255   |
| 4         | 172.16.96.0    | 172.16.96.1    | 172.16.127.254 | 172.16.127.255  |
| 5         | 172.16.128.0   | 172.16.128.1   | 172.16.159.254 | 172.16.159.255  |
| 6         | 172.16.160.0   | 172.16.160.1   | 172.16.191.254 | 172.16.191.255  |
```

---

