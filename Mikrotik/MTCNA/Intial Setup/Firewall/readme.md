

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

### Why this matters

Using these states allows you to create a very efficient "Fast Path" for your network. By accepting **Established** and **Related** traffic at the top of your rule list, the router doesn't have to check every single packet against every single rule—it just checks its memory, sees it's a known conversation, and lets it through.

