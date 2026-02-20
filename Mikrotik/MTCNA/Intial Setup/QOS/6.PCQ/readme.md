

## What is PCQ?

**PCQ** stands for **Per Connection Queue**.

It is a queue type in **MikroTik RouterOS** that automatically **divides bandwidth equally** among multiple users or connections.

Instead of manually creating a queue for every user, PCQ does it dynamically.

---

## Why PCQ Exists

Problem:

You have 20 users.
You set a 20 Mbps limit.
One user starts downloading heavily.
He takes most of the bandwidth.
Everyone else suffers.

Solution:

PCQ automatically splits bandwidth fairly between active users.

---

## How PCQ Works (Simple Version)

PCQ:

1. Detects active users based on IP
2. Creates a sub-queue for each user
3. Splits bandwidth evenly between them

If:

* 1 active user → gets full bandwidth
* 2 users → each gets 50%
* 4 users → each gets 25%

It dynamically adjusts.

---

## Key PCQ Parameters

### 1. pcq-classifier

This decides how traffic is divided.

Common values:

* `src-address` → divides based on source IP
* `dst-address` → divides based on destination IP

For ISP style download control:

* Download → use `dst-address`
* Upload → use `src-address`

If you mix this up, your fairness breaks.

---
<img width="561" height="520" alt="image" src="https://github.com/user-attachments/assets/4711b484-8e2a-44b0-8857-ba6836d93d6a" />


### 2. pcq-rate

Maximum rate per user.

Example:

* pcq-rate = 2M
  Means each user can get up to 2 Mbps.

If total bandwidth is 20 Mbps:

* 5 users → each 2 Mbps
* 10 users → still max 2 Mbps each
* If only 1 user → still limited to 2 Mbps

Important: pcq-rate limits per user, not total.

---

### 3. pcq-limit and pcq-total-limit

These control buffering size.
Usually default values are fine unless tuning for high performance networks.

---

## Where PCQ Is Used

PCQ is usually applied inside:

* `/queue tree`
* `/queue simple`

Most professional setups use PCQ with **queue tree**, not simple queue.

---

## When Should You Use PCQ?

Use PCQ when:

* You want equal bandwidth distribution
* You don’t want to manually create queues
* You manage multiple users
* You are building ISP-style bandwidth control

Do NOT use PCQ if:

* You need priority-based shaping
* You want guaranteed bandwidth per VIP user


