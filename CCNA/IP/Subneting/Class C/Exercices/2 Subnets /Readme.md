```markdown
Consider the following IP address: **192.168.0.1/24**

We need to create **2 subnets**.

## Step 1: Determine the New Subnet Mask

Old subnet mask (binary): 11111111.11111111.11111111.00000000  →  /24

```


```

To create **2 subnets**, we must borrow bits from the **host portion**.

### How many bits do we need to borrow?

Formula: 2^n ≥ number of required subnets

```


```

For 2 subnets: 2^1 = 2

```


```

✅ **We need to borrow 1 bit**

### Bit Value Table (Last Octet)

| Bit Position | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|--------------|----|----|----|----|----|----|----|----|
| Decimal Value|128 | 64 | 32 | 16 | 8  | 4  | 2  | 1  |

### New Subnet Mask

Borrowing **1 bit** from the host portion (highlighted in red):
```

11111111.11111111.11111111.<span style="color:red">1</span>0000000

```

New subnet mask: /25  →  255.255.255.128

```


```

### Result

- **Number of subnets:** 2  
- **Hosts per subnet:** 2⁷ − 2 = 126
```

