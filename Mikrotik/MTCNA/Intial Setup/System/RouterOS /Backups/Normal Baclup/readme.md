

# MikroTik Backup File (Backup)

## What is a MikroTik Backup File?

A **MikroTik backup file** is a **binary file** that contains a **full snapshot** of the router configuration, including:

* All system and interface settings
* Firewall, routing, wireless, queues, etc.
* User accounts
* **Sensitive data such as passwords**

This backup represents the **exact state of the router** at the moment the backup was created.

---

## Backup Restore Compatibility

* A backup file can be restored **only** on:

  * The **same device**
  * Or a **compatible MikroTik router**
* ❌ Restoring between **different models** is not supported
  Example:

  * hAP → hEX ❌ (will not work)

> Always restore backups on the same model to avoid errors.

---

## Security Options

When creating a backup, you can:

* 🔐 Set a **password** on the backup file
* 🔒 Enable **encryption** for additional security

These options protect the backup from unauthorized access.

---

## Backup Creation Examples

![Backup Step 1](https://github.com/user-attachments/assets/cf172dd0-34a6-4d3e-b42f-7429f1d017ac)

![Backup Step 2](https://github.com/user-attachments/assets/0a99e7e8-1fe4-4463-a8c8-7dd7b67c0d0c)

![Backup Step 3](https://github.com/user-attachments/assets/17c1ae7e-181e-4434-8feb-7de77eb06aff)

![Backup Step 4](https://github.com/user-attachments/assets/1418c9e9-b906-4e1e-8877-401c5fc05993)

---

## Important Exam Notes (MTCNA)

* Backup files are **binary** and **not editable**
* They include **passwords and sensitive data**
* Best practice: use **password + encryption**
* Use backups for **full recovery**, not migration
