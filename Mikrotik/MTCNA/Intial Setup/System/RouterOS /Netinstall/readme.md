

# MikroTik Netinstall Step-by-Step (MD)

## 1. Identify Router Architecture

* Go to **mikrotik.com → Products**
* Search for the router you have
  Example: **hAP Series**
* Open the product page
* **Note the Architecture** (MIPSBE, ARM, ARM64, etc.)

![Router Architecture](https://github.com/user-attachments/assets/7907ebe0-cc18-483d-a443-d2efa28abad2)

---

## 2. Download RouterOS Packages

* Go to **mikrotik.com → Software**
* Under **RouterOS main packages**
* Download the package that matches:

  * Your **RouterOS version**
  * Your **hardware architecture**

![RouterOS Packages](https://github.com/user-attachments/assets/16eb510c-7fc0-4301-afa3-44fa5522c652)

---

## 3. Download Netinstall

* From the same **Software** page
* Download **Netinstall** for your operating system (Windows)

---

## 4. Prepare the PC Network

* Disable **ALL network adapters** on the PC

  * Wi-Fi
  * VPN
  * Virtual adapters
* Keep **ONLY Ethernet enabled**

![Disable NICs](https://github.com/user-attachments/assets/eca1e166-75b2-4aab-8d05-4d9ada0dd5c3)

---

## 5. Set Static IP on Ethernet

* Set a **static IP** on the Ethernet adapter
  Example:

  * IP: `192.168.88.2`
  * Mask: `255.255.255.0`
  * Gateway: empty

![Static IP](https://github.com/user-attachments/assets/6840c94c-6515-4673-9623-22e5e763b128)

---

## 6. Open Netinstall

* Run **Netinstall as Administrator**
* Do **NOT** connect power to the router yet

---

## 7. Cable Setup

* Remove **ALL cables** from the router
* Connect **ONLY**:

  * PC Ethernet → Router **ether1**
* ⚠️ **CCR & RB1xxx series**:

  * Use the **LAST Ethernet port**

---

## 8. Enter Netinstall Mode

1. Press and hold the **RESET** button
2. Plug in the **power cable**
3. Keep holding RESET for:

   * **5 seconds** → Reset configuration
   * **10 seconds** → CAP mode (Access Points)
   * **15 seconds** → **Netinstall mode**
4. Release RESET

---

## 9. Enable Net Booting

* In Netinstall:

  * Enable **Net booting**
  * Set boot server IP (PC IP)

![Net Booting](https://github.com/user-attachments/assets/a8edc7ee-1d82-4545-9e27-3a22220e5db1)

---

## 10. Router Detection

* Router should appear automatically in Netinstall

![Router Detected](https://github.com/user-attachments/assets/90ce149a-8343-4fad-ac6e-8aa30e2627f4)

---

## 11. Select RouterOS Package

* Click **Browse**
* Select the downloaded **.npk** file

![Select File](https://github.com/user-attachments/assets/5e64c560-b783-4490-9ed3-9d4ee3954a17)

---

## 12. Install RouterOS

* Click **Install**
* Wait until installation finishes
* Router will reboot automatically

![Install](https://github.com/user-attachments/assets/8f521d21-2622-4e91-9f69-e9f26da0228e)

---

## Final Notes (Exam & Real Life)

* License is **NOT lost**
* Configuration is **deleted**
* Default user after install:

  * `admin` with **no password**

If you want next, I can:

* Turn this into a **one-page Netinstall cheat sheet**
* Add **common Netinstall errors and fixes**
* Rewrite it to be **MTCNA lab instructions**

Just tell me, Boss 💪
