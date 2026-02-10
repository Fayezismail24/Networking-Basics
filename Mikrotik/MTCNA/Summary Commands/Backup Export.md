
### **Backup**

```bash
/system/backup/save name=GTA
/system/backup/save name=f\GTA password=MySecret123 dont-encrypt=no
/system/backup/load name=GTA.backup
```

### **Export**

```bash
/export file=fGTA
/export file=GTA section=interface
/import file=GTA.rsc
