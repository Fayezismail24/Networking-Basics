

## 1. New

* **Definition:** This refers to a packet that is attempting to open a brand new connection.
* **Example:** You type a website address into your browser and hit Enter. The very first packet (a TCP SYN) sent to the web server is marked as **New**.
* **Firewall Strategy:** This is where you apply your most restrictive rules. You usually only allow "New" connections from your internal network to the internet, not the other way around.

## 2. Established

* **Definition:** This refers to a packet that belongs to a connection the firewall already knows about.
* **Example:** Once the web server replies to your request and the "handshake" is finished, all subsequent data packets (loading the images, text, etc.) are **Established**.
* **Firewall Strategy:** Most admins place a rule at the very top of their list to "Accept Established" packets. Since the firewall already vetted the "New" packet, processing these is very fast and saves CPU.

## 3. Related

* **Definition:** This is a packet that is opening a *new* connection, but it is technically linked to an existing one.
* **Example:** This is common with FTP or VoIP. You might start a connection on one port (the control channel), and then the server asks to open a second port to actually transfer a file (the data channel). The firewall sees the second connection as **Related** to the first.
* **Firewall Strategy:** Like Established traffic, these are usually accepted early in the rule list to ensure complex applications don't break.

## 4. Invalid

* **Definition:** This is a packet that does not belong to any known connection and doesn't make sense in the current context.
* **Example:** A packet that claims to be part of a conversation you never started, or a packet with "impossible" flags (like a finishing packet for a connection that hasn't opened yet).
* **Firewall Strategy:** These are almost always **Dropped** immediately. They are often signs of network errors or scanning/hacking attempts.

---

### ⚠️ Note: Connection Tracking Requirements

Connection Tracking must be **enabled** to use NAT (Network Address Translation).

If Connection Tracking is **OFF**, then **no NAT will happen**.

The router requires the state table to rewrite packet headers and manage the "buffer" between overlapping networks.

---

### Why Is This Required?

In the **Src-NAT example** we discussed earlier, the router changes:

172.16.1.10 → 192.168.1.10

The router must **remember** this translation.

Without Connection Tracking:

- The router forgets the translation immediately.
- The return traffic (reply packet) will not know which internal IP to go back to.
- The connection will time out or be dropped as **Invalid**.

---

Connection Tracking is what allows the router to:

- Track active sessions
- Reverse NAT translations automatically
- Maintain proper two-way communication

Without it, Twice NAT simply cannot function.

---

By Defualt its Enabled





