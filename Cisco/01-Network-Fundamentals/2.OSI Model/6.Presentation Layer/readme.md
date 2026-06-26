

# Presentation Layer (OSI Layer 6)

## What is the Presentation Layer?

The Presentation Layer is the sixth layer of the OSI model.
It sits between the Session Layer (Layer 5) and the Application Layer (Layer 7).

Its job is to ensure that data sent by one application can be
read and understood by another application on a different system.
It handles how data is formatted, encoded, encrypted, and compressed
before it is handed to the Application Layer.

Think of Layer 6 as a translator — it makes sure both sides
speak the same language regardless of the underlying system or platform.

---

## Responsibilities

- Data translation — converting data between different formats
- Encoding — defining how characters and data are represented in binary
- Encryption and decryption — securing data before transmission
- Compression and decompression — reducing data size for efficient transfer
- Serialization — converting data structures into a format suitable for transmission

---

## Data Translation

Different systems may represent data differently.
Layer 6 ensures both sides agree on the format.

| Scenario | Layer 6 Role |
|----------|-------------|
| Windows to Linux file transfer | Converts line endings (CRLF ↔ LF) |
| Different character sets | Translates between ASCII, EBCDIC, Unicode |
| Big-endian to little-endian | Converts byte order between systems |
| Integer representation | Normalizes signed/unsigned integer formats |

---

## Character Encoding

Character encoding defines how text characters are represented as binary.

| Encoding | Description | Use Case |
|----------|-------------|----------|
| ASCII | 7-bit — 128 characters | English text, legacy systems |
| Extended ASCII | 8-bit — 256 characters | Western European characters |
| EBCDIC | IBM mainframe encoding | Legacy IBM systems |
| UTF-8 | Variable length — 1 to 4 bytes | Most common on the internet today |
| UTF-16 | 2 or 4 bytes per character | Windows internals, Java |
| UTF-32 | Fixed 4 bytes per character | Rare — high memory usage |
| Unicode | Universal standard — defines code points for all characters | Basis for UTF-8, UTF-16, UTF-32 |

> UTF-8 is backward compatible with ASCII.
> The first 128 UTF-8 code points are identical to ASCII.
> UTF-8 is the dominant encoding standard on the modern web.

---

## Data Formats Handled at Layer 6

The Presentation Layer defines and interprets many common data formats.

### Text and Markup

| Format | Description |
|--------|-------------|
| ASCII / UTF-8 | Plain text |
| HTML | Web page markup |
| XML | Structured data exchange |
| JSON | Lightweight data interchange — APIs and web services |
| CSV | Comma-separated values — tabular data |
| YAML | Human-readable configuration format |

### Media

| Format | Type | Description |
|--------|------|-------------|
| JPEG | Image | Lossy compressed image |
| PNG | Image | Lossless compressed image |
| GIF | Image | Lossless, supports animation |
| MPEG | Video | Compressed video format |
| MP4 | Video | Container for video and audio |
| MP3 | Audio | Compressed audio |
| WAV | Audio | Uncompressed audio |

### Application Data

| Format | Description |
|--------|-------------|
| XDR (External Data Representation) | Standard for data exchange between different architectures |
| ASN.1 (Abstract Syntax Notation) | Used in SNMP, LDAP, X.509 certificates |
| Protocol Buffers (protobuf) | Google's binary serialization format |
| MessagePack | Binary JSON alternative |

---

## Encryption and Decryption

One of the most important Layer 6 functions in modern networking
is encryption — protecting data so only the intended recipient can read it.

### Symmetric Encryption

Both sides use the same key to encrypt and decrypt.

| Algorithm | Key Size | Description |
|-----------|----------|-------------|
| AES-128 | 128 bits | Fast and secure — used in WPA2, TLS |
| AES-256 | 256 bits | Higher security — used in VPNs, government |
| DES | 56 bits | Legacy — broken, do not use |
| 3DES | 112/168 bits | Legacy — being phased out |
| ChaCha20 | 256 bits | Fast on mobile — used in TLS 1.3 |

> AES (Advanced Encryption Standard) is the dominant symmetric cipher today.
> DES and 3DES are legacy — avoid in any new deployment.

### Asymmetric Encryption

Uses a key pair — public key to encrypt, private key to decrypt.

| Algorithm | Key Size | Description |
|-----------|----------|-------------|
| RSA | 2048+ bits | Most widely used — TLS certificates, SSH |
| ECC (Elliptic Curve) | 256 bits | Smaller keys, same strength as RSA 3072 |
| Diffie-Hellman | Variable | Key exchange — not encryption itself |
| ECDH | Variable | Elliptic Curve Diffie-Hellman — used in TLS 1.3 |

> Asymmetric encryption is used to exchange keys securely.
> Symmetric encryption is used for the actual data transfer — it is much faster.

### Hashing — Data Integrity

Hashing is not encryption — it is a one-way function used to
verify data integrity.

| Algorithm | Output Size | Description |
|-----------|-------------|-------------|
| MD5 | 128 bits | Legacy — broken for security use, still used for checksums |
| SHA-1 | 160 bits | Legacy — deprecated for security use |
| SHA-256 | 256 bits | Current standard — used in TLS, certificates, IPSec |
| SHA-384 | 384 bits | Higher security variant |
| SHA-512 | 512 bits | Highest standard variant |
| HMAC | Variable | Hash-based Message Authentication Code — adds a secret key |

> Hashing verifies that data has not been tampered with.
> Even a one-bit change in the input produces a completely different hash.

---

## TLS — Where Layer 6 Lives in the Real World

TLS (Transport Layer Security) is the clearest real-world example
of Layer 6 in action. It provides encryption, authentication,
and data integrity for HTTPS and many other protocols.

### TLS Handshake (TLS 1.3 Simplified)

```
Client                                  Server
  │                                       │
  │ ── ClientHello ─────────────────────► │   Supported cipher suites, TLS version
  │ ◄── ServerHello ─────────────────────  │   Chosen cipher suite
  │ ◄── Certificate ─────────────────────  │   Server's public key + identity
  │ ◄── ServerHelloDone ─────────────────  │
  │                                       │
  │ ── Key Exchange ────────────────────► │   Encrypted pre-master secret
  │ ◄── Session Keys Derived ────────────  │   Both sides derive symmetric keys
  │                                       │
  │ ── Finished ────────────────────────► │   Encrypted with session key
  │ ◄── Finished ────────────────────────  │   Verified
  │                                       │
  │ ════ Encrypted Application Data ══════│   HTTPS traffic
```

| TLS Component | Layer 6 Function |
|---------------|-----------------|
| Certificate (X.509) | Authentication and public key exchange |
| Cipher suite negotiation | Agreeing on encoding and encryption algorithms |
| Session key derivation | Generating symmetric keys from the handshake |
| Record encryption | Encrypting and decrypting application data |
| MAC / HMAC | Ensuring data integrity per record |

### Common TLS Cipher Suite Example

```
TLS_AES_256_GCM_SHA384
│   │           │
│   │           └── SHA384 — integrity / hashing
│   └────────────── AES-256-GCM — symmetric encryption
└────────────────── TLS — protocol
```

---

## Compression

Layer 6 can compress data before transmission to reduce bandwidth usage.

| Algorithm | Description | Use Case |
|-----------|-------------|----------|
| GZIP | Deflate-based compression | HTTP content encoding — most common |
| Deflate | ZIP compression algorithm | HTTP, PNG images |
| Brotli | Google compression — better ratio than GZIP | HTTPS web traffic |
| LZ77 / LZ78 | Base for many modern algorithms | General purpose |
| Zstandard (zstd) | Fast with high compression ratio | Modern applications |

> HTTP/HTTPS uses GZIP or Brotli to compress HTML, CSS, and JS before sending.
> The server compresses — the client decompresses — both at Layer 6.

---

## Serialization

Serialization converts in-memory data structures into a transmittable format.

```
Application object:
{
  "name": "Fayez",
  "role": "IT Manager",
  "certified": true
}

Serialized (JSON over HTTPS):
7b 22 6e 61 6d 65 22 3a 22 46 61 79 65 7a 22 ...  (UTF-8 encoded bytes)

Deserialized at destination:
Back to the original object in the receiving application
```

| Format | Type | Used In |
|--------|------|---------|
| JSON | Text | REST APIs, web services |
| XML | Text | SOAP, configuration files |
| Protocol Buffers | Binary | gRPC, Google services |
| MessagePack | Binary | High-performance APIs |
| ASN.1 / DER | Binary | X.509 certificates, SNMP, LDAP |

---

## X.509 Certificates

X.509 is the standard format for digital certificates used in TLS.
It is encoded using ASN.1 — a Layer 6 data format.

| Field | Description |
|-------|-------------|
| Version | Certificate format version (v3 is current) |
| Serial Number | Unique identifier issued by the CA |
| Signature Algorithm | Algorithm used to sign the certificate (e.g. SHA256withRSA) |
| Issuer | Certificate Authority (CA) that signed it |
| Validity | Not Before / Not After dates |
| Subject | Entity the certificate belongs to (domain, organization) |
| Public Key | RSA or ECC public key |
| Extensions | SANs (Subject Alternative Names), key usage, etc. |
| Signature | CA's digital signature over the certificate |

---

## Presentation Layer in the TCP/IP Model

The TCP/IP model does not have a dedicated Presentation Layer.
Its functions are absorbed into the Application Layer.

| OSI Layer | TCP/IP Layer | Where Layer 6 Lives Today |
|-----------|-------------|--------------------------|
| Layer 7 — Application | Application | HTTP, FTP, DNS, SMTP |
| Layer 6 — Presentation | Application | TLS, encoding, compression, serialization |
| Layer 5 — Session | Application | SIP, NetBIOS, TLS session |

> On the CCNA exam, OSI Layer 6 is tested conceptually.
> Understand what it does — not where to find a Layer 6 header in Wireshark.

---

## Layer 6 in the Context of the OSI Model

| Layer | Name | PDU | Key Function |
|-------|------|-----|-------------|
| Layer 7 | Application | Data | User-facing services and protocols |
| Layer 6 | Presentation | Data | Encoding, encryption, compression, translation |
| Layer 5 | Session | Data | Session setup, maintenance, termination |
| Layer 4 | Transport | Segment / Datagram | End-to-end delivery, port numbers |
| Layer 3 | Network | Packet | IP addressing, routing |
| Layer 2 | Data Link | Frame | MAC addressing, framing |
| Layer 1 | Physical | Bits | Signals, cables, connectors |

---

## Summary

- Layer 6 translates data between different formats so applications can understand each other
- Character encoding defines how text is represented — UTF-8 is the modern standard
- Encryption secures data in transit — TLS is the dominant Layer 6 security mechanism
- AES is the standard symmetric cipher — RSA and ECC handle asymmetric key exchange
- Hashing verifies data integrity — SHA-256 is the current standard
- Compression reduces data size — GZIP and Brotli are used in HTTP/HTTPS
- Serialization converts data structures for transmission — JSON, XML, and protobuf
- X.509 certificates are ASN.1-encoded Layer 6 structures used in TLS
- In modern networks Layer 6 functions are embedded in application protocols
- The TCP/IP model collapses Layers 5, 6, and 7 into a single Application Layer

