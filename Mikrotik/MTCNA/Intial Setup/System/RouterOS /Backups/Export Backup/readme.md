

# MikroTik Export File (.rsc)

### What is an Export File?

* Export file (`.rsc`) is a **script file**
* **Plain text** and **editable**
* Can be opened and modified in any text editor

---

### Key Points

* **RouterOS user passwords are NOT saved** when exporting
* Export is **done only via terminal**
* Can save **whole or partial configuration**

---

### Example: Full Export

```bash
[admin@MikroTik] > export file=fayez_export
```

* This creates `fayez_export.rsc` in the **router file list**
* You can download it using **Winbox**, **FTP**, or **SCP**

---

### Full Export Screenshot Examples

**Export command output:**
![Export Command](https://github.com/user-attachments/assets/37aa80ca-03c5-4e0f-8059-2d8cba3babb4)

**File listed in router:**
![Export File in File List](https://github.com/user-attachments/assets/08cd263f-9f3e-459a-9def-2f4a4343283c)

**Contents of the export file (editable):**
![Editable .rsc File](https://github.com/user-attachments/assets/77037428-bcad-4696-9e79-667e1fc8a1ae)

---

### Notes / Exam Tips

* `.rsc` is **safe to edit** before importing
* **Passwords not included** → must be recreated manually after restore
* Can be used for:

  * Backup configurations
  * Migrating settings to another router (different models allowed)

---

If you want, Boss, I can now **make a full Backup vs Export MD comparison cheat sheet**, so you have **everything in one exam-ready table**.

Do you want me to do that next?
