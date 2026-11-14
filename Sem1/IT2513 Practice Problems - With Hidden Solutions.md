# 📝 IT2513 Data Security — Practice Problems with Hidden Solutions
### Click to reveal answers • Based on your lecture slides and tutorials

---

# ═══════════════════════════════════════════════
# TOPIC 1: Need for Information Security
# ═══════════════════════════════════════════════

---

### Problem 1.1 — Match the Principle ⭐
**Match each security principle with the attack that compromises it.**

| Principle | Attack |
|-----------|--------|
| A. Confidentiality | 1. Modification |
| B. Authentication | 2. Interruption |
| C. Integrity | 3. Fabrication |
| D. Availability | 4. Interception |
| E. Non-Repudiation | 5. Repudiation |

<details>
<summary>🔓 Click to reveal solution</summary>

**Answers:**
- A. Confidentiality → **4. Interception** (eavesdropping/sniffing)
- B. Authentication → **3. Fabrication** (masquerade/impersonation)
- C. Integrity → **1. Modification** (alteration/replay)
- D. Availability → **2. Interruption** (DoS attack)
- E. Non-Repudiation → **5. Repudiation** (sender denies sending)

**Key insight:** Each principle has exactly ONE primary attack that breaks it. This mapping is essential for MCQs.

</details>

---

### Problem 1.2 — True or False ⭐
**State whether each statement is True or False. If False, correct it.**

1. Confidentiality and privacy mean the same thing.
2. Passive attacks are easier to detect than active attacks.
3. Authentication can be compromised by a modification attack.
4. A Man-in-the-Middle attack compromises authentication.
5. ACL is a superset of Access Control Matrix.
6. Using a password and fingerprint together is called 2FA.
7. A replay attack affects integrity.
8. Non-repudiation is provided by encryption alone.

<details>
<summary>🔓 Click to reveal solution</summary>

1. **FALSE.** Privacy is the *right* of an individual to control information about themselves. Confidentiality is the *assurance* that only authorized parties access information.

2. **FALSE.** Passive attacks are **harder** to detect because the attacker makes no modification to data — the transmission appears normal.

3. **FALSE.** Authentication is compromised by **fabrication** (masquerade), not modification. Modification compromises **integrity**.

4. **TRUE.** In MITM, the attacker pretends to be a legitimate party, which is a fabrication attack that compromises authentication.

5. **FALSE.** ACL is a **subset** of the Access Control Matrix. The matrix covers all subjects × objects; an ACL covers one object's permissions.

6. **TRUE.** Password = "what you know", fingerprint = "what you are". Using 2 out of 3 factors = 2FA.

7. **TRUE.** A replay attack captures a message and resends it — the original content is replayed but the context/integrity is compromised.

8. **FALSE.** Non-repudiation is provided by **digital signature**, not just encryption. A digital signature uses the sender's private key.

</details>

---

### Problem 1.3 — Short Answer ⭐⭐
**A company's financial system is attacked. An attacker intercepts wire transfer details. The attacker then changes the destination bank account number before the message reaches the recipient bank.**

(a) Which security principle is compromised during interception?
(b) Which security principle is compromised during the modification?
(c) Name the two types of active attacks demonstrated here.
(d) Suggest one countermeasure for each.

<details>
<summary>🔓 Click to reveal solution</summary>

**(a)** **Confidentiality** — the attacker intercepted (eavesdropped on) the wire transfer details.

**(b)** **Integrity** — the message was modified (the account number was changed).

**(c)** The two active attacks are:
- **Modification** (alteration) — changing the account number
- The overall scenario also shows **interception** (passive) first, then modification (active)

**(d) Countermeasures:**
- For interception → **Encryption** (ensures confidentiality)
- For modification → **Digital signatures / Hash functions** (ensures integrity)

</details>

---

### Problem 1.4 — Fill in the Blanks ⭐
**Complete the following:**

1. The 6 security principles are: Confidentiality, __________, Integrity, __________, Access Control, and __________.

2. __________ attacks are harder to detect because the attacker does not modify data.

3. Authentication can be verified using three factors: what you know, what you have, and __________.

4. __________ assures that only authorized parties can access information.

5. __________ assures that systems are available to authentic users all the time.

<details>
<summary>🔓 Click to reveal solution</summary>

1. Confidentiality, **Authentication**, Integrity, **Non-repudiation**, Access Control, and **Availability**.

2. **Passive** attacks are harder to detect.

3. What you **are** (biometrics — fingerprint, facial recognition, retina).

4. **Confidentiality** assures authorized access only.

5. **Availability** assures systems are available to authentic users.

</details>

---

# ═══════════════════════════════════════════════
# TOPIC 2: Cryptographic Concepts & Techniques
# ═══════════════════════════════════════════════

---

### Problem 2.1 — Terminology Fill-in ⭐
**Fill in the blanks:**

1. The art of encoding messages to make them non-readable is called __________.
2. The process of transforming plaintext to ciphertext is called __________.
3. The combination of cryptography and cryptanalysis is called __________.
4. The message that can be understood by anyone is called __________.
5. Encryption is a __________-way function.

<details>
<summary>🔓 Click to reveal solution</summary>

1. **Cryptography**
2. **Encryption**
3. **Cryptology**
4. **Plaintext** (or clear text)
5. **Two** (2-way) — there is always a way to decrypt

</details>

---

### Problem 2.2 — Caesar Cipher ⭐⭐
**Using a Caesar Cipher with key = 3, encrypt the plaintext: "HELLO WORLD"**

<details>
<summary>🔓 Click to reveal solution</summary>

**Method:** Shift each letter forward by 3 positions (wrapping around).

```
H + 3 = K
E + 3 = H
L + 3 = O
L + 3 = O
O + 3 = R
(space stays)
W + 3 = Z
O + 3 = R
R + 3 = U
L + 3 = O
D + 3 = G
```

**Ciphertext: KHOOR ZRUOG**

**To decrypt:** Shift each letter backward by 3.
K - 3 = H, H - 3 = E, O - 3 = L, etc. → "HELLO WORLD" ✓

</details>

---

### Problem 2.3 — Caesar Cipher Decryption ⭐⭐
**You intercept this Caesar Cipher ciphertext: "FYYFHP". Find the plaintext.**

<details>
<summary>🔓 Click to reveal solution</summary>

**Method:** Brute force — try all 25 possible shifts until meaningful text appears.

We know from the lecture that **shift = 5** decrypts it:

F(5) - 5 = A(0)
Y(24) - 5 = T(19)
Y(24) - 5 = T(19)
F(5) - 5 = A(0)
H(7) - 5 = C(2)
P(15) - 5 = K(10)

**Plaintext: ATTACK**

To verify: The attacker would try shifts 1 through 25. At shift 5, the result "ATTACK" makes sense as English text.

**Brute force table (selected):**
| Shift | Result |
|-------|--------|
| 1 | EXXEGO |
| 2 | DWWDFN |
| 3 | CVVCEM |
| 4 | BUUBDL |
| **5** | **ATTACK** ✓ |

</details>

---

### Problem 2.4 — Mono-alphabet Cipher ⭐⭐
**A mono-alphabet cipher uses this key alphabet:**

```
Plaintext:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Ciphertext: Q W E R T Y U I O P A S D F G H J K L Z X C V B N M
```

**Encrypt the plaintext: "SECURITY"**

<details>
<summary>🔓 Click to reveal solution</summary>

**Method:** Look up each plaintext letter in the top row, take the corresponding letter from the bottom row.

```
S → L
E → T
C → E
U → X
R → K
I → O
T → Z
Y → N
```

**Ciphertext: LTEXKOZN**

**To decrypt:** Look up each ciphertext letter in the bottom row, take the corresponding letter from the top row.

</details>

---

### Problem 2.5 — Vernam Cipher (One-Time Pad) ⭐⭐⭐
**Encrypt the plaintext "MATH" using Vernam cipher with the one-time pad "CODE".**

Show all steps: encoding, addition, mod 26, and decoding back to letters.

<details>
<summary>🔓 Click to reveal solution</summary>

**Step 1: Encode letters** (A=0, B=1, ... Z=25)

| Plaintext | M | A | T | H |
|-----------|---|---|---|---|
| PT value | 12 | 0 | 19 | 7 |

| OTP | C | O | D | E |
|-----|---|---|---|---|
| OTP value | 2 | 14 | 3 | 4 |

**Step 2: Add PT + OTP**

| | M+C | A+O | T+D | H+E |
|---|---|---|---|---|
| Sum | 12+2=14 | 0+14=14 | 19+3=22 | 7+4=11 |

**Step 3: Mod 26**

| Sum | 14 | 14 | 22 | 11 |
|-----|----|----|----|----|
| Mod 26 | 14 | 14 | 22 | 11 |

(All values are already < 26, so no change)

**Step 4: Decode**

| Value | 14 | 14 | 22 | 11 |
|-------|----|----|----|-----|
| Letter | O | O | W | L |

**Ciphertext: OOWL**

**Verification (Decryption — CT - OTP mod 26):**

| CT | O | O | W | L |
|----|---|---|---|---|
| CT value | 14 | 14 | 22 | 11 |
| OTP value | 2 | 14 | 3 | 4 |
| Subtract | 12 | 0 | 19 | 7 |
| Mod 26 | 12 | 0 | 19 | 7 |
| Letter | M | A | T | H | ✓

</details>

---

### Problem 2.6 — Vernam Cipher with Negative Mod ⭐⭐⭐
**Decrypt the ciphertext "DCWRO" using the one-time pad "WORLD".**

Show all steps including handling of negative values.

<details>
<summary>🔓 Click to reveal solution</summary>

**Step 1: Encode**

| Ciphertext | D | S | C | W | R |
|------------|---|---|---|---|---|
| CT value | 3 | 18 | 2 | 22 | 17 |

| OTP | W | O | R | L | D |
|-----|---|---|---|---|---|
| OTP value | 22 | 14 | 17 | 11 | 3 |

**Step 2: Subtract CT - OTP**

| | D-W | S-O | C-R | W-L | R-D |
|---|-----|-----|-----|-----|-----|
| Subtract | 3-22 = **-19** | 18-14 = 4 | 2-17 = **-15** | 22-11 = 11 | 17-3 = 14 |

**Step 3: Mod 26** (for negative values, add 26)

| Subtract | -19 | 4 | -15 | 11 | 14 |
|----------|-----|---|-----|----|----|
| +26 if negative | -19+26 = **7** | 4 | -15+26 = **11** | 11 | 14 |
| Final | 7 | 4 | 11 | 11 | 14 |

**Step 4: Decode**

| Value | 7 | 4 | 11 | 11 | 14 |
|-------|---|---|----|----|----|
| Letter | H | E | L | L | O |

**Plaintext: HELLO** ✓

**🔑 Remember:** When mod result is negative, add 26 until positive.
- -19 mod 26 = -19 + 26 = **7**
- -15 mod 26 = -15 + 26 = **11**

</details>

---

### Problem 2.7 — Rail Fence Cipher ⭐⭐
**Encrypt "CRYPTOGRAPHY" using Rail Fence cipher (2 rails).**

<details>
<summary>🔓 Click to reveal solution</summary>

**Plaintext:** C R Y P T O G R A P H Y (12 characters)

**Step 1: Write in 2 rails**

```
Rail 1 (odd positions 1,3,5,7,9,11):  C  Y  P  G  A  Y  → CYPGAY
Rail 2 (even positions 2,4,6,8,10,12): R  T  O  R  P  H  → RTORPH
```

**Step 2: Read row by row**

**Ciphertext: CYPGAYRTORPH**

**Decryption:**
- Ciphertext has 12 characters
- Split evenly: Rail 1 = CYPGAY (6 chars), Rail 2 = RTORPH (6 chars)
- Interleave: C-R-Y-T-P-O-G-R-A-P-H-Y → CRYPTOGRAPHY ✓

</details>

---

### Problem 2.8 — Columnar Transposition ⭐⭐⭐
**Encrypt "SECURITYISIMPORTANT" using Columnar Transposition with key "WORLD".**

Show the matrix and the reading order.

<details>
<summary>🔓 Click to reveal solution</summary>

**Key:** WORLD
**Key length:** 5
**Alphabetical ranking:** D=1, L=2, O=3, R=4, W=5

**Plaintext:** SECURITYISIMPORTANT (19 characters, pad with _ to fill 4 rows × 5 = 20)

**Step 1: Write plaintext row-by-row under key columns**

```
         W(5)    O(3)    R(4)    L(2)    D(1)
Row 1:    S       E       C       U       R
Row 2:    I       T       Y       I       S
Row 3:    I       M       P       O       R
Row 4:    T       A       N       T       _
```

**Step 2: Read columns in rank order (1,2,3,4,5)**

| Rank | Column | Letters |
|------|--------|---------|
| 1 | D | R, S, R, _ → **RSR_** |
| 2 | L | U, I, O, T → **UIOT** |
| 3 | O | E, T, M, A → **ETMA** |
| 4 | R | C, Y, P, N → **CYPN** |
| 5 | W | S, I, I, T → **SIIT** |

**Ciphertext: RSR_UIOTETMACYPNSIIT**

</details>

---

### Problem 2.9 — Diffie-Hellman Key Exchange ⭐⭐⭐
**Alice and Bob use Diffie-Hellman with n = 13, g = 5.**
- Alice's secret: x = 4
- Bob's secret: y = 3

(a) Calculate A (Alice sends to Bob)
(b) Calculate B (Bob sends to Alice)
(c) Calculate the shared key K from both sides
(d) Verify K₁ = K₂

<details>
<summary>🔓 Click to reveal solution</summary>

**Given:** n = 13, g = 5, x = 4 (Alice's secret), y = 3 (Bob's secret)

**(a) Alice calculates A:**
```
A = gˣ mod n = 5⁴ mod 13
5⁴ = 625
625 mod 13 = 625 ÷ 13 = 48 remainder 1
A = 1
```

**(b) Bob calculates B:**
```
B = gʸ mod n = 5³ mod 13
5³ = 125
125 mod 13 = 125 ÷ 13 = 9 remainder 8
B = 8
```

**(c) Alice calculates K₁ (using B from Bob):**
```
K₁ = Bˣ mod n = 8⁴ mod 13
8⁴ = 4096
4096 mod 13 = 4096 ÷ 13 = 315 remainder 1
K₁ = 1
```

**(d) Bob calculates K₂ (using A from Alice):**
```
K₂ = Aʸ mod n = 1³ mod 13
1³ = 1
1 mod 13 = 1
K₂ = 1
```

**Verification: K₁ = K₂ = 1** ✓

The shared symmetric key is **1**.

</details>

---

### Problem 2.10 — Diffie-Hellman MITM Attack ⭐⭐
**In a Diffie-Hellman exchange with n=11, g=7, Alice has x=3, Bob has y=9. An attacker Tom intercepts the exchange with his own secrets x'=8 and y'=6.**

(a) Calculate Alice's A, Bob's B, and Tom's A' and B'
(b) Show how Tom establishes separate shared keys with Alice and Bob
(c) Why are Alice and Bob unaware of the attack?

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) Calculate values:**

```
Alice: A = 7³ mod 11 = 343 mod 11 = 2
Bob:   B = 7⁹ mod 11 = 40353607 mod 11 = 8
Tom:   A' = 7⁸ mod 11 = 5764801 mod 11 = 9
Tom:   B' = 7⁶ mod 11 = 117649 mod 11 = 4
```

**(b) Tom's interception:**
- Alice sends A=2 to Bob → Tom intercepts and sends B'=4 to Alice instead
- Bob sends B=8 to Alice → Tom intercepts and sends A'=9 to Bob instead

**Key calculations:**
```
Alice: K₁ = B'ˣ mod n = 4³ mod 11 = 64 mod 11 = 9
Tom (with Alice): K₂' = Aʸ' mod n = 2⁶ mod 11 = 64 mod 11 = 9
→ K₁ = K₂' = 9 (shared between Alice and Tom)

Bob: K₂ = A'ʸ mod n = 9⁹ mod 11 = 387420489 mod 11 = 5
Tom (with Bob): K₁' = Bˣ' mod n = 8⁸ mod 11 = 16777216 mod 11 = 5
→ K₂ = K₁' = 5 (shared between Bob and Tom)
```

**(c) Alice and Bob are unaware because:**
- Alice thinks she shares key 9 with Bob (but it's actually with Tom)
- Bob thinks he shares key 5 with Alice (but it's actually with Tom)
- Tom can decrypt Alice's messages with K₂'=9, re-encrypt with K₁'=5, and forward to Bob
- Neither Alice nor Bob can detect the interception

**Prevention:** Mutually authenticate each other BEFORE starting the DH exchange.

</details>

---

### Problem 2.11 — Confusion and Diffusion ⭐
**Fill in the table:**

| Property | Confusion | Diffusion |
|----------|-----------|-----------|
| Protects relationship between | ciphertext and ___? | ciphertext and ___? |
| Achieved by | ___? | ___? |
| Used in which cipher type? | stream / block / both? | stream / block / both? |

<details>
<summary>🔓 Click to reveal solution</summary>

| Property | Confusion | Diffusion |
|----------|-----------|-----------|
| Protects relationship between | ciphertext and **key** | ciphertext and **plaintext** |
| Achieved by | **Substitution** | **Transposition (permutation)** |
| Used in which cipher type? | **Both** stream and block | **Block** cipher only |

</details>

---

### Problem 2.12 — Cryptanalytic Attacks ⭐
**For each attack type, state what the cryptanalyst knows:**

(a) Ciphertext Only Attack
(b) Known Plaintext Attack
(c) Chosen Plaintext Attack
(d) Chosen Ciphertext Attack
(e) Chosen Text Attack

<details>
<summary>🔓 Click to reveal solution</summary>

| Attack | Cryptanalyst knows |
|--------|-------------------|
| (a) Ciphertext Only | Encryption algorithm + Ciphertext only |
| (b) Known Plaintext | Algorithm + Ciphertext + One or more PT-CT pairs (same key) |
| (c) Chosen Plaintext | Algorithm + Ciphertext + PT chosen by attacker + its CT |
| (d) Chosen Ciphertext | Algorithm + Ciphertext + CT chosen by attacker + its decrypted PT |
| (e) Chosen Text | Both Chosen Plaintext AND Chosen Ciphertext |

**Difficulty order:** Ciphertext Only is the **hardest** (least info), Chosen Text is the **easiest** (most info).

</details>

---

# ═══════════════════════════════════════════════
# TOPIC 3: Symmetric Algorithms
# ═══════════════════════════════════════════════

---

### Problem 3.1 — Stream vs Block Cipher ⭐
**Distinguish between stream cipher and block cipher in terms of:**
(a) Encryption unit
(b) When message is available
(c) Example use case

<details>
<summary>🔓 Click to reveal solution</summary>

| Feature | Stream Cipher | Block Cipher |
|---------|--------------|--------------|
| (a) Encryption unit | **Bit by bit** | **Block by block** (fixed size) |
| (b) When message available | As it's being typed/produced (real-time) | Entire message available at encryption time |
| (c) Example use | Real-time messaging, voice streams | File encryption, stored data |

</details>

---

### Problem 3.2 — XOR Operation ⭐⭐
**Given: Plaintext P = 10110100, Key K = 11010110**

(a) Encrypt: C = P ⊕ K
(b) Decrypt: P = C ⊕ K (verify you get back the original plaintext)

<details>
<summary>🔓 Click to reveal solution</summary>

**XOR Truth Table:** 0⊕0=0, 0⊕1=1, 1⊕0=1, 1⊕1=0

**(a) Encryption:**
```
P: 1 0 1 1 0 1 0 0
K: 1 1 0 1 0 1 1 0
C: 0 1 1 0 0 0 1 0
```
**C = 01100010**

**(b) Decryption:**
```
C: 0 1 1 0 0 0 1 0
K: 1 1 0 1 0 1 1 0
P: 1 0 1 1 0 1 0 0
```
**P = 10110100** ✓ (matches original)

</details>

---

### Problem 3.3 — Block Cipher Weakness ⭐
**Explain why repeating plaintext blocks are a weakness of block cipher in ECB mode, and how CBC mode solves this.**

<details>
<summary>🔓 Click to reveal solution</summary>

**Weakness of ECB:**
- In ECB, each block is encrypted **independently** with the same key
- If two plaintext blocks have the **same content**, they produce **identical ciphertext blocks**
- A cryptanalyst can detect repeating patterns in the ciphertext, which reveals information about the plaintext structure

**How CBC solves this:**
- CBC adds a **feedback mechanism** — each plaintext block is XORed with the **previous ciphertext block** before encryption
- This means even identical plaintext blocks produce **different ciphertext blocks** because the XOR input is different each time
- An **Initialization Vector (IV)** is used for the first block to ensure the first block is also unique

</details>

---

### Problem 3.4 — Algorithm Modes Comparison ⭐⭐
**Fill in the comparison table for the four algorithm modes:**

| Feature | ECB | CBC | CFB | OFB |
|---------|-----|-----|-----|-----|
| Feedback type | | | | |
| IV needed? | | | | |
| Repeating PT → Repeating CT? | | | | |
| Works as stream cipher? | | | | |
| Error propagation? | | | | |

<details>
<summary>🔓 Click to reveal solution</summary>

| Feature | ECB | CBC | CFB | OFB |
|---------|-----|-----|-----|-----|
| Feedback type | None | Previous CT block | CT bits | Output bits |
| IV needed? | No | Yes | Yes | Yes |
| Repeating PT → Repeating CT? | **Yes** ❌ | No ✓ | No ✓ | No ✓ |
| Works as stream cipher? | No | No | **Yes** | **Yes** |
| Error propagation? | No | Yes (1 block) | Yes | **No** ✓ |

**Key differences:**
- OFB advantage: errors don't propagate
- OFB disadvantage: attacker can modify data + checksum simultaneously
- CFB feeds ciphertext back; OFB feeds output back

</details>

---

### Problem 3.5 — CBC Encryption Step-by-Step ⭐⭐⭐
**Encrypt "HELLO WORLD" (ASCII) using CBC mode. Given: IV = 1010, and a simplified 4-bit block cipher where Encrypt(X, K) = X ⊕ K for all blocks, with K = 1100.**

Assume: H=1000, E=0101, L=1100, L=1100, O=1111 (using 4-bit simplified encoding)

Show each step: XOR with IV/previous CT, then encrypt.

<details>
<summary>🔓 Click to reveal solution</summary>

**Given:** IV = 1010, K = 1100, Encrypt(X, K) = X ⊕ K

**Step 1:** Block 1: H = 1000
```
ITB₁ = IV ⊕ PT₁ = 1010 ⊕ 1000 = 0010
CT₁ = Encrypt(ITB₁, K) = 0010 ⊕ 1100 = 1110
```

**Step 2:** Block 2: E = 0101
```
ITB₂ = CT₁ ⊕ PT₂ = 1110 ⊕ 0101 = 1011
CT₂ = Encrypt(ITB₂, K) = 1011 ⊕ 1100 = 0111
```

**Step 3:** Block 3: L = 1100
```
ITB₃ = CT₂ ⊕ PT₃ = 0111 ⊕ 1100 = 1011
CT₃ = Encrypt(ITB₃, K) = 1011 ⊕ 1100 = 0111
```

**Step 4:** Block 4: L = 1100
```
ITB₄ = CT₃ ⊕ PT₄ = 0111 ⊕ 1100 = 1011
CT₄ = Encrypt(ITB₄, K) = 1011 ⊕ 1100 = 0111
```

**Results:**
| Block | Plaintext | ITB (XOR with IV/prev CT) | Ciphertext |
|-------|-----------|--------------------------|------------|
| 1 (H) | 1000 | 0010 | 1110 |
| 2 (E) | 0101 | 1011 | 0111 |
| 3 (L) | 1100 | 1011 | 0111 |
| 4 (L) | 1100 | 1011 | 0111 |

**Note:** Even though blocks 3 and 4 have the same plaintext (L=1100), the CBC chaining ensures the same CT only appears if both the PT AND the previous CT are identical — which happens here because CT₂ = CT₃. In real CBC with larger blocks and proper IV, this is much less likely.

</details>

---

### Problem 3.6 — Bit Rotation ⭐
**Given input: 10110101, perform:**
(a) Left Shift by 1 (LS1)
(b) Right Shift by 1 (RS1)
(c) Left Rotation by 1 (LR1)
(d) Right Rotation by 1 (RR1)

<details>
<summary>🔓 Click to reveal solution</summary>

**Input:** 1 0 1 1 0 1 0 1

**(a) Left Shift by 1:** Drop first bit, shift left, fill last bit with ?
```
Drop 1st bit (1): _0110101_
Result: 0110101_ (last bit unknown/vacant)
As shown in slides: 0110 101?
```

**(b) Right Shift by 1:** Drop last bit, shift right, fill first bit with ?
```
Drop last bit (1): _1011010_
Result: _1011010 (first bit unknown/vacant)
As shown in slides: ?101 1010
```

**(c) Left Rotation by 1:** First bit wraps to end
```
Original: 1 0 1 1 0 1 0 1
Rotate 1st bit (1) to back: 0 1 1 0 1 0 1 1
Result: 01101011
```

**(d) Right Rotation by 1:** Last bit wraps to front
```
Original: 1 0 1 1 0 1 0 1
Rotate last bit (1) to front: 1 1 0 1 1 0 1 0
Result: 11011010
```

</details>

---

### Problem 3.7 — DES Overview ⭐⭐
**List the 6 broad-level steps of DES encryption in order.**

<details>
<summary>🔓 Click to reveal solution</summary>

1. **Initial Permutation (IP)** — transposition of 64-bit plaintext using IP table
2. **Split** — divide into LPT (32-bit) and RPT (32-bit)
3. **16 Rounds** — each round performs confusion (substitution) and diffusion (transposition)
4. **Rejoin** — combine LPT and RPT back into 64-bit block
5. **Final Permutation (FP)** — transposition using FP table
6. **Output** — produces 64-bit ciphertext block

</details>

---

### Problem 3.8 — DES One-Round Details ⭐⭐⭐
**List the 5 sub-steps within each DES round, stating the bit-size transformation at each step.**

<details>
<summary>🔓 Click to reveal solution</summary>

| Step | Name | Transformation |
|------|------|---------------|
| a | **Key Transformation** | 56-bit key → shift + compression → **48-bit subkey** |
| b | **Expansion Permutation** | 32-bit RPT → expanded to **48 bits**; then XOR with 48-bit key → 48-bit output |
| c | **S-Box Substitution** | 48-bit input (8×6-bit blocks) → **32-bit output** (8×4-bit) |
| d | **P-Box Permutation** | 32-bit S-Box output → permuted 32-bit output |
| e | **XOR and Swap** | 32-bit P-Box output ⊕ LPT → new RPT; old RPT → new LPT |

**Bit sizes:** 56→48 (key), 32→48 (expansion), 48→32 (S-Box), 32→32 (P-Box and XOR/Swap)

</details>

---

### Problem 3.9 — S-Box Lookup ⭐⭐⭐
**Given a 6-bit input to an S-Box: 110111**

(a) Which bits form the row number?
(b) Which bits form the column number?
(c) What are the row and column values in decimal?

<details>
<summary>🔓 Click to reveal solution</summary>

**Input:** B1 B2 B3 B4 B5 B6 = 1 1 0 1 1 1

**(a) Row number:** Bits B1 and B6 (outer bits) = **1** and **1**
Row = 11 (binary) = **3** (decimal)

**(b) Column number:** Bits B2 B3 B4 B5 (middle bits) = **1 0 1 1**
Column = 1011 (binary) = **11** (decimal)

**(c) Values:**
- Row = **3**
- Column = **11**

You would then look up the S-Box table at Row 3, Column 11 to get the 4-bit output.

**Key rule:** Outer bits (1st and 6th) → row; Middle bits (2nd to 5th) → column.

</details>

---

### Problem 3.10 — DES Decryption ⭐
**How does DES decryption differ from DES encryption?**

<details>
<summary>🔓 Click to reveal solution</summary>

DES decryption uses the **exact same algorithm** as encryption. The **only difference** is the **reversal of the key schedule**:

- **Encryption** uses keys in order: K₁, K₂, K₃, ..., K₁₆
- **Decryption** uses keys in reverse: K₁₆, K₁₅, K₁₄, ..., K₁

This works because all operations in DES (IP, FP, S-Box, P-Box, XOR) are carefully designed to be **reversible**. The key reversal undoes the 16 rounds.

</details>

---

### Problem 3.11 — Triple DES ⭐⭐
**Draw the Triple DES encryption process using 3 keys. What is the sequence of operations?**

<details>
<summary>🔓 Click to reveal solution</summary>

**Triple DES with 3 keys (K₁, K₂, K₃):**

```
Plaintext
    ↓
Encrypt with K₁
    ↓
Ciphertext 1
    ↓
Decrypt with K₂  ← (decryption in the middle for backward compatibility)
    ↓
Ciphertext 2
    ↓
Encrypt with K₃
    ↓
Final Ciphertext
```

**Sequence:** Encrypt(K₁) → Decrypt(K₂) → Encrypt(K₃)

**With 2 keys:** Encrypt(K₁) → Decrypt(K₂) → Encrypt(K₁) — K₃ = K₁

**Why decrypt in the middle?** For backward compatibility with single DES: if K₁ = K₂ = K₃, then Triple DES = single DES.

</details>

---

### Problem 3.12 — Symmetric Key Problems ⭐
**List three problems with using symmetric key encryption.**

<details>
<summary>🔓 Click to reveal solution</summary>

1. **Key Distribution:** The sender and recipient need the same key — but how do you securely transmit the key to the recipient?

2. **Multiple Keys Required:** For n persons, you need n(n-1)/2 keys. For 4 people (A,B,C,D), that's 6 keys (AB, AC, AD, BC, BD, CD). This doesn't scale well.

3. **Key Management:** Issues include issuing keys, replacing expired keys, securely storing keys, and deciding who manages them.

</details>

---

# ═══════════════════════════════════════════════
# TOPIC 4: Asymmetric Algorithms
# ═══════════════════════════════════════════════

---

### Problem 4.1 — RSA Fundamentals ⭐
**For RSA, what is the public key and what is the private key?**

<details>
<summary>🔓 Click to reveal solution</summary>

- **Public key:** (E, N) — shared with everyone. Used by others to encrypt messages TO you.
- **Private key:** D — kept secret by the owner. Used to decrypt messages received.

N and E are published; D is never shared.

</details>

---

### Problem 4.2 — Modular Arithmetic ⭐⭐
**Calculate:**
(a) 58 mod 5
(b) -16 mod 5
(c) 33 mod 7
(d) -33 mod 5

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) 58 mod 5:**
58 ÷ 5 = 11 remainder **3**
**58 mod 5 = 3**

**(b) -16 mod 5:**
-16 ÷ 5 = -3 remainder -1 (negative!)
Add modulus: -1 + 5 = 4
**-16 mod 5 = 4**

**(c) 33 mod 7:**
33 ÷ 7 = 4 remainder **5**
**33 mod 7 = 5**

**(d) -33 mod 5:**
-33 ÷ 5 = -6 remainder -3 (negative!)
Add modulus: -3 + 5 = 2
**-33 mod 5 = 2**

**🔑 For negative mod results:** Add the modulus until the result is positive.

</details>

---

### Problem 4.3 — GCD (Euclidean Algorithm) ⭐⭐
**Find gcd(27, 12) using the Euclidean Algorithm. Show all steps.**

<details>
<summary>🔓 Click to reveal solution</summary>

**Euclidean Algorithm:** gcd(a, b) = gcd(b, a mod b); gcd(a, 0) = a

```
gcd(27, 12)
= gcd(12, 27 mod 12)    [27 = 2×12 + 3]
= gcd(12, 3)
= gcd(3, 12 mod 3)      [12 = 4×3 + 0]
= gcd(3, 0)
= 3
```

**gcd(27, 12) = 3**

**Verification:** Divisors of 27: 1, 3, 9, 27. Divisors of 12: 1, 2, 3, 4, 6, 12. Common: 1, 3. Greatest: **3** ✓

</details>

---

### Problem 4.4 — RSA Key Generation ⭐⭐⭐
**Using RSA with P = 11 and Q = 3:**

(a) Calculate N
(b) Calculate (P-1)(Q-1)
(c) Choose a suitable E and explain why
(d) Calculate D

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) N = P × Q = 11 × 3 = 33**

**(b) (P-1)(Q-1) = 10 × 2 = 20**

**(c) Choose E:**
E must have **no common factor** with 20.
Factors of 20: 1, 2, 4, 5, 10, 20

Try E = 3: gcd(3, 20) = 1 ✓ (no common factors)

**E = 3** (public key component)

**(d) Calculate D:**
(D × E) mod (P-1)(Q-1) = 1
(D × 3) mod 20 = 1

Try values:
- D = 1: 3 mod 20 = 3 ✗
- D = 2: 6 mod 20 = 6 ✗
- D = 3: 9 mod 20 = 9 ✗
- ...
- D = 7: 21 mod 20 = 1 ✓

**D = 7** (private key)

**Verification:** 3 × 7 = 21 = 1 × 20 + 1 → 21 mod 20 = 1 ✓

</details>

---

### Problem 4.5 — RSA Encryption/Decryption ⭐⭐⭐
**Using RSA with P=11, Q=3, E=3, D=7 (from Problem 4.4):**

(a) What is the encoded value of the letter "F"? (A=1, B=2, ...)
(b) Encrypt "F" using the public key
(c) Decrypt the ciphertext using the private key

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) Encoding:**
F is the 6th letter → **PT = 6**

**(b) Encryption:**
CT = PTᴱ mod N = 6³ mod 33
6³ = 216
216 mod 33 = 216 ÷ 33 = 6 remainder **18**
**CT = 18**

**(c) Decryption:**
PT = CTᴰ mod N = 18⁷ mod 33

Let me compute step by step:
18¹ mod 33 = 18
18² mod 33 = 324 mod 33 = 324 - 9×33 = 324 - 297 = 27
18⁴ mod 33 = 27² mod 33 = 729 mod 33 = 729 - 22×33 = 729 - 726 = 3
18⁷ mod 33 = 18⁴ × 18² × 18¹ mod 33 = 3 × 27 × 18 mod 33
= 3 × 27 = 81 mod 33 = 81 - 2×33 = 15
= 15 × 18 = 270 mod 33 = 270 - 8×33 = 270 - 264 = 6

**PT = 6** → Letter "F" ✓

</details>

---

### Problem 4.6 — RSA Full Example ⭐⭐⭐⭐
**Given RSA with P = 7, Q = 17:**

(a) Find N, (P-1)(Q-1), and choose a suitable E
(b) Calculate D
(c) Encrypt the letter "K" (K = 11)
(d) Decrypt the ciphertext from (c)

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) Key generation:**
```
N = P × Q = 7 × 17 = 119
(P-1)(Q-1) = 6 × 16 = 96
```

Choose E: Must be coprime with 96.
Factors of 96: 1, 2, 3, 4, 6, 8, 12, 16, 24, 32, 48, 96

Try E = 5: gcd(5, 96) = 1 ✓

**E = 5** (public key)

**(b) Calculate D:**
(D × 5) mod 96 = 1

5D = 96y + 1
Try y = 4: D = (96×4 + 1)/5 = 385/5 = **77**

Verify: 5 × 77 = 385 = 4 × 96 + 1 → 385 mod 96 = 1 ✓

**D = 77** (private key)

**(c) Encrypt "K" (PT = 11):**
CT = 11⁵ mod 119
11² = 121 mod 119 = 2
11⁴ = 2² = 4
11⁵ = 11⁴ × 11 = 4 × 11 = 44

**CT = 44**

**(d) Decrypt (CT = 44):**
PT = 44⁷⁷ mod 119

This requires modular exponentiation:
44¹ mod 119 = 44
44² mod 119 = 1936 mod 119 = 1936 - 16×119 = 1936 - 1904 = 32
44⁴ mod 119 = 32² mod 119 = 1024 mod 119 = 1024 - 8×119 = 1024 - 952 = 72
44⁸ mod 119 = 72² mod 119 = 5184 mod 119 = 5184 - 43×119 = 5184 - 5117 = 67
44¹⁶ mod 119 = 67² mod 119 = 4489 mod 119 = 4489 - 37×119 = 4489 - 4403 = 86
44³² mod 119 = 86² mod 119 = 7396 mod 119 = 7396 - 62×119 = 7396 - 7378 = 18
44⁶⁴ mod 119 = 18² mod 119 = 324 mod 119 = 324 - 2×119 = 86

77 = 64 + 8 + 4 + 1
44⁷⁷ = 44⁶⁴ × 44⁸ × 44⁴ × 44¹ mod 119
= 86 × 67 × 72 × 44 mod 119

86 × 67 = 5762 mod 119 = 5762 - 48×119 = 5762 - 5712 = 50
50 × 72 = 3600 mod 119 = 3600 - 30×119 = 3600 - 3570 = 30
30 × 44 = 1320 mod 119 = 1320 - 11×119 = 1320 - 1309 = 11

**PT = 11** → Letter "K" ✓

</details>

---

### Problem 4.7 — RSA Which Key? ⭐⭐
**For each scenario, state which key is used for encryption and decryption:**

(a) A bank wants customers to send confidential account information
(b) A sender wants to sign a digital document (non-repudiation)
(c) A recipient wants to receive a confidential message from anyone

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) Confidentiality (Bank):**
- Customers encrypt with → **Bank's public key**
- Bank decrypts with → **Bank's private key**

**(b) Non-repudiation (Digital Signature):**
- Sender encrypts (signs) with → **Sender's private key**
- Anyone can verify/decrypt with → **Sender's public key**

**(c) Confidentiality (Recipient):**
- Senders encrypt with → **Recipient's public key**
- Recipient decrypts with → **Recipient's private key**

**Rule of thumb:**
- Confidentiality → encrypt with recipient's PUBLIC key
- Authentication/Non-repudiation → encrypt with sender's PRIVATE key

</details>

---

### Problem 4.8 — RSA Security ⭐
**Why is it difficult to crack RSA?**

<details>
<summary>🔓 Click to reveal solution</summary>

RSA's security relies on the **computational difficulty of factoring large numbers**:

1. It is **easy** to multiply two large primes: N = P × Q (takes microseconds)
2. It is **extremely difficult** to factor N back into P and Q (when N is 100+ digits, it would take years even with massive computing power)

To find the private key D, an attacker needs to:
- Know P and Q (to compute (P-1)(Q-1))
- But P and Q can only be found by factoring N
- Factoring a very large N is computationally infeasible with current technology

Given only E and N (the public key), finding D is practically impossible.

</details>

---

### Problem 4.9 — Digital Envelope ⭐⭐
**Explain why a digital envelope is used instead of pure asymmetric encryption. What does it contain?**

<details>
<summary>🔓 Click to reveal solution</summary>

**Why not pure asymmetric?**
- Asymmetric algorithms are **significantly slower** than symmetric algorithms
- Encrypting large messages (e.g., files, emails) with RSA alone would be impractical

**Solution — Digital Envelope:**
- Encrypt the **message** with a fast **symmetric key** (symmetric algorithm)
- Encrypt the **symmetric key** with the recipient's **public key** (asymmetric algorithm)
- Send both together

**What it contains:**
1. **Encrypted Symmetric Key** — the session key encrypted with recipient's public key
2. **Ciphertext** — the actual message encrypted with the symmetric key
3. **Symmetric Algorithm** — which symmetric algorithm was used
4. **Asymmetric Algorithm** — which asymmetric algorithm was used

This combines the **speed** of symmetric encryption with the **secure key exchange** of asymmetric encryption.

</details>

---

### Problem 4.10 — Symmetric vs Asymmetric Comparison ⭐⭐
**Complete the comparison table:**

| Characteristic | Symmetric | Asymmetric |
|----------------|-----------|------------|
| Keys used | | |
| Speed | | |
| Ciphertext size vs plaintext | | |
| Key exchange | | |
| Keys for n participants | | |
| Usage | | |

<details>
<summary>🔓 Click to reveal solution</summary>

| Characteristic | Symmetric | Asymmetric |
|----------------|-----------|------------|
| Keys used | **Same key** for encrypt & decrypt | **Different keys** (public + private) |
| Speed | **Very fast** | **Slower** |
| Ciphertext size vs plaintext | Usually **≤ plaintext** | **≥ plaintext** |
| Key exchange | **Big problem** (how to share?) | **No problem** (public key shared openly) |
| Keys for n participants | **n(n-1)/2** (doesn't scale) | **n pairs** (scales well) |
| Usage | Encryption/decryption only (confidentiality) | Encryption + **digital signature** (confidentiality + integrity + non-repudiation) |

</details>

---

### Problem 4.11 — Number of Keys Calculation ⭐⭐
**How many keys are needed for:**
(a) Symmetric encryption among 5 people?
(b) Asymmetric encryption among 5 people?

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) Symmetric:** n(n-1)/2 = 5 × 4 / 2 = **10 keys**

Each pair needs a unique shared key: AB, AC, AD, AE, BC, BD, BE, CD, CE, DE

**(b) Asymmetric:** Each person needs 1 key pair (public + private)
Total = n pairs = **5 key pairs** (10 keys total, but only 5 public + 5 private)

Each person publishes their public key and keeps their private key secret.

</details>

---

# ═══════════════════════════════════════════════
# 🔥 BONUS: Mixed / Tricky Exam-Style Questions
# ═══════════════════════════════════════════════

---

### Bonus 1 — Quick Fire 20 MCQ ⭐⭐
**Answer each in one word/number:**

1. How many rounds in DES? → **16**
2. DES block size? → **64 bits**
3. DES key size (effective)? → **56 bits**
4. Name of DES structure? → **Feistel**
5. AES replaced DES in what year? → **2002**
6. Blowfish was designed by? → **B. Schneier**
7. RC5 64-bit was cracked in how many days? → **1757 days**
8. Current min symmetric key size? → **256 bits**
9. Current min asymmetric key size? → **2048 bits**
10. Vernam cipher key is called? → **One-time pad**
11. Caesar cipher shifts by how many? → **3**
12. Mono-alphabet total permutations? → **26!**
13. DH is used for? → **Key exchange only** (not encryption)
14. CBC stands for? → **Cipher Block Chaining**
15. ECB weakness? → **Repeating patterns**
16. IV in CBC is how many bits? → **64 bits**
17. S-Box input/output sizes? → **48 input → 32 output**
18. RSA named after? → **Rivest, Shamir, Adleman**
19. RSA based on difficulty of? → **Factoring large numbers**
20. ECC advantage? → **Shorter keys, faster**

<details>
<summary>🔓 Click to reveal answers</summary>

1. **16**
2. **64 bits**
3. **56 bits**
4. **Feistel** Cipher Structure
5. **2002**
6. **B. Schneier**
7. **1757 days** (4.81 years)
8. **256 bits**
9. **2048 bits**
10. **One-time pad** (OTP)
11. **3**
12. **26!** ≈ 4.03 × 10²⁶
13. **Key exchange** only
14. **Cipher Block Chaining**
15. **Repeating plaintext blocks produce repeating ciphertext**
16. **64 bits**
17. **48 input → 32 output**
18. **Rivest, Shamir, Adleman**
19. **Factoring the product of two large prime numbers**
20. **Higher cryptographic strength with shorter keys, faster, suitable for mobile devices**

</details>

---

### Bonus 2 — Scenario Questions ⭐⭐⭐
**For each scenario, identify: (1) the security principle involved, (2) the attack type, (3) the countermeasure.**

**(a)** An employee intercepts an email containing trade secrets and reads it.

**(b)** A hacker changes the bank account number in a payment instruction.

**(c)** A fake website pretends to be a bank's website to collect login credentials.

**(d)** A server is flooded with requests and becomes unavailable.

**(e)** A customer sends a wire transfer then claims they never authorized it.

<details>
<summary>🔓 Click to reveal solution</summary>

| Scenario | Principle | Attack Type | Countermeasure |
|----------|-----------|-------------|----------------|
| (a) | **Confidentiality** | **Interception** (passive) | Encryption |
| (b) | **Integrity** | **Modification** (active) | Digital signatures, hashing |
| (c) | **Authentication** | **Fabrication/Masquerade** (active) | Digital certificates, mutual authentication |
| (d) | **Availability** | **Interruption/DoS** (active) | Redundancy, increased bandwidth, firewalls |
| (e) | **Non-Repudiation** | **Repudiation** | Digital signatures |

</details>

---

### Bonus 3 — Complete RSA Walkthrough ⭐⭐⭐⭐
**Given P = 5, Q = 13:**

(a) Compute N, φ = (P-1)(Q-1)
(b) Choose E (must be coprime with φ)
(c) Compute D
(d) Encrypt the letter "N" (encoded as 14)
(e) Decrypt the result

<details>
<summary>🔓 Click to reveal solution</summary>

**(a) Key generation:**
```
N = 5 × 13 = 65
φ = (5-1)(13-1) = 4 × 12 = 48
```

**(b) Choose E:**
Factors of 48: 1, 2, 3, 4, 6, 8, 12, 16, 24, 48
Try E = 5: gcd(5, 48) = 1 ✓

**E = 5**

**(c) Compute D:**
(D × 5) mod 48 = 1

Try D = 29: 29 × 5 = 145 = 3 × 48 + 1 → 145 mod 48 = 1 ✓

**D = 29**

**(d) Encrypt "N" (PT = 14):**
CT = 14⁵ mod 65
14² = 196 mod 65 = 196 - 3×65 = 196 - 195 = 1
14⁴ = 1² = 1
14⁵ = 1 × 14 = 14 mod 65 = 14

**CT = 14**

**(e) Decrypt:**
PT = 14²⁹ mod 65

Using repeated squaring:
14¹ mod 65 = 14
14² mod 65 = 1
14⁴ mod 65 = 1² = 1
14⁸ mod 65 = 1
14¹⁶ mod 65 = 1

29 = 16 + 8 + 4 + 1
14²⁹ = 14¹⁶ × 14⁸ × 14⁴ × 14¹ = 1 × 1 × 1 × 14 = 14

**PT = 14** → Letter "N" ✓

</details>

---

*Use this file alongside the Study Guide. Practice doing each problem yourself before clicking to reveal the answer. The more you practice, the faster you'll be on test day!*
