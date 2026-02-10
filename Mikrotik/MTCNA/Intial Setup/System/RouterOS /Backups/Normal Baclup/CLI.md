

# MikroTik Backup Command

### Basic Command

```bash
[admin@MikroTik] > system/backup/save name=fayeztest
[admin@MikroTik] > system backup save name=" " 


```

**Explanation:**

* `system/backup/save` → The command to **create a full backup**
* `name=fayeztest` → The **filename** of the backup
* The file will be saved in the **router’s file list**

---

### Optional Parameters

| Option          | Example                | Description                                                |
| --------------- | ---------------------- | ---------------------------------------------------------- |
| `password=`     | `password=MySecret123` | Protects the backup with a password                        |
| `dont-encrypt=` | `dont-encrypt=no`      | Enables encryption (`no` = encrypt, `yes` = no encryption) |

**Example with password and encryption:**

```bash
[admin@MikroTik] > system/backup/save name=fayeztest password=MySecret123 dont-encrypt=no
```

**What this does:**

* Saves the backup as **fayeztest.backup**
* Requires the **password** to restore
* Encrypts the backup for security

---

### Notes

* Backup is **binary**, includes all config and passwords
* Only restore on **same device or compatible model**
* Recommended to **download the backup** to your PC after creation

```bash
[admin@MikroTik] > file print
```

* Use `file print` to **see the backup in the router file list**

