# 2. Adopt a Device — UniFi Network Application

Adoption is the process by which the UniFi Network Application takes ownership and full management control of a UniFi device. Until a device is adopted, it is **unmanaged** — it may be online and reachable, but the controller cannot configure or monitor it.

---

## Prerequisites

Before attempting adoption, confirm the following:

- The UniFi Network Application is **running and accessible**
- The device is **powered on** and connected to the same network as the controller (Layer 2 reachability required for standard adoption)
- The device has a **valid IP address** (via DHCP or static)
- The device is running **factory default firmware** or has been **reset** (if previously adopted by another controller)
- SSH is **enabled** on the controller site:  
  `Settings → System → Advanced → Device SSH Authentication`  
  (Set a username and password — you will need this for manual/SSH adoption)

> ⚠️ If the device was previously adopted by a **different controller**, it will show as **"Managed by Other"** and cannot be adopted until it is factory reset.

---

## Adoption Methods

### Method 1 — Auto-Discovery (Same L2 Network)

This is the standard method when the controller and the device are on the **same subnet**.

1. Open the **UniFi Network Application**
2. Go to **Devices** (left sidebar)
3. The device will appear with the status **"Pending Adoption"**
4. Click the device → click **Adopt**
5. Wait for the device to go through:  
   `Adopting → Provisioning → Connected`

Done. The controller now manages the device.

---

### Method 2 — Layer 3 Adoption (Different Subnet / Remote Site)

Use this when the device is on a **different subnet** than the controller and cannot be auto-discovered.

#### Option A — Set Inform URL via SSH

1. SSH into the device using its IP address:
   ```
   ssh ubnt@<device-ip>
   ```
   Default credentials: `ubnt / ubnt`  
   Post-adoption credentials: whatever is set under `Settings → System → SSH Authentication`

2. Set the inform URL to point to your controller:
   ```
   set-inform http://<controller-ip>:8080/inform
   ```

3. The device will appear in the controller UI as **"Pending Adoption"**

4. Click **Adopt** in the controller

5. Run `set-inform` a second time if it does not connect automatically after the first adoption click:
   ```
   set-inform http://<controller-ip>:8080/inform
   ```

> 💡 The second `set-inform` is often required — the first one registers the device, the second one completes the handshake.

#### Option B — DHCP Option 43

Configure your DHCP server to push **Option 43** with the controller's inform URL. Supported on most enterprise DHCP servers (Windows Server DHCP, MikroTik, etc.).

- Value format: `https://<controller-ip-or-hostname>:8443/inform`
- Devices will automatically send their inform to this address on boot

---

### Method 3 — UniFi OS Console Discovery

If you are using a **UDM, UDM Pro, UDM SE, or CloudKey**, devices connected to its ports may be discovered and adopted directly through the UniFi OS interface without needing manual intervention.

1. Log in to the **UniFi OS portal** (typically `https://192.168.1.1`)
2. Open the **Network** application
3. Navigate to **Devices**
4. Pending devices connected to the console's switch ports will auto-appear

---

## Adoption Status Reference

| Status | Meaning |
|---|---|
| **Pending Adoption** | Device discovered, waiting for you to adopt |
| **Adopting** | Controller is sending configuration to the device |
| **Provisioning** | Device is applying the configuration |
| **Connected** | Fully adopted and managed |
| **Managed by Other** | Device belongs to a different controller — reset required |
| **Isolated** | Device adopted but cannot reach the controller |
| **Updating** | Firmware update in progress |

---

## Troubleshooting

### Device not appearing in Pending Adoption

- Confirm the device has an IP (check your DHCP leases or connect a monitor/console)
- Confirm the device and controller are on the **same VLAN/subnet** (or use L3 adoption)
- Try a **factory reset** — hold the reset button for 10 seconds until the LED cycles
- Confirm the controller is **reachable on port 8080** from the device's subnet

### Device stuck on "Adopting" or "Provisioning"

- SSH into the device and run `set-inform` manually (see Method 2 above)
- Check that **firewall rules** are not blocking TCP 8080 or 8443 between the device and controller
- Restart the device and wait 60–90 seconds before checking status again

### "Managed by Other" error

The device still holds the inform URL and credentials of a previous controller.

**Fix:**
1. Factory reset the device (hold reset button ~10 sec)
2. Re-adopt using any method above

### Device disconnects after adoption (goes to "Isolated")

- The device cannot reach the controller's inform URL after adoption
- Check routing between the device's VLAN and the controller's IP
- Verify the controller is running and accessible on port **8080** (HTTP inform)

---

## Notes

- **HTTPS Inform (port 8443)** is used when the controller has a valid SSL certificate. For self-hosted controllers without a cert, stick to **HTTP port 8080**.
- After adoption, the device will automatically keep checking in with the controller and receive any configuration pushes.
- Devices can be **forgotten** (un-adopted) from the controller UI — this does not factory reset the device, but it will return to "Pending Adoption" if still reachable.
