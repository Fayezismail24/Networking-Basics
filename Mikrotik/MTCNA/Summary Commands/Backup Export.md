
### **Backup**

```bash
/system backup save name=GTA.backup
/system backup load name=GTA.backup

/system backup save name=GTA.backup password=MySecret123 dont-encrypt=no

```

### **Export**

```bash
/system export file=GTA
/system export file=GTA section=interface
/ import file=GTA.rsc
