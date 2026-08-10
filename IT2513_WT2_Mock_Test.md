# IT2513 Data Security - Written Test 2 Mock Test
**Topics 5-7: Hash Functions · Digital Signatures · Cryptography in PKI**

> **Instructions (mirror the real test)**  
> - Closed-book · 50 minutes · 30 marks total  
> - Section A: 8 MCQs × 1 mark = **8 marks** · Section B: Multi-select 3 × 2, Fill-in-the-blanks 6 × 1, Open-ended 4+3+3 = **22 marks**  
> - Suggested timing: MCQ 8 min · Multi-select 10 min · Fill-in-blanks 8 min · Open-ended 20 min · review 4 min  
> - The answer for every question is **hidden below the question** - attempt it first, then click to reveal.  

---

## Section A: MCQ (8 × 1 = 8 marks)

*Circle ONE option per question.*

**A1. [Topic 5] A ___ is used to verify the integrity of a message.**

A. digital envelope
B. decryption algorithm
C. none of the above
D. message digest

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: D. message digest**  
A message digest (hash) uniquely represents a message; any change in the message changes the digest, so comparing digests verifies integrity.
</details>

**A2. [Topic 5] When two different messages produce the same message digest value, this is called a ___.**

A. hash
B. attack
C. collision
D. avalanche effect

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: C. collision**  
A collision violates the collision-resistance requirement of a good hash function.
</details>

**A3. [Topic 5] ___ is a message digest algorithm.**

A. IDEA
B. MD5
C. DES
D. RSA

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: B. MD5**  
DES and IDEA are symmetric block ciphers and RSA is an asymmetric cipher; MD5 (128-bit) is a message digest algorithm.
</details>

**A4. [Topic 6] To create a digital signature, the sender needs the ___.**

A. recipient's private key
B. sender's private key
C. recipient's public key
D. sender's public key

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: B. sender's private key**  
Signing encrypts the message digest with the SENDER'S OWN PRIVATE key; anyone can verify with the sender's public key.
</details>

**A5. [Topic 6] Which of the following is NOT a main purpose of a digital signature?**

A. Authenticity of the data
B. Non-repudiation
C. Confidentiality of the data
D. Integrity of the signed data

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: C. Confidentiality of the data**  
A digital signature provides integrity, authenticity and non-repudiation, but NEVER confidentiality - for that you need encryption (e.g. a digital envelope).
</details>

**A6. [Topic 6] Which of the following is considered the strongest message digest algorithm?**

A. SHA-1
B. SHA-256
C. SHA-128
D. SHA-512

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: D. SHA-512**  
SHA-512 has the longest digest (512 bits, 64-bit words). SHA-128 does not exist; SHA-1 (160-bit) has known weaknesses.
</details>

**A7. [Topic 7] A digital certificate binds a user with ___.**

A. the user's public key
B. the user's private key
C. the user's passport
D. the user's name only

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: A. the user's public key**  
A certificate binds the SUBJECT to their PUBLIC key. The private key must never appear in a certificate.
</details>

**A8. [Topic 7] The CA signs a digital certificate with ___.**

A. its own private key
B. its own public key
C. the user's private key
D. the user's public key

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: A. its own private key**  
The CA encrypts the certificate's message digest with ITS OWN PRIVATE key; verifiers decrypt with the CA's public key.
</details>

---

## Section B1: Multi-Select (3 × 2 = 6 marks)

*Choose ALL options that apply. 2 marks for all correct; 1 mark for one error; 0 otherwise.*

**B1. [Topic 5] Which of the following are requirements of a good message digest (hash) function?  (Choose ALL that apply)**

A. Irreversible
B. Avalanche effect
C. Collision-resistant
D. Variable-length output
E. Reversible
F. Deterministic

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: A, B, C, F**  
A hash must be deterministic, irreversible, collision-resistant, exhibit the avalanche effect and be fast. It is never reversible, and it maps ANY input length to a FIXED-length output.
</details>

**B2. [Topic 6] Which of the following statements about digital signatures are TRUE?  (Choose ALL that apply)**

A. They provide confidentiality of the signed data
B. They provide non-repudiation
C. They verify the integrity of the signed data
D. They can be created by anyone who has the sender's public key
E. They rely on asymmetric (public-key) cryptography

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: B, C, E**  
A digital signature gives integrity, authenticity and non-repudiation via the sender's PRIVATE key. It does not encrypt the data (no confidentiality), and only the private-key holder can sign.
</details>

**B3. [Topic 7] The Registration Authority (RA) is responsible for which of the following tasks?  (Choose ALL that apply)**

A. Authorizing requests for certificate revocation
B. Signing and issuing digital certificates
C. Generating keys on behalf of end users
D. Authorizing requests for key backup and recovery
E. Accepting and verifying registration information about new users

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Correct: A, C, D, E**  
The RA handles registration, key generation and authorizing backup/recovery/revocation requests - but it NEVER signs or issues certificates. Only the CA does that.
</details>

---

## Section B2: Fill-in-the-Blanks (6 × 1 = 6 marks)

*Write ONE answer in each blank.*

**C1. [Topic 5] The MD5 algorithm hashes an arbitrary-length byte string into a ______-bit value.**

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Answer: 128**  
MD5 produces a 128-bit message digest (4 chaining variables x 32 bits).
</details>

**C2. [Topic 5] In MD5, each 512-bit block is divided into 16 sub-blocks, each ______ bits long.**

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Answer: 32**  
Sub-blocks M[0]...M[15] are each 32 bits (16 x 32 = 512).
</details>

**C3. [Topic 5] In HMAC, the inner signature is calculated as Si = K' XOR ______.**

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Answer: ipad**  
Si = K' XOR ipad; So = K' XOR opad. The two are then hashed together with the message.
</details>

**C4. [Topic 6] To verify a digital signature, the recipient decrypts the digital signature using the sender's ______ key, then compares the result with the message digest it computed.**

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Answer: public**  
Verification always uses the SENDER'S PUBLIC key (the mirror of the private key used to sign).
</details>

**C5. [Topic 6] The three digital signature techniques approved in FIPS 186-5 are RSA, ______ and EdDSA.**

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Answer: ECDSA**  
FIPS 186-5 (Feb 2023) approves RSA, Elliptic Curve DSA (ECDSA) and Edwards Curve DSA (EdDSA).
</details>

**C6. [Topic 7] The offline mechanism for checking whether a digital certificate has been revoked is the ______ (list of revoked certificate serial numbers published by the CA).**

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Answer: Certificate Revocation List (CRL)**  
CRL = offline (client downloads the list); OCSP = online (client queries a responder).
</details>

---

## Section B3: Open-Ended (10 marks)

*Answer in the space provided. Number your steps. Name the exact key used in every encryption/decryption step.*

**D1. [Topic 5] (4 marks)**

(a) [1 mark] Using the simple message digest algorithm taught in class - multiply each digit in the number by the next digit, and if the product is a 2-digit number, disregard the first digit - compute the message digest of the number 7316294.  Show your working.

(b) [2 marks] A wants to send message M to B using HMAC to provide message integrity and data-origin authentication. Describe the steps performed by A (sender) and by B (receiver).

(c) [1 mark] An attacker intercepts M and modifies it. Why can the attacker NOT also replace the MAC so that B still accepts the modified message?

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Model answer**

(a) 7316294: 7x3=21->1; 1x1=1; 1x6=6; 6x2=12->2; 2x9=18->8; 8x4=32->2.  Digest = 2.
(b) Step 1: A calculates MAC = HMAC(K, M) using the shared symmetric key K.
    Step 2: A sends M together with the MAC to B.
    Step 3: B calculates MAC = HMAC(K, M) using the same key K.
    Step 4: B compares the received MAC with the calculated MAC. If they are equal, the message is accepted as authentic; otherwise B rejects it.
(c) The symmetric key K is known only to A and B. The attacker does not have K, so after changing M it cannot compute a valid replacement MAC that B would accept.
</details>

**D2. [Topic 6] (3 marks)**

(a) [2 marks] Alice wants to send Bob a confidential message while also providing integrity and non-repudiation, using a DIGITAL ENVELOPE together with a DIGITAL SIGNATURE. Describe the steps performed by Alice (sender) and by Bob (recipient).

(b) [1 mark] Why does Alice sign the message digest instead of signing the original plaintext?

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Model answer**

(a) Sender (Alice):
    Step 1: Hash the plaintext PT to obtain message digest MD.
    Step 2: Encrypt MD with Alice's own PRIVATE key to create the digital signature DS.
    Step 3: Generate a symmetric secret key and encrypt PT + DS with it.
    Step 4: Encrypt the symmetric key with Bob's PUBLIC key.
    Step 5: Send the encrypted (PT + DS) and the encrypted symmetric key to Bob.
    Recipient (Bob):
    Step 6: Decrypt the symmetric key with his own PRIVATE key.
    Step 7: Decrypt PT + DS with the symmetric key (confidentiality - only Bob can).
    Step 8: Hash PT to obtain MD1.
    Step 9: Decrypt DS with Alice's PUBLIC key to obtain MD2.
    Step 10: Compare MD1 and MD2 - equal => signature valid (non-repudiation), else reject.
(b) Efficiency (hash is much shorter and hashing is faster than signing), compatibility (hash converts any input into a fixed format/length) and integrity (a minute change in the text produces a large change in the hash).
</details>

**D3. [Topic 7] (3 marks)**

(a) [2 marks] List the FOUR steps in the creation of a digital certificate.

(b) [1 mark] Explain how the CA signs a digital certificate and how a user verifies that the certificate is genuine.

<details>
<summary><b>Answer (hidden - click to reveal)</b></summary>

**Model answer**

(a) 1. Key generation - the subject creates the key pair, or the RA creates it on the subject's behalf.
    2. Registration - the subject creates a Certificate Signing Request (CSR) containing the public key, name and other identifying information, and sends it to an RA.
    3. Verification - the RA verifies the subject's credentials and checks proof of possession (POP) of the private key.
    4. Certificate creation - the RA passes the information to the CA; the CA verifies it, creates the certificate, sends it to the subject and keeps a copy in the certificate directory.
(b) CA signs: it computes the message digest of all the certificate fields, encrypts the digest with its own PRIVATE key to obtain the digital signature, and inserts the signature into the certificate. User verifies: it computes the digest of all fields EXCLUDING the CA's signature (MD1), decrypts the CA's signature using the CA's PUBLIC key (MD2), and accepts the certificate only if MD1 = MD2.
</details>

---

## Answer Key (quick check)

| Q | Topic | Answer |
|---|-------|--------|
| A1 | Topic 5 | **D. message digest** |
| A2 | Topic 5 | **C. collision** |
| A3 | Topic 5 | **B. MD5** |
| A4 | Topic 6 | **B. sender's private key** |
| A5 | Topic 6 | **C. Confidentiality of the data** |
| A6 | Topic 6 | **D. SHA-512** |
| A7 | Topic 7 | **A. the user's public key** |
| A8 | Topic 7 | **A. its own private key** |
| B1 | Topic 5 | **A, B, C, F** |
| B2 | Topic 6 | **B, C, E** |
| B3 | Topic 7 | **A, C, D, E** |
| C1 | Topic 5 | **128** |
| C2 | Topic 5 | **32** |
| C3 | Topic 5 | **ipad** |
| C4 | Topic 6 | **public** |
| C5 | Topic 6 | **ECDSA** |
| C6 | Topic 7 | **Certificate Revocation List (CRL)** |
| D1 | Topic 5 | see model answer (click-to-reveal under the question) |
| D2 | Topic 6 | see model answer (click-to-reveal under the question) |
| D3 | Topic 7 | see model answer (click-to-reveal under the question) |

## Marking Guide

**Section A (8 marks):** 1 mark per MCQ.  
**Section B1 (6 marks):** 2 marks per multi-select - all correct = 2; one error (a missing correct option or one extra wrong option) = 1; otherwise 0.  
**Section B2 (6 marks):** 1 mark per blank. Accept abbreviations (CRL, RA, ECDSA) and equivalent exact terms (e.g. 'Registration Authority').  
**Section B3 (10 marks):**  
- **D1 (4):** (a) 1 - digest = 2 with working; (b) 2 - sender: compute MAC with shared key, send M + MAC; receiver: recompute MAC, compare, reject if unequal; (c) 1 - key known only to sender and receiver, attacker cannot compute a valid replacement MAC.  
- **D2 (3):** (a) 2 - sender: hash PT, encrypt MD with sender's PRIVATE key (DS), encrypt PT+DS with symmetric key, encrypt symmetric key with recipient's PUBLIC key; receiver: decrypt symmetric key with own private key, decrypt PT+DS, hash PT (MD1), decrypt DS with sender's public key (MD2), compare. Deduct 1/2 for each wrong key or a missing comparison; (b) 1 - any two of efficiency / compatibility / integrity.  
- **D3 (3):** (a) 2 - 1/2 mark per step (key generation, registration/CSR, verification/POP, certificate creation); (b) 1 - sign with CA's private key, verify with CA's public key, digest comparison.  

**Common deductions:** naming the wrong key (e.g. 'sender's public key' when signing); omitting the final MD1 = MD2 comparison; claiming a digital signature provides confidentiality; claiming HMAC provides non-repudiation; saying the RA issues certificates; leaving a blank empty.