
## MikroTik Recovery & Configuration Comparison

| Feature / Action                          | Backup (.backup)                            | Export (.rsc)                                 | Reset Configuration                               | Netinstall                                                 |
| ----------------------------------------- | ------------------------------------------- | --------------------------------------------- | ------------------------------------------------- | ---------------------------------------------------------- |
| File Type                                 | Binary                                      | Script / Plain text                           | N/A                                               | N/A                                                        |
| Editable                                  | ❌                                           | ✅                                             | ❌                                                 | ❌                                                          |
| Includes full configuration               | ✅                                           | ✅ (except passwords)                          | ❌                                                 | ❌                                                          |
| Includes users                            | ✅                                           | ✅ (passwords NOT included)                    | ❌ (all users deleted)                             | ❌ (all users deleted)                                      |
| Includes passwords                        | ✅                                           | ❌                                             | ❌                                                 | ❌                                                          |
| Keeps license                             | ✅                                           | ✅                                             | ✅                                                 | ✅                                                          |
| Keeps installed packages                  | ✅                                           | ✅                                             | ✅                                                 | ❌                                                          |
| Can restore to same device                | ✅                                           | ✅                                             | ✅                                                 | ✅                                                          |
| Can restore to different compatible model | ❌                                           | ✅                                             | ❌                                                 | ✅ (if hardware architecture matches)                       |
| Reinstalls RouterOS                       | ❌                                           | ❌                                             | ❌                                                 | ✅                                                          |
| Works if router won’t boot                | ❌                                           | ❌                                             | ❌                                                 | ✅                                                          |
| Password protection                       | ✅                                           | ✅                                             | N/A                                               | N/A                                                        |
| Encryption                                | ✅                                           | ✅                                             | N/A                                               | N/A                                                        |
| How to create                             | GUI / Terminal                              | Terminal only                                 | Reset button / System → Reset                     | PC + Netinstall tool                                       |
| Notes / Exam Tips                         | Full snapshot, safest for complete recovery | Script, editable, passwords must be recreated | Soft reset, config wiped but OS + packages remain | Nuclear option, OS + config + packages wiped, license kept |

---

### Key Exam Takeaways

1. **Backup** → safest, restores everything, including users and passwords.
2. **Export** → editable script, passwords NOT saved, good for migration.
3. **Reset Configuration** → wipes config and users, keeps OS + packages + license.
4. **Netinstall** → wipes everything, reinstalls OS, keeps license, works if router dead.
