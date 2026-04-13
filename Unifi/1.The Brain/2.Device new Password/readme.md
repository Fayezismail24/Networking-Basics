# 2. Device SSH Credentials After Adoption — UniFi Network Application

When a UniFi device is adopted by the Network Application, its **SSH credentials change automatically**.  
The device no longer accepts the factory default `ubnt / ubnt` login — it switches to the **site-wide SSH credentials** defined in the controller.

---

## Why the Password Changes

During adoption, the controller pushes its full site configuration to the device. Part of that configuration is the **Device SSH Authentication** settings. From that point forward, all SSH access to the device must use the controller-defined credentials, not the factory defaults.

> ⚠️ If you try to SSH into an adopted device using `ubnt / ubnt`, access will be **denied**.

---

## Where to Find the SSH Credentials

**Path:**  
`Settings → System → SSH Authentication → Device SSH Settings`

| Field | Description |
|---|---|
| **Username** | SSH username pushed to all adopted devices on this site |
| **Password** | SSH password pushed to all adopted devices on this site |

> 💡 The password field is **masked** in the UI — it does not display in plain text.  
> You must know the password you originally set. There is no "reveal" button.

---

## What to Do If You Don't Know the Password

If the SSH password was set by someone else or you've forgotten it:

1. Go to `Settings → System → SSH Authentication → Device SSH Settings`
2. **Set a new password** — this will be pushed to all adopted devices on the next provision
3. To apply immediately, go to **Devices**, select the device → click **Force Provision**
4. SSH into the device using the new credentials

> ⚠️ Changing the SSH password here affects **all adopted devices** on the site, not just one.

---

## Quick Reference

| Scenario | SSH Credentials to Use |
|---|---|
| Device is **factory default** (not yet adopted) | `ubnt / ubnt` |
| Device is **adopted** by the controller | Credentials from `Settings → System → SSH Authentication` |
| Device was **reset** after adoption | Back to `ubnt / ubnt` until re-adopted |

---

## Notes

- SSH access is typically only needed for **manual `set-inform`**, troubleshooting, or advanced configuration.
- Under normal operation, all configuration is pushed by the controller — direct SSH is not required.
- If you use **SSH keys** instead of a password, they are configured in the same `Device SSH Settings` section.
