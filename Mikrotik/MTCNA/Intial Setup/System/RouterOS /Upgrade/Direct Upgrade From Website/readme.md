# Upgrading MikroTik RouterOS from the MikroTik Website

To upgrade your **MikroTik RouterOS** from the MikroTik website, follow these steps:

## 1. Visit the MikroTik Website
- Go to the official **MikroTik website** for downloading the latest RouterOS version:
  - [MikroTik Downloads Page](https://mikrotik.com/download)

## 2. Select Your RouterOS Version
- Scroll down to the **RouterOS** section.
- Choose the appropriate **RouterOS version** for your device. Make sure to select the correct **architecture** (e.g., **MIPSBE**, **x86_64**, **ARM**, etc.) depending on your hardware.

## 3. Download the Latest Version
- Click on the **"Download"** button next to the version you want to install. The file will be in a `.npk` format, which is used to install RouterOS.

## 4. Upload the File to Your Router
- **Option 1:** **Winbox**  
  - Open **Winbox** and log in to your MikroTik router.
  - Go to **Files** in the left menu.
  - Drag and drop the downloaded `.npk` file into the Winbox window.

- **Option 2:** **FTP (or SCP)**  
  - Use an FTP client (e.g., FileZilla) or SCP to upload the `.npk` file directly to your MikroTik router.

## 5. Install the Update
- After uploading the `.npk` file, you need to **reboot the router** to apply the update.
- To reboot the router, you can either:
  - Go to **System > Reboot** in Winbox.
  - Or run the following command in the **CLI**:
    ```bash
    /system reboot
    ```

## 6. Verify the Upgrade
- Once the router reboots, verify the upgrade by checking the RouterOS version:
  - Open **Winbox** or the **CLI** and run:
    ```bash
    /system resource print
    ```
  - You should see the updated version listed in the output.

---

## Additional Notes:
- **Backup your configuration** before upgrading, as sometimes upgrades can cause unexpected issues or require resets. Use the **Backup** feature in Winbox or via the CLI:
  ```bash



  /system backup save name=backup_before_upgrade

<img width="1919" height="1020" alt="image" src="https://github.com/user-attachments/assets/22affa74-90ea-434e-a8b6-b1afe096404a" />


<img width="579" height="37" alt="image" src="https://github.com/user-attachments/assets/cf3d489f-8136-40f1-8dcf-d71131b58a35" />



<img width="1895" height="913" alt="image" src="https://github.com/user-attachments/assets/3ba584f6-574b-4eb0-a016-07da1c61578f" />


