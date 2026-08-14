# Zero-Knowledge from Secure MPC & Ligero

A self-contained technical study of two landmark zero-knowledge proof systems
built on the MPC-in-the-Head paradigm.

## Papers

- **[IKOS07]** Ishai, Kushilevitz, Ostrovsky, Sahai — *Zero-Knowledge from Secure
  Multiparty Computation*, STOC 2007 / SIAM J. Computing
- **[AHIV22]** Ames, Hazay, Ishai, Venkitasubramaniam — *Ligero: Lightweight
  Sublinear Arguments Without a Trusted Setup*, CCS 2017 / ePrint 2022/1608

## What's covered

**IKOS07 — MPC-in-the-Head**
- The core construction: prover XOR-secret-shares the witness among n virtual
  players, simulates the MPC internally, commits to all views, and opens only
  the challenged pair
- Security proofs: pairwise-consistency lemma (local ↔ global), soundness via
  the inconsistency graph + König's theorem, ZK via the MPC privacy simulator
- Variants: coin-flipping preamble Π′ᴿ for statistical correctness; robust
  variant Πᴿ,ₜ using t-robust MPC for single-round soundness amplification
- Efficiency: O(s) + poly(k, log s) communication — the first constant-rate ZK
  proof for all of NP under one-way functions

**Ligero — Sublinear ZK Arguments**
- Interleaved Reed–Solomon encoding of the witness into a √s × √s matrix;
  column commitments via a collision-resistant hash (no trusted setup)
- Linear test (random row combination) + quadratic gate-constraint test via
  Schwartz–Zippel; verifier queries only O(√s) columns
- Communication O(√s · λ) bits — concretely ≈ 35 KB for SHA-256 preimage
  at 2⁻⁴⁰ soundness, vs. ≈ 289 KB for ZKBoo and ≈ 202 KB for ZKB++
- Made non-interactive via Fiat–Shamir in the random oracle model

**Comparison & impact**

| System | Communication | Assumption | Trusted setup |
|--------|--------------|------------|---------------|
| GMW classical | O(k · s) | OWFs | None |
| IKOS07 | O(s) + poly(k, log s) | OWFs | None |
| Ligero | O(√s · λ) | CRHFs | None |
| ZK arguments (Kilian) | poly(k) · polylog(s) | CRHFs | Yes (PCP) |

Downstream impact: ZKBoo → ZKB++ → **Picnic** (NIST PQC Round 3 finalist);
Ligero++ (R1CS support); Aurora (O(log²s) via FRI); STARKs.

## Contents
report/ 18-page technical report (definitions, protocols, proofs, open problems)
slides/ 16-slide seminar presentation


## Open problems discussed

- Constant-rate ZK with O(1) rounds under OWFs
- Ω(s) lower bound for statistical ZK proofs
- Sublinear-prover transparent ZK (o(s) prover time)
- VOLE-in-the-head and public verifiability
