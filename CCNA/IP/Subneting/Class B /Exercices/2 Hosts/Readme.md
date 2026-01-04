Got it, Boss. The version you pasted still has errors: it mixes **2-host subnetting** with a **/27 example for 30 hosts**. Since you said the requirement is **2 usable hosts** for a **172.16.0.0/16** network, here’s the **correct and complete fix**, in your Markdown style, continuing properly with multiple /30 subnets.

```markdown
Consider the following IP address: **172.16.0.0/16**

We need to create a subnet that supports **at least 2 usable hosts**.

---

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary):

```

11111111.11111111.00000000.00000000  → /16

```

To support **2 usable hosts**, we must borrow bits from the **host portion** (not the network portion).

---

### How many bits do we need?

Formula:

```

2^n − 2 ≥ required hosts

```

For 2 hosts:

```

2^2 − 2 = 2

```

✅ **We need 2 host bits**

That means we borrow:

```

32 − 16 − 2 = 14 bits borrowed from the original host portion

```

---

### New Subnet Mask

Borrowing **14 bits** from the host portion:

```

11111111.11111111.11111111.11111100

```

New subnet mask:

```

/30 → 255.255.255.252

```

---

## Step 2: Determine the Increment

The increment is the value of the **last borrowed bit** (in the last octet):

```

Increment = 4

```

---

## Step 3: Determine Usable Hosts per Subnet

- Host bits: **2**  
- Total usable hosts per subnet:

```

2^2 − 2 = 2 usable hosts

```

---

## Step 4: Configure the Subnets

| Subnet # | Network ID      | First Host     | Last Host      | Broadcast Address |
|-----------|----------------|----------------|----------------|-----------------|
| 1         | 172.16.0.0     | 172.16.0.1     | 172.16.0.2     | 172.16.0.3      |
| 2         | 172.16.0.4     | 172.16.0.5     | 172.16.0.6     | 172.16.0.7      |
| 3         | 172.16.0.8     | 172.16.0.9     | 172.16.0.10    | 172.16.0.11     |
| 4         | 172.16.0.12    | 172.16.0.13    | 172.16.0.14    | 172.16.0.15     |
| 5         | 172.16.0.16    | 172.16.0.17    | 172.16.0.18    | 172.16.0.19     |
| 6         | 172.16.0.20    | 172.16.0.21    | 172.16.0.22    | 172.16.0.23     |
| 7         | 172.16.0.24    | 172.16.0.25    | 172.16.0.26    | 172.16.0.27     |
| 8         | 172.16.0.28    | 172.16.0.29    | 172.16.0.30    | 172.16.0.31     |
```

---


