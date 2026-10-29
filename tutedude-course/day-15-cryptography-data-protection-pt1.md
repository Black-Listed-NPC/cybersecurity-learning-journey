# Day 15 - Module 7 (Part 1): Cryptography Fundamentals and Data Protection Principles

**Date:** 22 Oct 2026
**Module:** Module 7 - Data Protection and Cryptography (part 1 of 2)
**Study time:** 1h 39m

| Lecture | Duration |
|---|---|
| Cryptography Fundamentals | 35m |
| Data Protection and Security Principles (Part 1) | 1h 04m |

## Covered today

### What cryptography is
The science of protecting information by turning readable **plaintext** into unreadable **ciphertext**, so only people with the right key can read it. Goals: keep data confidential, authentic and untampered.

### Encryption vs encoding vs hashing
| | Purpose | Reversible? | Example | Easy way to remember |
|---|---|---|---|---|
| Encryption | Protection | Yes, with the key | AES, RSA | Locking data with a key |
| Encoding | Compatibility / transport | Yes, by anyone | Base64 | Changing the format |
| Hashing | Integrity | No | SHA-256 | A digital fingerprint |

Base64 is **not** security. Anyone can decode it.

### Symmetric encryption (AES)
- One shared key encrypts and decrypts: `plaintext + key = ciphertext`, `ciphertext + same key = plaintext`.
- Very fast and strong. The hard part is **sharing the key safely**.
- Used for disk encryption (BitLocker, FileVault), VPNs and database encryption.

### Asymmetric encryption (RSA / ECC)
- A key pair: the **public key encrypts**, the **private key decrypts**. The private key is never shared.
- Slower than AES.
- Used for HTTPS/TLS, digital certificates, PGP/GPG email and SSH.
- **Hybrid in practice:** asymmetric crypto exchanges a session key, then AES encrypts the actual data.

### Hashing and collisions
- A fixed-length digest; a tiny change in the input completely changes the hash (the avalanche effect).
- **MD5** is broken, **SHA-1** is weak; **SHA-256 / SHA-3** are recommended.
- **Collision:** two different inputs with the same hash, so a fake file can pass as genuine and signature checks can be bypassed.

### Mini lab - encrypt, decrypt, verify
```bash
echo "This is my secret data" > secret.txt
gpg -c secret.txt          # symmetric encryption -> secret.txt.gpg
gpg secret.txt.gpg         # decrypt with the same passphrase
sha256sum secret.txt       # fingerprint before transfer
sha256sum secret.txt       # same hash after transfer = file unchanged
```

### Data protection and security principles (Part 1)
- Revisited the CIA triad in a data-protection context: classify and label data, encrypt it, limit access, use MFA (confidentiality); use hashing, digital signatures and change tracking (integrity); use redundancy and fault tolerance (availability).
- **Threat types:** intentional (malware, phishing), unintentional (human error, like forgetting updates), natural (disasters).
- **Risk sources:** external (attacks from outside) and internal (malicious or untrained insiders).
- **Identity:** identification -> authentication -> authorisation -> accounting; password policy (length, complexity, expiry, history) and MFA.
- **Non-repudiation:** digital signatures, biometrics and video surveillance stop someone from denying an action.

## Key takeaways
- Hashing proves integrity, encryption gives confidentiality, and digital signatures add authenticity and non-repudiation.
- Choosing the wrong primitive (encoding instead of encryption, MD5 instead of SHA-256) is itself a vulnerability - OWASP A04, Cryptographic Failures.
