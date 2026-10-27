# Module 7 — Data Protection and Cryptography
**Date:** 26 Oct 2026

Covered the theoretical and practical foundations of modern cryptography, data security states, encryption mechanisms, and how core principles protect information across its lifecycle.

---

## What I learned today

### Core Cryptographic Concepts
* **Plaintext vs Ciphertext:** Plaintext is raw, readable data; ciphertext is the scrambled output produced by an encryption algorithm using a specific key.
* **Ciphers & Keys:** A cipher is the mathematical formula/algorithm, while the key provides the entropy. Under Kerckhoffs's principle, the algorithm can be public as long as the key stays confidential.
* **Three States of Data:**
  * **Data at Rest:** Stored on disk/DBs (protected via full-disk encryption like BitLocker/LUKS, database-level encryption).
  * **Data in Transit:** Moving over networks (protected using TLS/SSL, IPsec, SSH).
  * **Data in Use:** Loaded into RAM/CPU cache (mitigated using hardware enclaves, secure memory, access control).

### Symmetric vs Asymmetric Encryption
* **Symmetric Encryption:**
  * Uses a single shared key for both encryption and decryption.
  * Very fast and resource-efficient; ideal for bulk data transfer.
  * Common algorithms: **AES** (AES-128, AES-256), **DES/3DES** (legacy/deprecated).
  * Main challenge: Key distribution (how to securely share the secret key without interception).
* **Asymmetric Encryption (Public Key Cryptography):**
  * Uses a mathematically linked key pair: a **Public Key** (shared openly to encrypt) and a **Private Key** (kept secret to decrypt).
  * Slower than symmetric encryption; primarily used for key exchange, identity verification, and digital signatures.
  * Common algorithms: **RSA**, **ECC (Elliptic Curve Cryptography)**, **Diffie-Hellman**.

### Hashing, Integrity & Digital Signatures
* **Cryptographic Hash Functions:**
  * One-way deterministic functions that produce a fixed-length output (digest) regardless of input size.
  * Properties: Collision-resistant, irreversible, avalanche effect (minor input change vastly alters output).
  * Standards: **SHA-256 / SHA-3** (modern standards); **MD5** and **SHA-1** are cryptographically broken due to collisions.
* **Digital Signatures:**
  * Ensures authentication, integrity, and non-repudiation.
  * Workflow: The sender hashes the message, encrypts the hash with their **private key**, and the recipient verifies it by decrypting the signature with the sender's **public key** and comparing hashes.
* **PKI & Digital Certificates:**
  * **Public Key Infrastructure (PKI):** Hierarchical trust model binding public keys to entities using digital certificates (X.509 standard) signed by trusted Certificate Authorities (CAs).

### Data Protection Principles & Governance
* **Principle of Least Privilege (PoLP):** Granting only the bare minimum access permissions necessary to perform a role.
* **Defense in Depth:** Layering controls (encryption, firewalls, IAM, segmentation) so no single failure compromises the data.
* **Data Minimization & Retention:** Storing only strictly required data and securely wiping/sanitizing media once retention periods lapse.

---

## Things I found interesting / want to explore more
- How hybrid cryptosystems work under the hood (e.g., TLS using asymmetric RSA/ECC for the handshake and Diffie-Hellman key exchange, then switching to symmetric AES-GCM for high-speed session encryption).
- The practical differences in key size and performance between RSA (e.g., 2048/4096-bit) and ECC (e.g., 256-bit curves) offering equivalent security levels.
- How quantum computing advancements (e.g., Shor's algorithm) impact current asymmetric standards and the industry's shift toward Post-Quantum Cryptography (PQC).

---

## My own words summary
Today's focus shifted from network attacks and exploitation tools to the defensive mathematics that keep data private. Grasping how symmetric ciphers handle raw speed while asymmetric algorithms solve the trust and key-distribution dilemma made modern protocols like TLS click. Hashing and digital signatures tie the whole package together by guaranteeing integrity and authenticity without needing to reveal the actual contents.