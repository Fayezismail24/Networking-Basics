
### **Backup**

```bash
/system backup save name=GTA.backup
/system backup load name=GTA.backup

/system backup save name=GTA.backup password=MySecret123 dont-encrypt=no
/system/backup/load name=fayezzz.backup password=123

```

### **Export**

```bash
/system export file=GTA
/ import file-name=GTA.rsc
```

### **Partial Export **
```bash
ip address export file="132"
import file-name=132.rsc
