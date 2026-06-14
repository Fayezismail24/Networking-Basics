By default, most passwords (console, vty, enable password) appear in **plaintext** in `show running-config`

Fix this with:

```bash
R1(config)# service password-encryption
```

> This uses a weak **Type 7** encryption — not cryptographically strong, but prevents casual shoulder-surfing.  
> `enable secret` uses **Type 5 (MD5)** regardless of this command.

---
