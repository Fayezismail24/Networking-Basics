## Netinstall vs Reset Configuration

### Netinstall

**What it is**

* A **PC-based recovery tool**
* Reinstalls **RouterOS from scratch** over Ethernet

**What it does**

* Reinstall RouterOS
* Recover a non-booting router
* Remove **all configuration**
* Reset lost passwords
* Upgrade or downgrade RouterOS version

**What it keeps**

* ✅ License
* ❌ Configuration

**When to use**

* Router does not boot
* RouterOS is corrupted
* Forgotten admin password and router is inaccessible
* Winbox cannot detect the router

**Requirements**

* PC with Netinstall
* Ethernet connection
* Router in Netinstall mode

---

### Reset Configuration

**What it is**

* A **local reset** function inside RouterOS or via reset button

**What it does**

* Deletes configuration
* Resets users and passwords
* Keeps installed RouterOS

**What it keeps**

* ✅ License
* ❌ Configuration
* ✅ RouterOS version

**When to use**

* Router boots normally
* You still have access or can use reset button
* You want to start fresh without reinstalling OS

**Requirements**

* No PC needed
* Router must boot

---

| Feature / Action                            | Netinstall | Reset Configuration      |
| ------------------------------------------- | ---------- | ------------------------ |
| Requires PC                                 | ✅          | ❌                        |
| Reinstalls RouterOS                         | ✅          | ❌                        |
| Works if router won’t boot                  | ✅          | ❌                        |
| Removes configuration                       | ✅          | ✅                        |
| Deletes users & passwords                   | ✅          | ✅                        |
| Restores default admin (no password)        | ✅          | ✅                        |
| Keeps license                               | ✅          | ✅                        |
| Change RouterOS version (upgrade/downgrade) | ✅          | ❌                        |
| Keeps installed packages                    | ❌          | ✅                        |
| Choose which packages to install            | ✅          | ❌                        |
| Reset lost password                         | ✅          | ✅ (only if router boots) |


Both Netinstall and Reset Configuration:

❌ Delete all users

❌ Delete all passwords

✅ Restore the default admin user

## Key exam traps ⚠️

* ❌ **Reset Configuration does NOT reinstall RouterOS**
* ❌ **Netinstall does NOT keep configuration**
* ✅ **Both keep the license**
* ✅ **Only Netinstall can recover a dead router**

---

## One-line exam answers

* **Reset Configuration**: Removes config only, RouterOS stays.
* **Netinstall**: Reinstalls RouterOS and removes everything except license.

---

## Devil’s advocate (quick check)

If someone says:

> “Why not always use Netinstall?”

Answer:

* Slower
* Needs PC
* Not needed if router boots normally

