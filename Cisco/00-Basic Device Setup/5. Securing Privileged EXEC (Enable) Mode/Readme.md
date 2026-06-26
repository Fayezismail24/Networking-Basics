This is the most important password — it controls full access to the device.

### Option A – `enable password` (Plaintext – NOT recommended)

```bash
R1(config)# enable password cisco
```

> ⚠️ Stored in plaintext in the config. Avoid in production.

### Option B – `enable secret` (MD5 Hashed – Recommended)

```bash
R1(config)# enable secret Str0ng@Pass!
```

> ✅ Always prefer `enable secret` over `enable password`.  
> If both are configured, `enable secret` takes ownerships.

---
