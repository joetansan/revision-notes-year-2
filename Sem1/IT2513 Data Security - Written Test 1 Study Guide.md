# 📚 IT2513 Data Security — Written Test 1 Study Guide
### Topics 1–4 (Weeks 1–7) | 30 Marks | 50 Minutes

> **Format:** 22 marks MCQ/Multi-Select/Fill-in-the-blanks + 8 marks Short Answer Questions
> **Professor's emphasis:** "Make sure you understand and can apply all cryptographic methods taught."
> **Reference textbook:** Atul K. (Chapters 1–4)

---

# ═══════════════════════════════════════════════
# TOPIC 1: Need for Information Security
# ═══════════════════════════════════════════════

## 1.1 Why Information Security Matters ⭐

**Core concept:** Confidential information sent in clear text (unencrypted) is NOT secure and can be compromised.

**Example:** Credit card details sent in cleartext from a browser to a web server can be intercepted by attackers.

**Why it matters:** This is the foundation of the entire course — every other topic exists to solve this problem.

---

## 1.2 The Six Security Principles ⭐⭐⭐

This is **heavily testable** — MCQs, fill-in-the-blanks, and short answer. Know each principle, what compromises it, and the countermeasure.

### i. Confidentiality
- **What:** Only authorized parties / intended recipients can access the information
- **Compromised by:** Interception (eavesdropping, sniffing)
- **Solution:** Encryption/Decryption
- **Key distinction:** Confidentiality ≠ Privacy. Privacy is the *right* of an individual to control information about themselves. Confidentiality is the *assurance* that only authorized parties access it.
- **Scenario:** User A sends a secret message to User B. Attacker C intercepts it. Confidentiality is lost.

### ii. Authentication
- **What:** Assures the identities of communicating parties — "Are you really who you claim to be?"
- **Compromised by:** Fabrication (masquerade / identity theft)
- **Scenario:** Attacker C pretends to be User A and communicates with User B (Man-in-the-Middle)
- **Three factors of authentication:**
  1. **What you know** — password, PIN
  2. **What you have** — security token, ID card, phone
  3. **What you are** — fingerprint, facial recognition, retina
- **2FA** = using any 2 of the above 3 methods ⭐

### iii. Integrity
- **What:** Information is not modified by unauthorized parties during transmission
- **Compromised by:** Modification (alteration or replay attack)
- **Scenario:** A sends "Transfer $100 to A". C intercepts and changes it to "Transfer $1000 to C". Integrity is lost.

### iv. Non-Repudiation
- **What:** Sender cannot deny having sent a message
- **Provided by:** Digital signature
- **Analogy:** Like signing a cheque — you can't deny making the payment because your signature is on it
- **Scenario:** A sends a message to B, then says "I didn't send it!" — non-repudiation prevents this

### v. Access Control
- **What:** Specifies and controls "who" can access "what"
- **Implementation:**
  - **Access Control Matrix** — table of subjects (users) × objects (files) × access privileges (read/write/execute)
  - **Access Control List (ACL)** — permissions attached to an object specifying which users have access. ACL is a **subset** of the Access Control Matrix.

```
Access Control Matrix:
           File 1    File 2
User 1     Read      Read, Write
User 2     Read,Write Read, Write

ACL of File 1:
  User 1: Read
  User 2: Read, Write
```

### vi. Availability
- **What:** Information/systems are available to authentic users all the time
- **Compromised by:** Interruption (Denial-of-Service / DoS attack)
- **Countermeasures:** Increasing network bandwidth, providing system and network redundancy

---

## 1.3 Types of Attacks ⭐⭐

```
                    Attacks
                   /      \
           Passive         Active
          /      \        /    |     \
  Release of   Traffic  Interruption  Modification  Fabrication
  Message      Analysis   (DoS)      /        \     (Masquerade)
  Contents                          Replay    Alteration
```

### Passive Attacks ⭐
- Attacker **eavesdrops/monitors** data transmission
- Attacker makes **no attempt to modify** data
- **Harder to detect** (no visible change to data)
- Types:
  1. **Eavesdropping / Release of message contents** — intercepts and forwards message content
  2. **Traffic analysis** — analyses data traffic patterns to detect communication patterns

### Active Attacks ⭐
- Attacker **modifies** original message or **creates** a false message
- Types:
  1. **Interruption (DoS)** — affects **availability**
  2. **Modification** — affects **integrity**
     - *Replay attack* — capture and resend message
     - *Alteration* — change original message
  3. **Fabrication (Masquerade)** — affects **authenticity** (authentication)

**🔑 Exam connection:** Each security principle maps to a specific attack type. Know this mapping!

| Principle | Compromised by |
|-----------|---------------|
| Confidentiality | Interception (passive) |
| Authentication | Fabrication (active) |
| Integrity | Modification (active) |
| Availability | Interruption (active) |

---

# ═══════════════════════════════════════════════
# TOPIC 2: Cryptographic Concepts and Techniques
# ═══════════════════════════════════════════════

## 2.1 Cryptography Terminology ⭐⭐⭐

| Term | Definition |
|------|-----------|
| **Cryptography** | Art and science of encoding messages to make them non-readable |
| **Cryptanalysis** | Technique of decoding messages without knowing the key (breaking a code) |
| **Cryptology** | Combination of cryptography + cryptanalysis |
| **Plaintext (Clear text)** | Message readable by anyone |
| **Ciphertext** | Codified plaintext that cannot be read by unintended recipients |
| **Encryption** | Process of transforming plaintext → ciphertext |
| **Decryption** | Process of transforming ciphertext → plaintext |

**How it works:**
```
Sender → Plaintext → [Encryption Algorithm + Key] → Ciphertext → Transmission Channel
→ [Decryption Algorithm + Key] → Plaintext → Recipient
```

**Key insight:** Encryption is a **2-way function** — there is always a way to decrypt. The algorithm is usually public; it's the **key** that makes it secure.

---

## 2.2 Techniques for Plaintext to Ciphertext ⭐⭐

Two fundamental approaches (+ a combination):

1. **Substitution** — replace characters with other characters/numbers/symbols
2. **Transposition** — rearrange (permute) the order of characters
3. **Product cipher** — uses BOTH substitution and transposition

---

## 2.3 Substitution Techniques ⭐⭐⭐

### a. Shift Cipher (Caesar Cipher) ⭐⭐
- Each letter is replaced by a letter a **fixed number of positions** down the alphabet (wraps around)
- Caesar cipher specifically uses a shift of **3**
- **Encryption:** character = character + key
- **Decryption:** character = character - key

**Worked Example (Key = 5):**
```
Plaintext:    A  T  T  A  C  K  A  T  D  A  W  N
              ↓  ↓  ↓  ↓  ↓  ↓  ↓  ↓  ↓  ↓  ↓  ↓
Ciphertext:   F  Y  Y  F  H  P  F  Y  I  F  B  S
```

**How to break it:** Brute-force attack — try all 25 possible shifts. Only 25 possibilities!

**🔑 Numerical approach:** If asked to decrypt, shift each ciphertext letter backward by the key value.

### b. Mono-alphabet Cipher ⭐⭐
- Uses **random substitution** — no relationship between replacements
- **Much harder to break** than Shift Cipher
- Possible keys: **26! = 4.03 × 10²⁶** permutations
- **How to break:** **Frequency Analysis** — count occurrences of each letter. In English, E, T, A are most frequent.

**Worked Example:**
```
Plaintext alphabet:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Ciphertext alphabet: M U A L V O Z K R N J X Q D F S H P E B C T I W Y G

Plaintext:    A  T  T  A  C  K  A  T  D  A  W  N
Ciphertext:   M  B  B  M  A  J  M  B  L  M  U  I  D
```

### c. Vernam Cipher (One-Time Pad) ⭐⭐
- Uses a **random, non-repeating key** (one-time pad) of the **same length** as plaintext
- Key is **never reused** — this makes it highly secure
- Suitable for **short messages**
- **Encryption:** (Plaintext + OTP) mod 26
- **Decryption:** (Ciphertext - OTP) mod 26 (if negative, add 26)

**Worked Example (Plaintext = HELLO, OTP = WORLD):**
```
Step 1: Encode letters (A=0, B=1, ... Z=25)

Plaintext:     H   E   L   L   O
PT values:     7   4   11  11  14
OTP:           W   O   R   L   D
OTP values:    22  14  17  11  3
Sum:           29  18  28  22  17
Mod 26:        3   18  2   22  17
Ciphertext:    D   S   C   W   R

Decryption (CT - OTP):
CT values:     3   18  2   22  17
OTP values:    22  14  17  11  3
Subtract:      -19 4   -15 11  14
Mod 26:        7   4   11  11  14
Plaintext:     H   E   L   L   O
```

**🔑 For negative mod:** Add 26 to make it positive. E.g., -19 mod 26 = -19 + 26 = 7

---

## 2.4 Transposition Techniques ⭐⭐

### a. Rail Fence Cipher
- Write plaintext in **diagonals** forming 2 rows, then read **row by row**

**Encryption (Plaintext = HELLOWORLD):**
```
Write in 2 rows (diagonals):
Rail 1: H  L  O  O  L    (positions 1,3,5,7,9)
Rail 2: E  L  W  R  D    (positions 2,4,6,8,10)

Read row by row → Ciphertext: HLOOLELWRD

Decryption:
Split into 2 halves: Rail 1 = HLOOL, Rail 2 = ELWRD
Interleave: H-E-L-L-O-W-O-R-L-D = HELLOWORLD ✓
```
Last 5: E L W R D → Rail 2

Read diagonally:
H . L . O . O . L
. E . L . W . R . D

→ H E L L O W O R L D = HELLOWORLD ✓
```

### b. Columnar Transposition Cipher ⭐⭐
- Write plaintext **row by row** in a matrix with width = length of key
- Read **column by column** in order of alphabetical position of key letters

**Worked Example (Key = HACK, Plaintext = TREE IS GREEN):**
```
Key letters: H  A  C  K
Alphabetical rank: 3  1  2  4

Matrix (plaintext fills left→right, row by row):
         H(rank3) A(rank1) C(rank2) K(rank4)
Row 1:    T        R        E        E
Row 2:    _        I        S        _       (spaces → _)
Row 3:    G        R        E        E
Row 4:    N        _        _        _

Read columns in rank order 1(A), 2(C), 3(H), 4(K):
Col A (rank 1): R, I, R, _     → RIR_
Col C (rank 2): E, S, E, _     → ESE_
Col H (rank 3): T, _, G, N     → T_GN
Col K (rank 4): E, _, E, _     → E_E_

Ciphertext: RIR_ESE_T_GNE_E_ ✓

**🔑 Key concept:** Plaintext fills the matrix row-by-row under the key columns. Then read columns in alphabetical order of the key letters. Use underscores (_) for empty spaces.

**Decryption:** Reverse the process — write ciphertext into columns in alphabetical order, then read row by row.

**Worked Example (Key = WORLD, Plaintext = "SECURITY IS IMPORTANT")** — from tutorial:
- Key length = 5, Alphabetical order: D(1), L(2), O(3), R(4), W(5)
- Fill 20 chars into 4 rows × 5 columns
- Read columns in order D, L, O, R, W

---

## 2.5 Confusion vs Diffusion ⭐⭐

| Property | Confusion | Diffusion |
|----------|-----------|-----------|
| **What it protects** | Relationship between ciphertext and **key** | Relationship between ciphertext and **plaintext** |
| **Effect of changing 1 bit** | Ciphertext changes significantly | Ciphertext changes significantly (~half the bits) |
| **Achieved by** | **Substitution** | **Transposition** |
| **Used by** | Stream cipher AND Block cipher | Block cipher only |

---

## 2.6 Symmetric vs Asymmetric Algorithms (Overview) ⭐⭐

| Feature | Symmetric | Asymmetric |
|---------|-----------|------------|
| Keys | Same key for encrypt & decrypt | Different keys (public + private) |
| Key distribution | Problem (how to share the key?) | No problem (public key is shared) |
| Number of keys for n parties | n(n-1)/2 | n pairs (2n keys) |
| Speed | Faster | Slower |

---

## 2.7 Diffie-Hellman Key Exchange ⭐⭐⭐

**Purpose:** Allows two parties to agree on a shared symmetric key over an **insecure channel** WITHOUT transmitting the key itself. DH is for **key exchange only**, NOT for encryption.

**Steps (Mathematical):**
1. Alice and Bob agree on two large prime numbers **n** and **g** (public)
2. Alice chooses secret **x**, calculates **A = gˣ mod n**, sends A to Bob
3. Bob chooses secret **y**, calculates **B = gʸ mod n**, sends B to Alice
4. Alice calculates **K₁ = Bˣ mod n**
5. Bob calculates **K₂ = Aʸ mod n**
6. **K₁ = K₂ = K** (the shared secret key!)

**Why it works:** gˣʸ mod n = gʸˣ mod n (exponents commute)

**Worked Example (n=11, g=7, x=3, y=6):**
```
Step 1: n=11, g=7 (publicly agreed)
Step 2: A = 7³ mod 11 = 343 mod 11 = 2
Step 3: B = 7⁶ mod 11 = 117649 mod 11 = 4
Step 4: K₁ = 4³ mod 11 = 64 mod 11 = 9
Step 5: K₂ = 2⁶ mod 11 = 64 mod 11 = 9
Result: K₁ = K₂ = 9 ✓
```

**🔑 You MUST be able to do this calculation on the test!**

### MITM Attack on Diffie-Hellman ⭐⭐
- Attacker (Tom) intercepts A and B, substitutes his own A' and B'
- Tom creates shared key K₂' with Alice and K₁' with Bob
- Both Alice and Bob think they're communicating securely with each other
- **Prevention:** Parties must **mutually authenticate** each other BEFORE the DH exchange

---

## 2.8 Key Range and Key Size ⭐

- **Key Range** = number of possible keys = 2^(key size)
- Bigger key range → harder to brute-force

| Key Size | Key Range |
|----------|-----------|
| 40 bits | 2⁴⁰ ≈ 1.1 × 10¹² |
| 64 bits | 2⁶⁴ ≈ 1.8 × 10¹⁹ |
| 128 bits | 2¹²⁸ ≈ 3.4 × 10³⁸ |

**Current practice:** Symmetric ≥ 256 bits, Asymmetric ≥ 2048 bits

---

## 2.9 Types of Cryptanalytic Attacks ⭐⭐

| Attack Type | What Cryptanalyst Knows |
|-------------|------------------------|
| **Ciphertext Only** | Encryption algorithm + ciphertext |
| **Known Plaintext** | Algorithm + ciphertext + one or more PT-CT pairs |
| **Chosen Plaintext** | Algorithm + ciphertext + PT chosen by attacker + its CT |
| **Chosen Ciphertext** | Algorithm + ciphertext + CT chosen by attacker + its decrypted PT |
| **Chosen Text** | Both chosen plaintext AND chosen ciphertext |

**Difficulty order:** Ciphertext Only (hardest) → ... → Chosen Text (easiest)

---

# ═══════════════════════════════════════════════
# TOPIC 3: Symmetric Algorithms
# ═══════════════════════════════════════════════

## 3.1 Algorithm Types ⭐⭐

| Feature | Stream Cipher | Block Cipher |
|---------|--------------|--------------|
| Encryption unit | **Bit by bit** | **Block by block** |
| When message is available | As it's being typed/produced | Entire message available at encryption time |
| Example use | Real-time messaging | File encryption |

### Stream Cipher — XOR Operation ⭐⭐
- XOR (Exclusive OR): true when **exactly one** input is true
- **Reversible:** P XOR K = C, then C XOR K = P

```
Truth Table:          Encryption:           Decryption:
A  B  A⊕B             Plaintext:  01100011   Ciphertext: 00110110
0  0   0               Key:        01010101   Key:        01010101
0  1   1               Ciphertext: 00110110   Plaintext:  01100011
1  0   1
1  1   0
```

### Block Cipher — Weakness and Solution ⭐
- **Weakness:** Repeating plaintext blocks produce repeating ciphertext blocks → patterns visible to cryptanalyst
- **Solution:** Use **chaining mode** — mix previous ciphertext block with current plaintext block

---

## 3.2 Confusion and Diffusion (Revisited for Symmetric) ⭐⭐

| | Confusion | Diffusion |
|---|-----------|-----------|
| **Definition** | Ciphertext gives no clue about plaintext | Spreads plaintext redundancy across rows/columns |
| **Achieved by** | Substitution | Transposition (permutation) |
| **Used in** | Stream AND Block ciphers | Block ciphers only |

---

## 3.3 Algorithm Modes ⭐⭐⭐

Four modes for block ciphers — adds randomness so the cipher isn't predictable:

### i. Electronic Code Book (ECB) ⭐⭐
- Each 64-bit block encrypted **independently** with the same key
- **Weakness:** If plaintext blocks repeat, ciphertext blocks also repeat
- **Best for:** Short plaintext only

```
PT Block 1 → Encrypt(K) → CT Block 1
PT Block 2 → Encrypt(K) → CT Block 2
PT Block n → Encrypt(K) → CT Block n
```

### ii. Cipher Block Chaining (CBC) ⭐⭐⭐
- Adds **feedback** mechanism — each ciphertext block is XORed with the next plaintext block before encryption
- Uses an **Initialization Vector (IV)** for the first block
- **IV properties:** Random 64-bit block, makes each message unique, same PT + different IV = different CT. IV need not be secret (but is usually kept secret in practice)

**CBC Encryption (MUST KNOW):**
```
Step 1: ITB₁ = IV ⊕ PTB₁    →    CTB₁ = Encrypt(ITB₁, K)
Step 2: ITB₂ = CTB₁ ⊕ PTB₂  →    CTB₂ = Encrypt(ITB₂, K)
Step n: ITBₙ = CTBₙ₋₁ ⊕ PTBₙ →   CTBₙ = Encrypt(ITBₙ, K)
```

**CBC Decryption:**
```
Step 1: OTB₁ = Decrypt(CTB₁, K)    →    PTB₁ = OTB₁ ⊕ IV
Step 2: OTB₂ = Decrypt(CTB₂, K)    →    PTB₂ = OTB₂ ⊕ CTB₁
Step n: OTBₙ = Decrypt(CTBₙ, K)    →    PTBₙ = OTBₙ ⊕ CTBₙ₋₁
```

**🔑 You may be asked to trace through CBC encryption/decryption step by step!**

### iii. Cipher Feedback (CFB) ⭐
- Works on block ciphers **acting as stream ciphers**
- **Ciphertext bits** are fed to the next stage of encryption
- Uses a **left shift register**
- **Process:** IV placed in shift register → encrypted → leftmost j bits XOR with plaintext j bits → ciphertext. Then shift register shifts left, ciphertext bits added to register.

### iv. Output Feedback (OFB) ⭐
- Similar to CFB but **output bits** (not ciphertext) are fed to next stage
- **Advantage over CFB:** Bit errors do NOT propagate
- **Disadvantage vs CFB:** Attacker can change data and checksum simultaneously undetected

**🔑 Mode Comparison Table:**

| Mode | ECB | CBC | CFB | OFB |
|------|-----|-----|-----|-----|
| Feedback | None | CT block | CT bits | Output bits |
| IV needed | No | Yes | Yes | Yes |
| Repeating PT blocks | Repeating CT ❌ | Different CT ✓ | Different CT ✓ | Different CT ✓ |
| Works as | Block cipher | Block cipher | Block/Stream | Block/Stream |
| Error propagation | No | Yes (1 block) | Yes | No ✓ |

---

## 3.4 Bit Rotation and Shifting ⭐

Used in CFB and OFB shift registers:

| Operation | Description | Input: 01010011 | Result |
|-----------|-------------|-----------------|--------|
| Left Shift (LS) | Drop first bit, shift left, fill with ? | 01010011 | 1010011? |
| Right Shift (RS) | Drop last bit, shift right, fill with ? | 01010011 | ?0101001 |
| Left Rotation (LR) | First bit wraps to end | 01010011 | 10100110 |
| Right Rotation (RR) | Last bit wraps to front | 01010011 | 10101001 |

---

## 3.5 DES (Data Encryption Standard) ⭐⭐⭐

**Key facts:**
- Developed by **IBM** in early 1970s
- **Block cipher**: 64-bit block size
- **Key**: 56 bits (+ 8 parity bits = 64 bits total)
- Based on **Feistel Cipher Structure**
- Superseded by **AES** in 2005

### Broad Level Steps ⭐⭐

```
64-bit Plaintext
    ↓
Step 1: Initial Permutation (IP) — transposition using IP table
    ↓
Step 2: Split into LPT (32-bit) and RPT (32-bit)
    ↓
Step 3: 16 rounds of encryption (each round: confusion + diffusion)
    ↓
Step 4: Recombine LPT and RPT
    ↓
Step 5: Final Permutation (FP)
    ↓
64-bit Ciphertext
```

### Details of One DES Round ⭐⭐⭐

Each round has 5 sub-steps:

**a) Key Transformation**
- 64-bit key → discard every 8th bit → 56-bit key
- 56-bit key split into two 28-bit halves
- **Circular left shift** on each half (1 bit for rounds 1,2,9,16; 2 bits for all others)
- **Compression permutation**: 56-bit → 48-bit subkey

**b) Expansion Permutation**
- 32-bit RPT → expanded to **48 bits**
- 32-bit RE divided into 8 blocks of 4 bits → each expanded to 6 bits

**c) S-Box Substitution** ⭐⭐
- 48-bit input → broken into 8 × 6-bit sub-blocks
- Each 6-bit sub-block → **4-bit output** via S-Box lookup
- **How S-Box works:** For each 6-bit input, bits 1 and 6 (outer bits) = **row number**, bits 2-5 (middle bits) = **column number**. Look up S-Box table for 4-bit output.
- **Result:** 48 bits → 32 bits

```
Input: B1 B2 B3 B4 B5 B6
       ↓              ↓
    Row number    Row number
       ↓   ↓   ↓   ↓
      Column number

Example: Input 110111
Row = B1B6 = 11 = 3
Column = B2B3B4B5 = 1011 = 11
Look up S-Box at row 3, column 11 → 4-bit output
```

**d) P-Box Permutation**
- 32-bit S-Box output is permuted using P-Box table

**e) XOR and Swap**
- 32-bit P-Box output ⊕ LPT → new RPT
- Old RPT → new LPT
- One round complete → repeat 16 times

### Final Permutation (FP)
- Performed **once** after 16 rounds
- Rejoins LPT and RPT → applies FP table → 64-bit ciphertext

### DES Decryption
- **Same algorithm** as encryption
- **Only difference:** Keys are applied in **reverse order** (K₁₆, K₁₅, ..., K₁ instead of K₁, K₂, ..., K₁₆)

### DES Analysis ⭐
- **DES cracked in 1998 and 1999** (22 hours with 100,000 computers)
- 56-bit key → 2⁵⁶ ≈ 7.2 × 10¹⁶ possible keys
- Brute force at 1 DES/μs → 1000 years (theoretical), but distributed computing broke it

---

## 3.6 Modified Versions of DES ⭐⭐

### Double DES
- Encrypt twice with two different keys (K₁ then K₂)
- Problem: vulnerable to **meet-in-the-middle attack**

### Triple DES ⭐⭐
**With 3 keys:**
```
Encrypt(K₁) → Decrypt(K₂) → Encrypt(K₃)
```

**With 2 keys:**
```
Encrypt(K₁) → Decrypt(K₂) → Encrypt(K₁)
```

Note: Decryption in the middle is for backward compatibility with single DES.

---

## 3.7 Other Symmetric Algorithms ⭐

| Algorithm | Notes |
|-----------|-------|
| **RC5** (Rivest Cipher) | 64-bit version cracked after 1757 days (~4.8 years) |
| **Blowfish** | Designed by B. Schneier (1993), **never cracked** |
| **AES (Rijndael)** | Superseded DES as US federal standard in 2002. **AES-256 never cracked** |

---

# ═══════════════════════════════════════════════
# TOPIC 4: Asymmetric Algorithms
# ═══════════════════════════════════════════════

## 4.1 Asymmetric Key Cryptography ⭐⭐⭐

**Core concept:** Uses **two different keys** — a **public key** (shared with everyone) and a **private key** (kept secret by owner).

**For n communicating parties:**
- Symmetric: **n(n-1)/2** keys needed
- Asymmetric: **n pairs** (each person has 1 key pair)

### Which key to use? ⭐⭐⭐

| Goal | Encrypt with | Decrypt with |
|------|-------------|-------------|
| **Confidentiality** | Recipient's **public** key | Recipient's **private** key |
| **Non-repudiation / Authentication** | Sender's **private** key | Sender's **public** key |

**Confidentiality example:** Customers encrypt messages with ABC Bank's public key → only the bank can decrypt with its private key.

**Authentication example:** For digital signature — signer encrypts hash of document with their private key. Receiver decrypts with signer's public key. If hashes match, signer is authenticated. Signer **cannot deny** signing (non-repudiation) because only they have the private key.

---

## 4.2 RSA Algorithm ⭐⭐⭐⭐

**THE most testable topic — you WILL get numerical questions!**

**Named after:** Rivest, Shamir, Adleman (1977)
**Based on:** The difficulty of factoring the product of two large prime numbers
**Used in:** SSL (Secure Sockets Layer) for web browsing security

### Mathematical Foundations ⭐⭐

**a) Integers:** ..., -3, -2, -1, 0, 1, 2, 3, ...

**b) Integer Division:** a = q × n + r
- Example: 33 ÷ 5 → a=33, n=5, q=6, r=3 → 33 = 6×5 + 3

**c) Divisibility:** When r=0, n divides a (written as n | a)
- Example: 35 ÷ 5 = 7 remainder 0 → 5 | 35

**d) Greatest Common Divisor (GCD):**
- Largest integer that divides both numbers
- **Euclidean Algorithm:** gcd(a,0) = a; gcd(a,b) = gcd(b, a mod b)

```
gcd(36, 20) = gcd(20, 16) = gcd(16, 4) = gcd(4, 0) = 4
```

**e) Modular Arithmetic:** a mod n = r (the remainder)
- 33 mod 5 = 3
- **Negative numbers:** -33 mod 5 → remainder is -3, add 5 → -3 + 5 = 2 → **-33 mod 5 = 2** ⭐

**Modular Properties:**
```
(a + b) mod n = [(a mod n) + (b mod n)] mod n
(a - b) mod n = [(a mod n) - (b mod n)] mod n
(a × b) mod n = [(a mod n) × (b mod n)] mod n
```

**f) Prime Numbers:** Divisible only by 1 and itself (1, 2, 3, 5, 7, 11, ...)
**Coprime:** gcd(a,b) = 1. E.g., gcd(5,2) = 1 → 5 and 2 are coprime.

### RSA Algorithm Steps ⭐⭐⭐

```
1. Choose two large primes P and Q
2. Calculate N = P × Q
3. Select encryption key E such that E has NO common factor with (P-1)(Q-1)
4. Calculate decryption key D such that: (D × E) mod (P-1)(Q-1) = 1
5. Encryption: CT = PTᴱ mod N
6. Decryption: PT = CTᴰ mod N
```

**Public key:** (E, N) — shared with everyone
**Private key:** D — kept secret by owner
**P, Q:** Kept secret, never revealed

### RSA Worked Example ⭐⭐⭐

**Given: P = 7, Q = 17**

**Step 1-2:** N = 7 × 17 = **119**

**Step 3:** (P-1)(Q-1) = 6 × 16 = **96**
- Factors of 96: 1, 2, 3, 4, 6, 8, 12, 16, 24, 32, 48, 96
- Choose E = 5 (no common factor with 96) ✓

**Step 4:** Find D where 5D mod 96 = 1
- 5D = 96y + 1 for some integer y
- Try y=4: D = (96×4 + 1)/5 = 385/5 = **77**
- Verify: 5 × 77 = 385 = 4 × 96 + 1 ✓

**Step 5:** Encrypt letter 'F' (A=1, B=2, ..., F=6)
- CT = 6⁵ mod 119
- 6⁵ = 7776
- 7776 mod 119 = **41** (7776 = 65 × 119 + 41)

**Step 6:** Decrypt: PT = 41⁷⁷ mod 119 = **6** = 'F' ✓

### RSA Implementation Summary ⭐⭐
```
Owner:  1. Keeps P, Q secret
        2. Calculates N = P×Q
        3. Selects E (public key)
        4. Calculates D (private key) — ONLY owner can do this
        5. Publishes N and E

Sender: 6. Encrypts message: CT = PTᴱ mod N using public (E, N)
        7. Sends CT to owner

Owner:  8. Decrypts: PT = CTᴰ mod N using private D
```

### Why RSA is Secure ⭐⭐
- Easy to multiply large primes: N = P × Q
- Extremely difficult to factor N back to P and Q (if N is ~100 digits)
- To find D, you need P and Q → you need to factor N
- With only E and N, finding D is computationally infeasible

---

## 4.3 Other Asymmetric Algorithms ⭐

| Algorithm | Key Feature |
|-----------|-------------|
| **ECC (Elliptic Curve Cryptography)** | Higher cryptographic strength with **shorter keys**. Fast, efficient — suitable for mobile/portable devices. Used in SHA-2 and ECDSA. |
| **ElGamal** | Based on Diffie-Hellman |
| **Diffie-Hellman** | Key exchange (covered in Topic 2) |

---

## 4.4 Digital Envelope ⭐⭐

**Problem:** Asymmetric algorithms are **slow**. Encrypting large messages with RSA is impractical.

**Solution:** Use symmetric encryption for the message, asymmetric encryption for the key.

```
Sender side:
1. Generate a random symmetric key (Sym Key)
2. Encrypt plaintext with Sym Key → Ciphertext (fast, symmetric)
3. Encrypt Sym Key with recipient's PUBLIC key → Encrypted Sym Key (asymmetric)
4. Send both: Ciphertext + Encrypted Sym Key

Recipient side:
5. Decrypt Encrypted Sym Key with own PRIVATE key → Sym Key
6. Decrypt Ciphertext with Sym Key → Plaintext
```

**What a digital envelope contains:**
1. Encrypted Symmetric Key
2. Ciphertext
3. Symmetric Algorithm used
4. Asymmetric Algorithm used

---

## 4.5 Symmetric vs Asymmetric — Full Comparison ⭐⭐⭐

| Characteristic | Symmetric | Asymmetric |
|----------------|-----------|------------|
| **Key used** | Same key for encrypt & decrypt | Different keys for encrypt & decrypt |
| **Speed** | **Very fast** | Slower |
| **Ciphertext size** | Usually ≤ plaintext size | ≥ plaintext size |
| **Key exchange** | **Big problem** | No problem (public key) |
| **Keys for n participants** | n(n-1)/2 (scalability issue) | n pairs (scales well) |
| **Usage** | Encryption/decryption only (confidentiality) | Encryption/decryption + digital signature (integrity + non-repudiation) |

---

# ═══════════════════════════════════════════════
# 🎯 PRACTICE PROBLEMS (from Tutorials)
# ═══════════════════════════════════════════════

## Tutorial 1 (Topic 1)
1. What are the key principles of security?
2. Why is confidentiality an important principle of security?
3. Discuss the reasons behind the significance of authentication.
4. In real life, how is message integrity ensured?
5. What is repudiation? How can it be prevented in real life?
6. What is access control? How different is it from availability?
7. Why are some attacks called passive? Why are some called active?
8. What are two categories of passive attacks?
9. What are three categories of active attacks?

## Tutorial 2 (Topic 2)
1. What are the two basic ways of transforming plaintext into ciphertext?
2. Difference between Substitution Cipher and Transposition Cipher?
3. How can Caesar Cipher be cracked? (Brute force — 25 possibilities)
4. What is Mono-alphabetic Cipher? How different from Caesar?
5. Why is Mono-alphabetic hard to crack? How to crack it? (Frequency analysis)
6. Discuss the Rail Fence algorithm.
7. **Columnar Transposition:** Plaintext = "SECURITY IS IMPORTANT", Key = "WORLD". Generate ciphertext.
8. **Diffie-Hellman:** n=11, g=7, x=3, y=6. Find the symmetric key. (= 9)
9. Discuss DH MITM attack with example.
10. Counter-measure against DH MITM? (Mutual authentication before exchange)

## Tutorial 3.1 (Topic 3a)
1. Two types of cipher? (Stream, Block)
2. Distinguish stream and block ciphers.
3. Weakness of block cipher? Solution? (Repeating patterns; chaining mode)
4. What is confusion? How achieved? Which ciphers use it?
5. What is diffusion? How achieved? Which ciphers use it?
6. Four modes of cipher? (ECB, CBC, CFB, OFB)
7. Discuss each algorithm mode in detail.
8. What is IV? Its significance?
9. Problems with symmetric key encryption? (Key distribution, multiple keys, key management)

## Tutorial 3.2 (Topic 3b)
1. Broad level steps in DES (with diagram).
2. Details of each DES round (with diagram).
3. Difference between DES encryption and decryption? (Key order reversed)
4. How is Double DES performed?
5. Difference between Triple DES with 2 vs 3 keys?

## Tutorial 4.1 (Topic 4a)
1. Steps to send message securely using asymmetric algorithm.
2. Given a = q × n + r, what are a, q, n, r? (dividend, quotient, divisor, remainder)
3. Find quotient and remainder of 58/11. What are 58 and 11 called?
4. Find divisors of 27 and 12. Common divisors? gcd(27,12)? (gcd = 3)
5. Find 58 mod 5 and -16 mod 5. (58 mod 5 = 3, -16 mod 5 = 4)

## Tutorial 4.2 (Topic 4b)
6. Describe RSA algorithm.
7. **RSA numerical:** P=11, Q=3. Find E and D. Encode "F". Find ciphertext. ⭐⭐⭐
8. Which parameters does recipient send to sender? (N and E — the public key)
9. Why is RSA hard to crack? (Factoring large N is computationally infeasible)
10. Advantages/disadvantages of symmetric vs asymmetric.

---

# ═══════════════════════════════════════════════
# 📝 QUICK-FIRE MCQ REVISION
# ═══════════════════════════════════════════════

1. **Q:** What are the 6 security principles?
   **A:** Confidentiality, Authentication, Integrity, Non-Repudiation, Access Control, Availability

2. **Q:** Confidentiality is compromised by?
   **A:** Interception

3. **Q:** Authentication is compromised by?
   **A:** Fabrication (masquerade)

4. **Q:** Integrity is compromised by?
   **A:** Modification (alteration or replay)

5. **Q:** Availability is compromised by?
   **A:** Interruption (DoS)

6. **Q:** What provides non-repudiation?
   **A:** Digital signature

7. **Q:** What is 2FA?
   **A:** Using 2 out of 3 authentication factors (know, have, are)

8. **Q:** Passive attacks are harder to ______ than active attacks.
   **A:** Detect

9. **Q:** Two types of passive attacks?
   **A:** Eavesdropping/release of message contents, Traffic analysis

10. **Q:** Three types of active attacks?
    **A:** Interruption, Modification, Fabrication

11. **Q:** Cryptography + Cryptanalysis = ?
    **A:** Cryptology

12. **Q:** Two basic techniques for plaintext→ciphertext?
    **A:** Substitution and Transposition

13. **Q:** Caesar cipher uses a shift of?
    **A:** 3

14. **Q:** How many possible keys in mono-alphabetic cipher?
    **A:** 26! ≈ 4.03 × 10²⁶

15. **Q:** How to break mono-alphabetic cipher?
    **A:** Frequency analysis (E, T, A most common in English)

16. **Q:** Vernam cipher uses a ______ pad.
    **A:** One-time (random, non-repeating, same length as plaintext)

17. **Q:** Confusion is achieved by?
    **A:** Substitution

18. **Q:** Diffusion is achieved by?
    **A:** Transposition (permutation)

19. **Q:** Symmetric algorithms use how many keys for n parties?
    **A:** n(n-1)/2

20. **Q:** Asymmetric algorithms use how many key pairs for n parties?
    **A:** n pairs

21. **Q:** DH Key Exchange is used for ______, not for ______.
    **A:** Key exchange, encryption

22. **Q:** How to prevent DH MITM attack?
    **A:** Mutual authentication before exchange

23. **Q:** Current minimum symmetric key size?
    **A:** 256 bits

24. **Q:** Current minimum asymmetric key size?
    **A:** 2048 bits

25. **Q:** Stream cipher encrypts ______ by ______.
    **A:** Bit by bit

26. **Q:** Block cipher encrypts ______ by ______.
    **A:** Block by block

27. **Q:** Which ECB weakness is solved by CBC?
    **A:** Repeating plaintext blocks produce repeating ciphertext

28. **Q:** What is IV?
    **A:** Initialization Vector — random 64-bit block used in CBC/CFB/OFB to make each message unique

29. **Q:** DES block size and key size?
    **A:** 64-bit block, 56-bit key (+ 8 parity bits)

30. **Q:** How many rounds in DES?
    **A:** 16

31. **Q:** What does S-Box do in DES?
    **A:** Substitution — 48-bit input (8×6-bit) → 32-bit output (8×4-bit)

32. **Q:** In S-Box, which bits form the row and column?
    **A:** Bits 1,6 (outer) = row; bits 2-5 (middle) = column

33. **Q:** DES decryption difference from encryption?
    **A:** Keys applied in reverse order (K16→K1 instead of K1→K16)

34. **Q:** Triple DES with 3 keys uses which operation sequence?
    **A:** Encrypt(K1) → Decrypt(K2) → Encrypt(K3)

35. **Q:** AES replaced DES in what year?
    **A:** 2002 (US federal standard), 2005 (DES fully superseded)

36. **Q:** RSA is based on the difficulty of?
    **A:** Factoring the product of two large prime numbers

37. **Q:** RSA public key consists of?
    **A:** E and N

38. **Q:** In RSA, what must E NOT have in common with (P-1)(Q-1)?
    **A:** Any common factor (E and (P-1)(Q-1) must be coprime)

39. **Q:** RSA encryption formula?
    **A:** CT = PTᴱ mod N

40. **Q:** RSA decryption formula?
    **A:** PT = CTᴰ mod N

41. **Q:** For confidentiality with asymmetric, encrypt with whose key?
    **A:** Recipient's public key

42. **Q:** For authentication/non-repudiation, encrypt with whose key?
    **A:** Sender's private key

43. **Q:** Digital envelope encrypts the message with ______ key and the key with ______ key.
    **A:** Symmetric (fast), recipient's public (asymmetric)

44. **Q:** ECC advantage over RSA?
    **A:** Higher cryptographic strength with shorter keys, faster, suitable for mobile devices

45. **Q:** Which has NOT been cracked: RC5, Blowfish, or AES-256?
    **A:** Blowfish and AES-256 have never been cracked. RC5 (64-bit) was cracked.

---

# ═══════════════════════════════════════════════
# 🔑 KEY NUMERICAL METHODS TO PRACTICE
# ═══════════════════════════════════════════════

## 1. Caesar/Shift Cipher
- Encrypt: shift each letter FORWARD by key
- Decrypt: shift each letter BACKWARD by key
- Brute force: try all 25 shifts

## 2. Mono-alphabet Cipher
- Substitute using given key mapping
- Break with frequency analysis

## 3. Vernam Cipher (One-Time Pad)
- Encrypt: (PT + OTP) mod 26
- Decrypt: (CT - OTP) mod 26 (if negative, add 26)

## 4. Rail Fence Cipher
- Write diagonally in 2 rows, read row by row
- Decrypt: split into 2 halves, interleave

## 5. Columnar Transposition
- Write plaintext row-by-row (width = key length)
- Read column-by-column in alphabetical order of key letters

## 6. Diffie-Hellman
- A = gˣ mod n, B = gʸ mod n
- K₁ = Bˣ mod n = K₂ = Aʸ mod n

## 7. RSA
- N = P × Q
- (P-1)(Q-1) = φ
- Choose E coprime with φ
- Find D: (D × E) mod φ = 1
- Encrypt: CT = PTᴱ mod N
- Decrypt: PT = CTᴰ mod N

## 8. GCD (Euclidean Algorithm)
- gcd(a,0) = a
- gcd(a,b) = gcd(b, a mod b)

## 9. Modular Arithmetic
- a mod n = remainder when a divided by n
- Negative: add n until positive

## 10. XOR Operation
- 0⊕0=0, 0⊕1=1, 1⊕0=1, 1⊕1=0
- Reversible: P⊕K=C, then C⊕K=P

---

*Good luck on your test! Remember: the professor expects you to APPLY these concepts, not just define them. Practice the numerical problems until you can do them without looking at the formulas.*
