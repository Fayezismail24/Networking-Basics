## What is Netinstall in MikroTik?

**Netinstall** is a **MikroTik recovery and installation tool** used to:

* Install RouterOS from scratch
* Reinstall RouterOS if the router is broken
* Recover a router that does not boot
* Reset a router when you cannot access it

It works over **Ethernet**, not Wi-Fi.

---

## When do we use Netinstall?

You use **Netinstall** when:

* RouterOS is **corrupted**
* You **forgot the admin password**
* The router is **bootlooping**
* The router does not appear in **Winbox**
* You want a **clean OS reinstall**

👉 Think of it like **formatting Windows using a USB**, but for MikroTik.

---

## How Netinstall works (simple flow)

1. Install **Netinstall** on your PC
2. Download the **RouterOS package (.npk)**
3. Connect PC to MikroTik via **Ethernet**
4. Set a **temporary IP** on your PC
5. Put the router into **Netinstall (Ethernet boot) mode**
6. Netinstall detects the router
7. Install RouterOS

---

## Key requirements

* **Ethernet cable only**
* PC and MikroTik must be on the **same subnet**
* Firewall on PC must be **disabled** (very important)
* Router must support **Ethernet boot**

---

## How to put MikroTik into Netinstall mode

Common method:

1. Power off the router
2. Press and hold **RESET**
3. Power on the router
4. Keep holding RESET until:

   * ACT LED flashes
   * or beep sound (depends on model)
5. Release RESET

Now the router is waiting for Netinstall.

---

## Important exam points (MTCNA)

* Netinstall uses **Ethernet**, not wireless
* Used for **recovery and reinstall**
* Requires **Netinstall software**
* Router boots from **network**
* Works at a **very low level (before RouterOS loads)**

---


---

## Netinstall can be used to…

### 1️⃣ Install package for different hardware architecture

❌ **FALSE**

* Each MikroTik device has a **fixed CPU architecture** (MIPSBE, SMIPS, ARM, ARM64, etc.)
* You **cannot** install RouterOS for a different architecture
* Netinstall will **not allow it**

👉 Example: You cannot install ARM RouterOS on a MIPS device.

---

### 2️⃣ Reinstall software without losing licence

✅ **TRUE**

* The **license is stored in the router hardware**
* Netinstall **does NOT remove the license**
* After reinstall, the same license level remains

👉 Very important MTCNA point.

---

### 3️⃣ Keep configuration, but reset a lost admin password

❌ **FALSE**

* Netinstall **wipes the configuration**
* You cannot keep config and just reset the password
* It is a **clean install**

👉 If config is kept, password stays. If password is reset, config is gone.

---

### 4️⃣ Install different software version (upgrade or downgrade)

✅ **TRUE**

* Netinstall allows:

  * Upgrade
  * Downgrade
  * Install a specific RouterOS version

👉 Useful when a new version is buggy.

---

## Final exam-ready summary

| Statement                                           | Correct |
| --------------------------------------------------- | ------- |
| Install package for different hardware architecture | ❌       |
| Reinstall software without losing licence           | ✅       |
| Keep configuration but reset admin password         | ❌       |
| Install different software version                  | ✅       |



* Compare **Netinstall vs Reset Configuration**
* Give you **step-by-step Netinstall lab**
* Tell you **common Netinstall mistakes in the exam**

Just say the word, Boss 💪
