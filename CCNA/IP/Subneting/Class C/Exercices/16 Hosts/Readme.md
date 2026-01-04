

```markdown
Consider the following IP address: **192.168.66.0/24**

We need to create a subnet that supports **at least 16 usable hosts**.

---

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary):

```

11111111.11111111.11111111.00000000  →  /24

```

To support **16 usable hosts**, we must borrow bits from the **host portion** (not the network portion).

---

### How many bits do we need?

Formula:

```

2^n − 2 ≥ required hosts

```

For 16 hosts:

```

2^5 − 2 = 30

```

✅ **We need 5 host bits**

That means we borrow:

```

8 − 5 = 3 bits

```

---

### Bit Value Table (Last Octet)

| Bit Position  | 2⁷  | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|---------------|-----|----|----|----|----|----|----|----|
| Decimal Value | 128 | 64 | 32 | 16 | 8  | 4  | 2  | 1  |

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

The increment is the value of the first remaining host bit:

```

Increment = 32

```

---

## Step 3: Determine Usable Hosts per Subnet

- Host bits: **5**
- Total usable hosts per subnet:

```

2^5 − 2 = 30 usable hosts

```

---

## Step 4: Configure the Subnets

### Subnet 1
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.0       |
| First Usable Host   | 192.168.66.1       |
| Last Usable Host    | 192.168.66.30      |
| Broadcast Address   | 192.168.66.31      |

### Subnet 2
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.32      |
| First Usable Host   | 192.168.66.33      |
| Last Usable Host    | 192.168.66.62      |
| Broadcast Address   | 192.168.66.63      |

### Subnet 3
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.64      |
| First Usable Host   | 192.168.66.65      |
| Last Usable Host    | 192.168.66.94      |
| Broadcast Address   | 192.168.66.95      |

### Subnet 4
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.96      |
| First Usable Host   | 192.168.66.97      |
| Last Usable Host    | 192.168.66.126     |
| Broadcast Address   | 192.168.66.127     |

### Subnet 5
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.128     |
| First Usable Host   | 192.168.66.129     |
| Last Usable Host    | 192.168.66.158     |
| Broadcast Address   | 192.168.66.159     |

### Subnet 6
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.160     |
| First Usable Host   | 192.168.66.161     |
| Last Usable Host    | 192.168.66.190     |
| Broadcast Address   | 192.168.66.191     |

### Subnet 7
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.192     |
| First Usable Host   | 192.168.66.193     |
| Last Usable Host    | 192.168.66.222     |
| Broadcast Address   | 192.168.66.223     |

### Subnet 8
| Category            | Address            |
|---------------------|--------------------|
| Network ID          | 192.168.66.224     |
| First Usable Host   | 192.168.66.225     |
| Last Usable Host    | 192.168.66.254     |
| Broadcast Address   | 192.168.66.255     |
```

