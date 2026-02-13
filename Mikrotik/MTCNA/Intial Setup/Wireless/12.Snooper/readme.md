In MikroTik RouterOS, the **Wireless Snooper** is an advanced diagnostic tool used to analyze the radio frequency (RF) environment. Unlike a standard "Scan," which only displays available Access Points (APs), Snooper provides a deep-dive analysis of traffic, noise, and channel congestion.

Based on your uploaded photos, here is a full explanation of the tool and its columns.

---

### 📡 What Snooper Does

The Snooper tool monitors all wireless activity on a selected interface. It is primarily used to:

* Identify the "quietest" channel for your AP.
* Detect non-WiFi interference or hidden traffic.
* Monitor real-time bandwidth usage of neighboring networks.

> **Important Note:** Running Snooper **disconnects** your wireless link because the radio must "hop" between frequencies to listen to the entire spectrum.

---

### 📊 Column-by-Column Explanation

Referring to the data in your screenshots (e.g., `image_c26219.png`), here is what each field represents:

| Column Name | Explanation | Why it Matters |
| --- | --- | --- |
| **Channel** | Displays the Frequency (e.g., `2412`), Channel Width (`20`), and Protocol (`gn`). | Helps you identify exactly which part of the spectrum is being analyzed. |
| **(Noise Floor)** | Found in parentheses inside the Channel column (e.g., `-108dBm` in your photo). | This is the background "static." **A lower number (more negative) is better.** -108dBm is excellent; -85dBm is very noisy. |
| **Address** | The MAC address (BSSID) of the hardware detected. | Uniquely identifies the physical device transmitting on that frequency. |
| **SSID** | The name of the WiFi network (e.g., `Electro Tabkh`, `Noor`). | Helps you correlate signal interference with a specific neighbor. |
| **Signal** | The strength of the signal from that specific device (e.g., `-82`). | Shows how "loudly" that neighbor is speaking at your location. |
| **Of Freq (%)** | **Occupancy of Frequency.** The percentage of time the channel is busy with *any* RF energy. | If this is high (e.g., >15%), the channel is crowded and will be slow, even if the signal is strong. |
| **Of Traf (%)** | **Occupancy of Traffic.** The percentage of time the channel is specifically carrying 802.11 WiFi data. | If Freq % is high but Traf % is low, you have non-WiFi interference (like a microwave). |
| **Bandwidth** | The real-time data rate being consumed by that device (e.g., `225.8 kbps`). | Shows if a neighbor is currently using the channel for a heavy download or stream. |
| **Networks** | The number of unique WiFi networks found on that specific frequency. | A high number means many routers are fighting for the same "airtime." |
| **Stations** | The number of client devices (phones, laptops) connected to that AP. | More stations on a channel increase the chance of packet collisions and lag. |
