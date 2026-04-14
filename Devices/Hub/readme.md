

## 📌 Overview

A **network hub** is a basic networking device used to connect multiple computers in a network. It operates at **Layer 1 (Physical Layer)** of the OSI model.

Unlike modern devices, a hub does not filter or manage traffic—it simply broadcasts incoming data to all connected devices.

---

## ⚙️ How It Works

When a device sends data to the hub:

1. The hub receives the signal
2. It repeats (broadcasts) the signal to all ports
3. Every connected device receives the data
4. Only the intended recipient processes it

---

## 🧠 Key Characteristics

* Works at Physical Layer (Layer 1)
* No MAC address filtering
* Broadcasts data to all devices
* Half-duplex communication
* Simple and low cost

---

## 📊 Hub vs Switch

| Feature       | Hub                | Switch                 |
| ------------- | ------------------ | ---------------------- |
| OSI Layer     | Layer 1 (Physical) | Layer 2 (Data Link)    |
| Data Handling | Broadcast          | Intelligent forwarding |
| Performance   | Slower             | Faster                 |
| Security      | Low                | Higher                 |

---

## 🖼️ Diagram

```
   PC1     PC2     PC3
    |       |       |
     \      |      /
        [ HUB ]
           |
         PC4
```

---

## 📦 Use Cases

* Small or temporary networks
* Learning and lab environments
* Legacy systems

---

## ⚠️ Limitations

* Network collisions
* Poor performance
* No traffic management
* Not used in modern networks
