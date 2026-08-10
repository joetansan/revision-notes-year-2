# IT2513 Data Security — Written Test 2 Study Guide

**Topics 5–7 (Weeks 8–15): Hash Functions · Digital Signatures · Cryptography in PKI**

---

## 0. Exam Snapshot (from the announcement)

| Item | Detail |
|---|---|
| When | Week 17 lesson |
| Format | Closed-book, proctored, **LockDown Browser** on lab desktop |
| Weight | **30%** of final grade |
| Marks | **8 MCQ** + **22 Multi-Select / Fill-in-the-blanks / Open-Ended** = 30 |
| Duration | **50 minutes** (+extra time if eligible) |
| Scope | **Topics 5 to 7** — revise lectures AND tutorials |
| Emphasis | "Understand and **can apply** all cryptographic methods taught" |

> The 22-mark section is the bulk of the paper. Expect multi-select questions (choose ALL that apply), blanks, and open-ended questions that make you **write out step-by-step processes** (HMAC, digital signature, digital envelope, certificate creation) — not just definitions.

---

## 1. What the Lecturer Will Likely Test

The tutorials are the lecturer's own revision set — the real test questions are almost always drawn from, or modelled on, these. Priority order:

### 🟥 HIGH confidence (tutorial MCQs + SAQs, straight from the slides)

| Likely question | Where it comes from | Answer / key points |
|---|---|---|
| MCQ: "A ___ is used to verify the integrity of a message" | Tutorial 5 Q1 | **message digest** |
| MCQ: "When two messages produce the same digest it is called ___" | Tutorial 5 Q2 | **collision** |
| MCQ: "___ is a message digest algorithm" | Tutorial 5 Q3 | **MD5** (DES/IDEA/RSA are cipher/encryption algorithms) |
| MCQ: "MAC is ___ a message digest" | Tutorial 5 Q4 | **different from** (MAC = digest + secret key) |
| MCQ: "To create a digital signature we need the ___" | Tutorial 6.1 Q3 | **sender's private key** |
| MCQ: "To verify a digital signature we need the ___" | Tutorial 6.1 Q4 | **sender's public key** |
| MCQ: "Strongest message digest algorithm" | Tutorial 6.1 Q2 | **SHA-512** (SHA-128 doesn't exist; SHA-1 is weak) |
| MCQ: "Which is NOT a main purpose of a digital signature" | Tutorial 6.2 Q1 | **Confidentiality** (DS gives integrity, authenticity, non-repudiation — never confidentiality) |
| MCQ: "DSS-approved hash function" | Tutorial 6.2 Q2 | **SHA3-256** (per FIPS 186-5; MD5/SHA-1/RIPEMD-160 not approved) |
| MCQ: "Final solution to the key-exchange problem" | Tutorial 7 Q1 | **digital certificate** |
| MCQ: "A digital certificate binds a user with ___" | Tutorial 7 Q2 | **the user's public key** |
| MCQ: "The ___ of the user should never appear in a certificate" | Tutorial 7 Q3 | **private key** |
| MCQ: "A ___ can issue digital certificates" | Tutorial 7 Q4 | **CA** |
| MCQ: "___ standard defines the structure of a digital certificate" | Tutorial 7 Q5 | **X.509** |
| MCQ: "The CA signs a certificate with ___" | Tutorial 7 Q6 | **its own private key** |
| MCQ: "Highest-authority CA is called ___" | Tutorial 7 Q7 | **root** CA |
| MCQ: "CRL is ___" / "OCSP is ___" | Tutorial 7 Q8/Q9 | CRL = **offline**, OCSP = **online** |
| SAQ: "If a sender encrypts with a symmetric key → provides ___" | Tutorial 6.1 SAQ 1 | **Confidentiality** (+ authentication if HMAC) |
| SAQ: "…with the recipient's public key → provides ___" | Tutorial 6.1 SAQ 2 | **Confidentiality** |
| SAQ: "…with his own private key → provides ___" | Tutorial 6.1 SAQ 3 | **Non-repudiation / authentication** |

### 🟨 MEDIUM-HIGH confidence (the "apply" open-ended questions)

| Likely question | Key points you must write |
|---|---|
| Steps for A→B with HMAC (integrity + origin auth) | 4 steps: A computes MAC(K,M) → A sends M+MAC → B computes MAC(K,M) → B compares; equal ⇒ good, else reject |
| Why can't the attacker also change the MAC? | Key is known **only to sender & receiver**; attacker lacks key to recompute a valid MAC |
| How does MAC assure integrity / origin auth? | Any change in M ⇒ different MAC (integrity); only the holder of the shared key can produce the correct MAC (origin auth) |
| MD vs MAC key difference | MD: integrity only. MAC: integrity **+ data-origin authentication** (uses a shared secret key) |
| HMAC disadvantages / non-repudiation | Symmetric key exchange problem; multiple recipients → key management (or single shared key → auth problem); **cannot provide non-repudiation** because both parties hold the same key |
| Steps to create / verify a digital signature | Create: hash PT→MD1, encrypt MD1 with sender's private key → DS, send PT+DS. Verify: hash PT→MD2, decrypt DS with sender's public key → MD1, compare MD1=MD2 |
| Why sign the hash instead of the document? | **Efficiency** (shorter, hashing faster than signing), **compatibility** (any input → fixed length/format), **integrity** (minute change → large hash change) |
| Digital envelope + signature together (10 steps) | See §3.4 — confidentiality + integrity + non-repudiation in one flow. **Very likely as a diagram/step question.** |
| 4 steps of digital certificate creation | Key generation → Registration (CSR) → Verification (POP) → Certificate creation |
| Roles of CA vs RA | RA: verify registration info, generate keys for users, authorize key backup/recovery & revocation. **RA does NOT sign or issue certificates.** |
| 3 POP mechanisms | ① sign CSR with private key, RA verifies with public key ② RA encrypts challenge string with public key, subject decrypts ③ RA encrypts dummy certificate, subject decrypts to retrieve it |
| How CA signs / user verifies a certificate | CA: hash all fields→MD, encrypt with **CA's private key**→DS, insert. User: hash fields (excluding signature)→MD1, decrypt DS with **CA's public key**→MD2, equal ⇒ trust |
| Common causes of revocation | Private key compromised; issuing CA compromised; owner no longer owns the domain |

### 🟩 MEDIUM confidence (concepts/application the lecturer emphasises in slides)

- MD5 pipeline: 5 steps + the 4 chaining variables + 4 rounds × 16 iterations (know the *order* of operations, not the t-table)
- Simple message-digest worked example (digit-multiplication) — **the lecturer taught two worked examples; expect a compute-the-digest question** (it's the cheapest "application" mark)
- Birthday attack idea: 23 people ⇒ >50% collision chance; used to find hash collisions
- SHA family: SHA-0/1/2/3, bit lengths, SHA-256 (32-bit words) vs SHA-512 (64-bit words)
- CMAC: CBC-based, subkeys K1/K2, tweak of last block
- DSS (FIPS 186-5, Feb 2023): approved techniques **RSA, ECDSA, EdDSA**; approved hashes **SHA3-224/256/384/512** (note: SHA-1 is *not* on the list — the tutorial answer is SHA3-256)
- Attacks on DS: **replay attack** (same content ⇒ same signature; counter: document ID + timestamp) and **public-key authenticity** (attacker posts own key as sender's)
- Certificate hierarchy: one-tier vs two-tier vs three-tier (which CA is offline/online; why two-tier is recommended)
- Certificate chain verification: walk up until a **trusted root** is found; root cert is self-signed
- Cross-certification: creates cross-level trust between different root CAs
- CRL vs OCSP vs SCVP (offline vs online; serial-number-only vs whole certificate; SCVP can check backdated validity)
- PKI risks: certificate-related, deployment, governance/visibility, security-related (4 categories)
- X.509 certificate fields (Version, Serial No, Signature Algorithm ID, Issuer, Validity, Subject, **Subject Public Key Info — never blank**, CA's signature)

---

## 2. Topic 5 — Hash Functions

### 2.1 Message Digest (Hash / MDC — Modification Detection Code)

- **Unique representation of a message** (like a human fingerprint). Used to ensure **integrity**.
- Maps a message of **any length** to a **fixed-length** hash value.
- Same input ⇒ always same output. Minute input difference ⇒ dramatically different output.

**Worked example (the lecturer's simple digest algorithm):** multiply each digit by the next digit; if the product has 2 digits, discard the first digit; skip a next-digit of 0.

```
Original number 7391723          Original number 7391743
 7×3=21→1                         7×3=21→1
 1×9=9                            1×9=9
 9×1=9                            9×1=9
 9×7=63→3                         9×7=63→3
 3×2=6                            3×4=12→2
 6×3=18→8                         2×3=6
 Digest = 8                       Digest = 6
```

A one-digit change (2→4) changed the digest (8→6) — this demonstrates the **avalanche effect**.

**5 requirements of a good hash function** (classic open-ended question):

| # | Requirement | Meaning |
|---|---|---|
| 1 | **Deterministic** | Same message ⇒ same hash value, every time |
| 2 | **Irreversible** | Original message cannot be derived from the hash |
| 3 | **Collision-resistant** | Different messages ⇒ different hash values |
| 4 | **Avalanche effect** | Small change in message ⇒ large change in hash |
| 5 | **Fast** | Hashing must be quick to compute |

### 2.2 Collision & Birthday Attack

- **Collision** = two different messages produce the same digest. Violates the collision-resistance requirement.
- With a 128-bit digest the chance is 1 in 2¹²⁸; 160-bit ⇒ 1 in 2¹⁶⁰ — very rare.
- **Birthday paradox:** with 23 people in a room there is >50% chance two share a birthday. n people ⇒ n(n−1)/2 pairs; (364/365)²⁵³ ≈ 49.95% no match ⇒ 50.05% match.
- **Birthday attack** uses this to discover collisions — finding collisions is easier than you'd think.

### 2.3 MD5

- Created by **Ronald Rivest** (RSA Data Security / MIT), 1991.
- Hashes an arbitrary-length byte string into a **128-bit** value.
- Declared **"cryptographically broken" in 2008** (colliding X.509 certificates could be created) — yet still widely used.

**MD5 pipeline (5 high-level steps — know these in order):**

1. **Padding** — padding p starts with bit `1` followed by `0`s so that **m + p = 512n − 64**
2. **Append length** — append the message length m as a **64-bit** value ⇒ total = m + p + 64 = **512n** (multiples of 512)
3. **Divide input into 512-bit blocks**
4. **Initialize chaining variables** — A = `01234567`, B = `89abcdef`, C = `fedcba98`, D = `76543210` (each 32 bits)
5. **Process blocks:**
   - 5.1 Copy chaining variables into registers a, b, c, d
   - 5.2 Divide each 512-bit block into **16 sub-blocks M[0]…M[15]** (32 bits each)
   - 5.3 **4 rounds**, each round = 16 iterations, each iteration = 7 steps (Process P → add → add M[i] → add t[k] → circular left shift by s bits → add to b → place into a), then **right rotation** of the register (abcd → dabc)
   - Hash value = register contents after round 4 of the **last** block

**Process P per round:**

| Round | Process P |
|---|---|
| 1 | (b AND c) OR ((NOT b) AND d) |
| 2 | (b AND d) OR (c AND (NOT d)) |
| 3 | b XOR c XOR d |
| 4 | c XOR (b OR (NOT d)) |

**Round details (know the pattern, not the numbers):**

| Round | Sub-block order M[i] | Constants | Shift s (pattern) |
|---|---|---|---|
| 1 | 0,1,2,…,15 | t[1..16] | 7,12,17,22 repeating |
| 2 | 6,11,0,5,10,15,4,9,14,3,8,13,2,7,12,1 | t[17..32] | different |
| 3 | 5,8,11,14,1,4,7,10,13,0,3,6,9,12,15,2 | t[33..48] | different |
| 4 | 14,5,12,3,10,1,8,15,6,13,4,11,2,9,0,7 | t[49..64] | different |

The constant array t has **64 elements** (16 used per round), e.g. t[1] = D76AA478 … t[64] = EB86D391. **Don't memorise the table — know its structure** (64 elements, 16 per round).

### 2.4 SHA family

| Algorithm | Digest | Notes |
|---|---|---|
| SHA-0 | 160-bit | Published 1993, **withdrawn** (undisclosed "significant flaw") |
| SHA-1 | 160-bit | Resembles MD5, designed by NSA; weaknesses found, replaced by SHA-2 |
| SHA-2 | 256/512-bit | **SHA-256 uses 32-bit words, SHA-512 uses 64-bit words**; SHA-256 is currently most common |
| SHA-3 | 224/256/384/512-bit | Based on **Keccak**; same hash lengths as SHA-2 but very different internal structure |

**Why is SHA more secure than MD5?** Longer digest (160–512 bits vs 128) ⇒ far smaller collision probability (2¹⁶⁰ vs 2¹²⁸), plus no known collision attacks on SHA-2/3 (MD5 is cryptographically broken since 2008).

### 2.5 Message Authentication Code (MAC)

- Ensures **integrity** AND **data-origin authentication**.
- Uses message digest + **symmetric encryption**; sender and receiver share a common symmetric key.

**Steps (A → B):**
1. A calculates MAC using key K and message M
2. A sends **M and MAC** to B
3. B calculates MAC using K and M
4. B compares received MAC with calculated MAC — equal ⇒ good; else **reject**

**The 4 classic "why" answers (memorise these):**

| Question | Answer |
|---|---|
| How does MAC assure integrity? | If the attacker changes M but not the MAC, B calculates a different MAC than the one received |
| Why can't the attacker also change the MAC? | The symmetric key is known **only to sender and receiver** — the attacker cannot compute a valid replacement MAC |
| How does MAC assure origin authentication? | Only the sender holds the key, so only the sender can produce the correct MAC |
| How does MAC differ from a symmetric algorithm? | Symmetric: reversible (encryption + decryption). MAC: **one-way / irreversible**, only mixes the key with the message |

**MD vs MAC — key difference:** MD provides integrity **only**; MAC provides integrity **and** data-origin authentication.

### 2.6 HMAC (Hash-based MAC)

- Hash function + secret key. E.g. **HMAC-MD5, HMAC-SHA1**.
- Legend: K = secret key, K′ = transformed key (b bits), Si/So = signatures, ipad/opad = paddings, b = bits per block.

**7 steps:**
1. **Transform key**: K = b ⇒ K′ = K; K < b ⇒ append 0s to the left (K′ = 0-padding + K); K > b ⇒ K′ = H(K) (hash it down)
2. **Si = K′ XOR ipad**
3. Append message M to Si
4. Hash (Si + M) → MD
5. **So = K′ XOR opad**
6. Append MD to So
7. Hash (So + MD) → **HMAC**

> ⚠️ **Slide inconsistency warning:** the lecture legend lists ipad = 0x5C and opad = 0x36, but the standard HMAC values (RFC 2104) are **ipad = 0x36, opad = 0x5C**. The exam is far more likely to ask *what Si is computed from* (K′ XOR ipad) than the exact byte value — but if a value question appears, use the standard (ipad 0x36, opad 0x5C).

**Disadvantages of HMAC:**
- Relies on a **symmetric secret key** ⇒ key-exchange problem
- Multiple recipients: many keys ⇒ key management burden; one shared key ⇒ authentication problem (can't tell recipients apart)

**Can HMAC be used as a digital signature / non-repudiation?** **No.** Both sender and receiver hold the same symmetric key, so a MAC could have been produced by either party — no way to prove which.

### 2.7 CMAC (Cipher-based MAC)

- Old name: **OMAC** (One-key MAC).
- Uses an encryption algorithm (**DES/AES**) to generate the MAC.
- Based on **CBC** (Cipher Block Chaining), but the result is a **single block**.

**Steps:** ① generate two sub-keys K1, K2 from key K → ② divide M into b-bit blocks M1…Mn → ③ **tweak Mn** with K1/K2 (depending on its block size) → ④ encrypt the chain; output is a fixed-size hash block, independent of message length.

---

## 3. Topic 6 — Digital Signatures

### 3.1 The recap table (what each key provides — very likely MCQ/SAQ)

| Sender encrypts with | Recipient decrypts with | Provides |
|---|---|---|
| Symmetric key | Symmetric key | **Confidentiality** (authentication if HMAC) |
| Recipient's public key | Recipient's private key | **Confidentiality** |
| Sender's private key | Sender's public key | **Non-repudiation (authentication)** |

### 3.2 Digital signature basics

- Cryptographic output that verifies the **authenticity** of data. Equivalent to a handwritten signature.
- Two operations: **signing** (uses signer's private key) and **verification** (anyone with the public key).
- Main purposes: **integrity** of the signed data + **non-repudiation** (signer cannot deny).
- Based on **asymmetric (public-key) cryptography**.
- A scheme = 3 algorithms: **key generation, signing, verifying**.

### 3.3 Create & verify (6 steps — the core "apply" question)

**Creating (sender):**
1. Sender hashes the plaintext PT with a digest algorithm (e.g. SHA-1) → **MD1**
2. Sender encrypts MD1 with **his own private key** → encrypted MD = **Digital Signature (DS)**
3. Sender sends **PT + DS** to recipient

**Verifying (recipient):**
4. Recipient hashes PT with the same algorithm → **MD2**
5. Recipient decrypts DS with the **sender's public key** → MD1
6. Compare: **MD1 = MD2** ⇒ accept & trust PT; else ⇒ **reject**

> ⚠️ **Slide typo warning:** slide 13's prose says "Step 2: …by encrypting the **PT** using his own Private Key" — the diagram and everything else make clear it's the **message digest** that is encrypted. In the exam, always say "encrypt the message digest (hash) with the sender's private key."

**Why sign the hash instead of the original document?**
1. **Efficiency** — the signature is much shorter; hashing is faster than signing
2. **Compatibility** — a hash converts any input/type into a fixed format and length
3. **Integrity** — a minute change in the text produces a large change in the hash

### 3.4 Digital envelope + digital signature (the 10-step combined flow — HIGH exam value)

Digital signature alone gives integrity + non-repudiation but **not confidentiality**. Add a digital envelope to get all three.

**Sender:**
1. Hash PT → MD
2. Encrypt MD with sender's **private key** → DS
3. Generate a **symmetric secret key**; encrypt PT + DS with it
4. Encrypt the symmetric key with the **recipient's public key**
5. Send: encrypted (PT+DS) **and** encrypted symmetric key

**Recipient:**
6. Decrypt the symmetric key with **his own private key**
7. Decrypt PT+DS with the symmetric key (⇒ **confidentiality** — only recipient can)
8. Hash PT → MD1
9. Decrypt DS with the **sender's public key** → MD2
10. Compare MD1 = MD2 ⇒ signature correct, else reject (⇒ **non-repudiation** — only the sender could have produced the DS)

### 3.5 Attacks on digital signatures

| Attack | Idea | Countermeasure |
|---|---|---|
| **Replay attack** | Same message content ⇒ same signature; attacker replays old signed message | Include **document IDs and timestamps** in the message so contents differ |
| **Public-key authenticity** | Attacker generates own key pair, signs altered message with own private key, and posts the generated public key as the sender's | Bind identity to public key via a **digital certificate / PKI** (Topic 7) |

### 3.6 Digital Signature vs HMAC (comparison table — likely MCQ/MS)

| | Digital Signature | HMAC |
|---|---|---|
| Key algorithm | **Asymmetric** | **Symmetric** |
| Operations | Encryption **and** decryption | Encryption only |
| Provides | **Non-repudiation** + integrity | **Source authentication** + integrity |

### 3.7 Digital Signature Standard (DSS)

- Published by **NIST** as FIPS 186; current version **FIPS 186-5 (3 Feb 2023)**.
- **3 approved signature techniques:** ① RSA ② ECDSA (Elliptic Curve DSA) ③ EdDSA (Edwards Curve DSA)
- **4 approved hash functions:** **SHA3-224, SHA3-256, SHA3-384, SHA3-512**

> ⚠️ **Update trap:** older materials mention SHA-1 under DSS — FIPS 186-5 approves only the SHA-3 family. That's why Tutorial 6.2 Q2's answer is **SHA3-256** (not SHA-1, MD5, or RIPEMD-160).

---

## 4. Topic 7 — Cryptography in PKI

### 4.1 Why PKI? (the MITM problem)

Without PKI, B publishes his public key in a directory service. Attacker C **replaces B's key with C's own key**. A retrieves what it thinks is B's key, encrypts with it — C intercepts, decrypts with C's private key (MITM), re-encrypts with B's real key and forwards. Both A and B think they're talking securely.

**PKI** = the framework behind digital certificates that proves **who the subject is** and that the **public key really belongs to them**, via trusted third parties (CAs).

### 4.2 Digital certificate & X.509

- An electronic document that **binds a public key to a subject** (person/organisation).
- Structure defined by the **X.509** standard (ITU).

**Typical contents (the "never blank" and "never included" traps):**

| Field | Description |
|---|---|
| Version | X.509 version (1, 2 or 3) |
| Certificate Serial Number | Unique integer generated by the CA |
| Signature Algorithm Identifier | Algorithm the CA used to sign |
| Issuer Name | DN of the CA that created/signed it |
| Validity (Not Before / Not After) | Timeframe the certificate is valid |
| Subject Name | DN of the end entity (user/org) the certificate refers to |
| Subject Public Key Information | The subject's public key + related algorithms — **can never be blank** |
| CA's Digital Signature | Signature over all the fields |

The user's **private key must NEVER appear in a certificate** (Tutorial 7 Q3).

### 4.3 CA and RA roles

**Certificate Authority (CA):** the trusted organisation that **issues** digital certificates to individuals/systems/organisations.
- Singapore: IMDA-accredited CAs — **Assurity Trusted Solutions** (GovTech's NCA) and **Netrust** (Asia's first public CA).
- Large organisations can run their own CA and be trusted externally via **certificate chaining** (their CA becomes an **intermediate CA** trusted by a public CA, e.g. Google's GTS CA 1C3 trusted by GlobalSign).

**Registration Authority (RA):** takes over some CA tasks:
- Accept and **verify registration information** about new users
- **Generate keys** on behalf of end users
- Accept/authorize requests for **key backup and recovery**
- Accept/authorize requests for **certificate revocation**
- ❗ **RA does NOT sign or issue certificates** (only the CA does)

### 4.4 Creating a digital certificate (4 steps)

1. **Key generation** — subject creates the key pair, OR the RA creates it on the subject's behalf
2. **Registration** — subject creates a **Certificate Signing Request (CSR)** containing public key, name, identifying info (email, server name); sends it to an RA
3. **Verification** — RA verifies the subject's credentials and checks **proof of possession (POP)** of the private key
4. **Certificate creation** — RA passes the info to the CA; CA verifies, creates the certificate, sends it to the subject, and keeps a copy in the **certificate directory**

**The 3 POP mechanisms:**
1. RA asks the subject to **digitally sign the CSR** with the private key; RA verifies with the public key
2. RA **encrypts a challenge string** with the subject's public key; subject must decrypt it correctly
3. RA generates a **dummy certificate**, encrypts it with the subject's public key; subject must decrypt and retrieve the plaintext certificate

### 4.5 Signing & verifying a certificate

**CA signs:** hash all the certificate fields → MD → encrypt MD with **CA's private key** → DS → insert DS into the certificate.

**User verifies:** hash all fields **excluding the CA's signature** → MD1 → decrypt DS with the **CA's public key** → MD2 → if MD1 = MD2 ⇒ valid certificate, else invalid.

### 4.6 CA hierarchy

| Type | Structure | Pros / Cons |
|---|---|---|
| **One-tier** | Single CA = root + issuing, **online** | Risks: ① the only CA is online ⇒ susceptible to compromise ② can't revoke the CA if compromised ③ difficult to expand. **Not recommended for production** |
| **Two-tier** | **Root CA offline** + issuing CA online | Separates roles ⇒ root private key better protected; scalable, flexible (different locations/security levels). **Meets most companies' needs** |
| **Three-tier** | Root (offline) + issuing (online) + **intermediate (offline)** between them | Intermediate CA used as a **policy CA**, and to **revoke CAs** (e.g. key compromise) without taking down other branches |

**Verifying a certificate:** walk up the **certificate chain** (B ← CA3 ← CA2 ← Root) until a **trusted authority** is found. The root CA certificate is **self-signed** (Issuer = Subject = Root CA).

**Cross-certification:** creates **cross-level trust** between different root CAs so certificates from one hierarchy are trusted in another.

### 4.7 Certificate revocation

**Why revoke?** A certificate may be revoked before expiry. Common causes:
1. The certificate's **private key has been compromised**
2. The **issuing CA has been compromised**
3. The owner **no longer owns the domain** it was issued for

**Two checking mechanisms:**

| | CRL (Certificate Revocation List) | OCSP (Online Certificate Status Protocol) |
|---|---|---|
| Mode | **Offline** | **Online** |
| How it works | CA publishes a list of revoked serial numbers (with date, reason, publication times); **clients download the CRL** and check the serial number | Client sends the serial number to the **OCSP responder**; responder checks the **X.500 directory**; returns a **digitally signed response**: **Good / Revoked / Unknown** (+ date/time/reason if revoked) |
| Typical issue | List can be stale between publications | Needs a live responder |

**OCSP vs SCVP (Simple Certificate Validation Protocol):**

| | OCSP | SCVP |
|---|---|---|
| Client request | Just the **certificate serial number** | The **entire certificate** (+ intermediate certs) |
| Chain of trust | Only the given certificate checked | Can check the **full chain** |
| Checks | Only revoked-or-not | Additional checks (full chain, which revocation source to use: CRL or OCSP) |
| Returned info | Only the status | Extra info as requested (proof of revocation, chain used) |
| Extra features | None | Can validate for a **backdated event** (e.g. was Bob's cert valid *at the time of signing*) |

### 4.8 PKI risks (4 categories — likely multi-select)

1. **Certificate-related:** outdated protocols; weak keys & infrequent key rotation; mismanaged certificates
2. **Deployment:** lack of automation; insufficient skills/resources; lack of PKI awareness
3. **Governance & visibility:** no clear certificate ownership; lack of policies/consistency; lack of centralized inventory/visibility
4. **Security-related:** improper protection/management of private keys; **compromised Root CA**; failure to patch & respond to vulnerabilities

---

## 5. Quick-Reference Pipeline Sheets (memorise these as flows)

**HMAC (7 steps):** K′ = pad-left/hash K to b bits → Si = K′ ⊕ ipad → append M → hash → MD → So = K′ ⊕ opad → append MD → hash → **HMAC**

**Digital signature:** PT → hash → MD1 → encrypt with **sender's private key** → DS → [send PT + DS] → recipient: PT → hash → MD2 ; DS → decrypt with **sender's public key** → MD1 ; compare MD1 = MD2

**Digital envelope + DS (10 steps):** hash PT → encrypt MD with sender's private key (DS) → encrypt PT+DS with symmetric key → encrypt symmetric key with **recipient's public key** → send → recipient decrypts symmetric key with own private key → decrypt PT+DS with symmetric key → hash PT (MD1) → decrypt DS with sender's public key (MD2) → compare

**Certificate signing:** cert fields → hash → MD → encrypt with **CA's private key** → DS (inside cert). Verify: fields (minus signature) → hash → MD1 ; DS → decrypt with **CA's public key** → MD2 ; compare

**Who signs/encrypts with what — final sanity table:**

| Operation | Key used |
|---|---|
| Create digital signature | Sender's **private** key |
| Verify digital signature | Sender's **public** key |
| Encrypt for confidentiality to B | B's **public** key |
| Decrypt confidential message | B's **private** key |
| CA signs a certificate | CA's **private** key |
| Verify a certificate | CA's **public** key |
| MAC/HMAC computation | Shared **symmetric** key |

---

## 6. Open-Ended Answer Templates (how to score full marks)

**"Describe the steps…" questions (HMAC, DS, envelope, cert creation):**
1. Write steps **in order**, one line per step, numbered (1..n) — markers give marks per step
2. For every encryption step, name the **exact key** ("encrypt MD1 with the sender's private key" — not "with a key")
3. Always end verification flows with the **comparison**: "if MD1 = MD2 accept, else reject"
4. Add the **one-line "why"** at the end (e.g. "This provides non-repudiation because only the sender holds the private key")

**"Why / Explain" questions:** state the reason, then the consequence. E.g. *Why can't the attacker change the MAC?* → "The symmetric key is known only to sender and receiver (reason) ⇒ the attacker cannot compute a valid replacement MAC after modifying the message (consequence)."

**"Provide(s) ___" questions:** map exactly: symmetric key → confidentiality; recipient's public key → confidentiality; sender's private key → non-repudiation/authentication.

**Comparison questions (MD vs MAC, DS vs HMAC, OCSP vs SCVP, CRL vs OCSP):** make a two-column table — one point per row, aim for 3–4 rows.

---

## 7. 50-Minute Exam Strategy

| Time | Section | Tactic |
|---|---|---|
| 0–8 min | MCQ (8 marks) | Answer all; if unsure, flag and return. Tutorial MCQs are recycled — recall the tutorial answers first |
| 8–18 min | Multi-select (6 marks) | Treat as "all that apply" — each option is TRUE or FALSE. Watch the "NOT" and "RA does NOT sign certificates" traps |
| 18–28 min | Fill-in-blanks (6 marks) | Exact terms: 128-bit, 32-bit, ipad, sender's public key, ECDSA, CRL — spell fully (e.g. "Certificate Revocation List (CRL)") |
| 28–48 min | Open-ended (10 marks) | 4-mark questions deserve ~8 minutes each. Number the steps. Name the keys. End with the comparison |
| 48–50 min | Review | Check you didn't read a "NOT" as a positive, and that every blank has *something* written |

**Last-minute do-not-forget list:**
- MD5 = 128-bit; SHA-1 = 160-bit; SHA-256 = 32-bit words; SHA-512 = 64-bit words
- ipad/opad, Si = K′ ⊕ ipad, So = K′ ⊕ opad
- MAC = integrity + origin auth; MD = integrity only; HMAC ≠ non-repudiation
- DSS FIPS 186-5: RSA / ECDSA / EdDSA + SHA3-224/256/384/512
- DS: sign with sender's private key, verify with sender's public key
- Cert: sign with CA's private key, verify with CA's public key; private key never in the certificate; Subject Public Key Info never blank
- RA verifies/registers but never signs or issues
- CRL = offline, OCSP = online, root CA = self-signed, cross-certification = trust across hierarchies
