**CRYSTALS-Kyber Mathematical Walkthrough Notebooks**
## Post-Quantum Key Encapsulation Mechanism | ML-KEM / FIPS 203
Step by step Jupyter notebooks for learning the complete mathematics of
**CRYSTALS-Kyber (ML-KEM, FIPS 203) using small pedagogical parameters
(q=17, n=8, k=2) where every arithmetic operation can be verified by hand.**
These notebooks accompany the paper:

**A Case Study on CRYSTALS-Kyber: Bridging Theory and Practice in Post-Quantum Key Encapsulation Pedagogy
Georgios Efthymiou Ionian University, 2026**

What's Inside
The notebooks walk through eight modules in order:
Module 0 which is the Global Setup
Sets the pedagogical parameters (Q=17, N=8, K=2, ETA=2). Run this cell first because every other cell depends on it. Do not modify these values; they are the verified ground truth for all exercises.
Module 1 is the Mathematical Foundations
The ring R_q = Z₁₇[X] / (X⁸ + 1), polynomial addition and multiplication mod q, and the primitive roots of unity that power the NTT.
Module 2: CBD Sampling
Why Kyber needs small coefficients, and how the Centered Binomial Distribution generates the secret vector s and error vector e from random bits.
Module 3: Forward NTT (Cooley-Tukey)
Why naive polynomial multiplication is O(n²) and how the Number Theoretic Transform reduces it to O(n log n). Full butterfly diagram with intermediate values at every step.
Module 4: Inverse NTT
The same butterfly structure run in reverse, with inverted twiddle factors and the final n⁻¹ mod q scaling step.
Module 5: Key Generation: t̂ = Â·ŝ + ê
Why all computation stays in the NTT domain, how SHAKE-256 generates the public matrix Â deterministically from a seed, and why knowing (Â, t̂) does not reveal s.
Module 6: Encapsulation
How the sender uses the public key to encrypt a message bit-by-bit using the ⌊q/2⌋ scaling trick, producing ciphertext (u, v).
Module 7: Decapsulation
How the receiver uses the secret key to recover the message, and why the noise bound ‖e‖∞ ≪ q/4 is the mathematical condition that makes correct decryption guaranteed.
Module 8: Full System Test
The complete KeyGen → Encapsulate → Decapsulate pipeline assembled in a single cell, with verification that the recovered message matches the original.

Quickstart
```bash
bashgit clone https://github.com/GEPD2/kyber-notebooks.git
cd kyber-notebooks
pip install numpy sympy jupyter
jupyter notebook
```
Open kyber_student.ipynb to work through the exercises, or kyber_solution.ipynb to see the complete solutions.
No external cryptography libraries required. Everything is implemented from scratch using only NumPy and SymPy.

## Parameters
ParameterPedagogicalFIPS 203 (ML-KEM-768)q (modulus)173329n (degree)8256k (rank)23η (noise)22VerificationBy handComputational
The pedagogical parameters are chosen so that every intermediate value fits on a single line and can be checked with a calculator. The algorithms are structurally identical to FIPS 203 production parameters.

## Related

kyber-platform with Interactive web platform with six difficulty levels, from modular arithmetic to raw C KEM implementation
KYber_LWE C implementation from scratch: Keccak, SHAKE, NTT, full ML-KEM for all three security levels
FIPS 203 Official NIST standard


License
MIT
