# 📝 Marked: Mock Test Attempt 1

## Score: **27 / 30 (90%)** — comfortably in the A band. Great attempt.

| Section | Marks | Your score |
|---|---|---|
| A — MCQ (8×1) | 8 | **8** ✅ |
| B1 — Multi-select (3×2) | 6 | **5** |
| B2 — Fill-in-blanks (6×1) | 6 | **5** |
| B3 — Open-ended (4+3+3) | 10 | **9** |
| **Total** | **30** | **27** |

---

## Section A — MCQ (8/8) ✅
All correct: A1 D. message digest · A2 C. collision · A3 B. MD5 · A4 B. sender's private key · A5 C. confidentiality · A6 D. SHA-512 · A7 A. public key · A8 A. its own private key. Perfect — no traps caught you.

## Section B1 — Multi-select (5/6)
- **B1 (1/2)** — you picked A, B, C, E, F; correct was **A, B, C, F**. E was **"Reversible"** — the trap. A hash is *irreversible*; "reversible" is the exact opposite. (D "variable-length output" was also a trap — hashes give *fixed*-length output.)
- B2 (2/2) ✅ · B3 (2/2) ✅ — including correctly *not* selecting "Signing and issuing digital certificates" for the RA. Nice.

## Section B2 — Fill-in-blanks (5/6)
- C1 128 ✅ · C2 32 ✅ · C4 public ✅ · C5 ECDSA ✅ · C6 CRL ✅
- **C3 (0/1)** — you wrote **"PAD"**; expected **"ipad"**. The answer needs the exact HMAC term: *Si = K′ XOR **ipad*** (and its partner *So = K′ XOR **opad***). "Padding" is the concept, but the blank asks for the specific operand — worth memorising since this exact formula is a favourite.

## Section B3 — Open-ended (9/10)

**D1 (4/4)** ✅ Excellent.
- (a) digest = 2 with full working — exactly right
- (b) Complete HMAC flow; bonus points for explicitly including the key-generation/sharing step (1) and ending with the comparison (5)
- (c) Correct and precise: attacker lacks the symmetric key, so cannot forge a valid MAC

**D2 (2.5/3)**
- (a) 2/2 — flawless 10-step flow, every key named correctly, comparison included. This is the exact "apply" answer the marker wants.
- (b) **0.5/1** — you gave only the *compatibility* reason. The standard answer wants **two of the three**: efficiency (signature much shorter; hashing faster than signing), compatibility, integrity (minute change → large hash change). One reason caps you at half.

**D3 (2.5/3)**
- (a) 2/2 — all four steps, plus a POP example (dummy certificate) — very strong.
- (b) **0.5/1** — right keys (sign with CA's private key, verify with CA's public key), but the mechanism is incomplete: the CA signs the **digest of the certificate fields**, and the user verifies by **hashing the fields (excluding the signature) → MD1**, decrypting the signature → **MD2**, and comparing **MD1 = MD2**. Saying "the certificate can be decrypted with the CA's public key" is imprecise — it's the *signature* that's decrypted. Markers look for that digest-comparison ending.

---

## What to fix before the real test
1. **Memorise ipad/opad** — the exact HMAC formula terms (C3)
2. **"Why sign the digest?" = 3 reasons** — always write efficiency + compatibility + integrity (D2b)
3. **Certificate verification ends with MD1 = MD2** — hash fields, decrypt signature, compare (D3b)
4. Multi-select strategy is working — you only dropped one mark on a polarity trap ("reversible")

Your open-ended technique is in great shape — numbered steps, keys named, comparisons included. The lost marks are all small recall items, not understanding. Want me to generate a fresh variant (different seed) so you can test again under the 50-minute clock?