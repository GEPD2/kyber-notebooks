# CRYSTALS-Kyber Mathematical Walkthrough Notebooks
## Post-Quantum Key Encapsulation Mechanism | ML-KEM / FIPS 203

Step-by-step Jupyter notebooks for learning the complete mathematics of
**CRYSTALS-Kyber (ML-KEM, FIPS 203)** using small pedagogical parameters
(**q = 17, n = 8, k = 2**), where every arithmetic operation can be verified by hand.

These notebooks accompany the paper:

> **A Case Study on CRYSTALS-Kyber: Bridging Theory and Practice in Post-Quantum
> Key Encapsulation Pedagogy** — Georgios Efthymiou, Ionian University, 2026.

## What's Inside

The notebooks walk through nine modules (0–8) in order:

- **Module 0 — Global Setup.** Sets the pedagogical parameters (`Q=17, N=8, K=2, ETA=2`)
  and the precomputed reference values. Run this cell first, since every other cell
  depends on these shared constants.
- **Module 1 — Mathematical Foundations.** The ring `R_q = Z₁₇[X] / (X⁸ + 1)`,
  polynomial addition and multiplication mod q, and the primitive roots of unity
  that power the NTT.
- **Module 2 — CBD Sampling.** Why Kyber needs small coefficients, and how the
  Centered Binomial Distribution turns random bits (the PRF output — `SHAKE-256`
  in FIPS 203) into the secret vector s and the error vector e.
- **Module 3 — Forward NTT (Cooley–Tukey).** Why naive polynomial multiplication
  is O(n²) and how the Number Theoretic Transform reduces it to O(n log n), with
  the full butterfly trace and intermediate values at every step.
- **Module 4 — Inverse NTT.** The same butterfly structure run in reverse, with the
  inverse twiddle factors and the final `n⁻¹ mod q` scaling step.
- **Module 5 — Public Key: t̂ = Â·ŝ + ê.** Why all computation stays in the NTT
  domain, how the public matrix Â is derived deterministically from a public seed ρ
  (expanded with `SHAKE-128`, the XOF, in FIPS 203), and why knowing (Â, t̂) does
  not reveal s.
- **Module 6 — Encapsulation.** How the sender uses the public key to encode a
  message bit with the `⌊q/2⌋` scaling trick, producing the ciphertext (u, v).
- **Module 7 — Decapsulation.** How the receiver uses the secret key to recover the
  message, and why the noise bound `‖e‖∞ ≪ q/4` is the condition that guarantees
  correct decryption.
- **Module 8 — Full System Test.** The complete KeyGen → Encapsulate → Decapsulate
  pipeline assembled in a single cell, verifying that the recovered message matches
  the original.

## Quickstart

```bash
git clone https://github.com/GEPD2/kyber-notebooks.git
cd kyber-notebooks
pip install jupyter
jupyter notebook
```

Open **`kyber_student.ipynb`** to work through the exercises, or
**`kyber_solution.ipynb`** to see the complete solutions. Greek-language versions
are also provided: **`kyber_student_gr.ipynb`** and **`kyber_solution_gr.ipynb`**.

No external cryptography libraries are required. Everything (modular arithmetic,
CBD sampling, the forward/inverse NTT, and the full KEM) is implemented from
scratch in pure Python, using only the standard-library `math` module.

## Parameters

| Parameter     | Pedagogical | FIPS 203 (ML-KEM-768) |
|---------------|:-----------:|:---------------------:|
| q (modulus)   | 17          | 3329                  |
| n (degree)    | 8           | 256                   |
| k (rank)      | 2           | 3                     |
| η (noise)     | 2           | 2                     |
| Verification  | By hand     | Computational         |

The pedagogical parameters are chosen so that every intermediate value fits on a
single line and can be checked with a calculator. The algorithms are structurally
identical to the FIPS 203 production parameters; only the magnitudes differ.

## Related

- **[kyber-platform](https://github.com/GEPD2/kyber-platform)** — interactive web
  platform with six difficulty levels, from modular arithmetic to a raw C KEM
  implementation.
- **[KYber_LWE](https://github.com/GEPD2/KYber_LWE)** — C implementation from
  scratch: Keccak, SHAKE, the NTT, and the full ML-KEM for all three security levels.
- **[FIPS 203](https://doi.org/10.6028/NIST.FIPS.203)** — the official NIST standard.
