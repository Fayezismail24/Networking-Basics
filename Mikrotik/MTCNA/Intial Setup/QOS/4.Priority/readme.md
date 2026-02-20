
## Queue Priority (QoS Concept)

Priority in a queue determines **who gets served first when bandwidth is congested**.

If there is no congestion, priority does nothing.  
It only matters when total traffic demand exceeds available bandwidth.

---

## 🔹 What Priority Actually Means

Imagine your WAN link has:

10 Mbps total bandwidth.

Traffic demand:

- Voice traffic → 2 Mbps  
- Video → 5 Mbps  
- Downloads → 10 Mbps  

Total demand = 17 Mbps  
Available = 10 Mbps  

Now the router must decide:

Who gets bandwidth first?

That decision is controlled by **queue priority**.

---

## 🔹 Priority Values (MikroTik)

In MikroTik Simple Queues and Queue Tree:

1 → Highest priority  
8 → Lowest priority  

So:

- Priority 1 = Served first  
- Priority 8 = Served last  

Important:

Priority does NOT increase bandwidth.  
It only affects traffic during congestion.

---

## 🔹 Example Configuration

- VoIP → priority 1  
- Gaming → priority 2  
- Web browsing → priority 4  
- Downloads → priority 8  

During congestion:

1. VoIP is protected first  
2. Gaming is protected next  
3. Browsing shares what remains  
4. Downloads are slowed down first  

This prevents latency-sensitive traffic (like voice) from being disrupted.

---

## 🔹 When Does Priority Apply?

Priority works only when:

- Queues share the same parent  
- The parent max-limit is being reached  

If there is free bandwidth, all queues can use it regardless of priority.

---

## 🔹 Common Mistake

Higher priority does NOT mean more bandwidth.

If you want guaranteed bandwidth, use:

`limit-at` → Minimum guaranteed bandwidth  

Priority only controls borrowing order when congestion happens.

---


