

# MikroTik Backup & Restore Commands

### 1️⃣ Save Backup

```bash
[admin@MikroTik] > system/backup/save name=fayeztest
```

**Optional Parameters:**

```bash
[admin@MikroTik] > system/backup/save name=fayeztest password=MySecret123 dont-encrypt=no
```

* `name=` → Backup filename
* `password=` → Protects backup
* `dont-encrypt=no` → Encrypts the backup

**Check backup file:**

```bash
[admin@MikroTik] > file print
```

---

### 2️⃣ Restore Backup

```bash
[admin@MikroTik] > system/backup/load name=fayeztest.backup
```

**Explanation:**

* `system/backup/load` → Command to **restore a full backup**
* `name=` → The **backup filename** to restore
* If the backup has a **password**, you will be prompted to enter it

**Example with password:**

```bash
[admin@MikroTik] > system/backup/load name=fayeztest.backup
Enter password: MySecret123
```

**What happens after restore:**

* Router **reverts to the exact state** when backup was created
* All configuration, users, and passwords are restored
* Default admin user will be replaced if it was changed in the backup

---

### Notes / Exam Tips

* Backup is **binary** → cannot edit manually
* Only restore on **same device or compatible model**
* Always **download backup to PC** for safety
* Restoring **overwrites all current configuration**

