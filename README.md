# Golay length106: reproducibility materials

Reproducibility code, execution evidence, exact certificates and limited Lean formalization for **A computer-assisted nonexistence proof for binary Golay pairs of length106**, prepared by **SUNGBIN HONG**.

This is a computer-assisted finite result with an explicit computational trust boundary. No human checking/understanding, human expert peer review, publication priority, or proof of the general Golay length conjecture is claimed. The manuscript has not yet been deposited on Hexagon at the time of this initial archive version.

## Files

- [native-reproduction.zip](native-reproduction.zip): complete accepted-result native sources and historical campaigns,102orientation output, sign-space descriptors, exact integer certificates, literal modulo32 witnesses, reproduction instructions, and separately documented corrected Mac replay. It contains its own public integrity manifest.
- [partial-lean-formalization.zip](partial-lean-formalization.zip): Lean4.9.0 sources, verifier, scope documentation and axiom audit. **Not a formal proof of the main enumeration or global nonexistence theorem.**
- [VALIDATION.json](VALIDATION.json): exact archive hashes and validation scopes.
- [PORTABILITY_FINDING.md](PORTABILITY_FINDING.md): a rejected replay, the overload defect, correction and regression checks.
- [FORMALIZATION_SCOPE.md](FORMALIZATION_SCOPE.md): exactly what Lean proves and does not prove.
- [LICENSE.md](LICENSE.md): CC BY4.0, to the extent applicable rights are held.

The archives are the distributable source/data packages, not just executable binaries. Download and unpack them; reviewed source and reproducibility commands are included. Prefer rebuilding source over executing supplied historical snapshots.

## Mathematical target

For A,B in {−1,+1}^106, define the original positive-lag **aperiodic** residual

`r_k = sum(i=0..105-k) (a_i*a_(i+k)+b_i*b_(i+k)), 1<=k<=105`.

The computer-assisted result excludes every pair for which all r_k are divisible by64, hence excludes ordinary binary aperiodic Golay pairs of length106. The weaker modulo32 system has exactly8normalized pairs,64raw ordered pairs in one standard symmetry orbit. This does not address periodic/complex pairs, other untested lengths, or a global energy optimum.

## Main validation

Two structurally different historical implementations covered all67,108,864folded H values and returned the same102orientations. Independent original-correlation reconstruction verified94inconsistent sign systems and8complete affine spaces. Compact integer-character certificates exclude all8spaces modulo64 and reconstruct the modulo32 witnesses. A fresh direct sign replay checked all136,314,944remaining assignments with original integer products.

A later **corrected** Apple-Clang/AArch64 primary replay covered all67,108,864indices with exactly1nonunit and exactly the same102-output set. Its strict coverage, source/binary, original parity and exact-set audit passed. That is a primary-implementation replay on different hardware, not a third unrelated solver or a theorem-kernel proof.

## Important portability correction

The unmodified legacy primary source can select a libc++ floating mathematical `remainder(U,U)` overload instead of its polynomial helper. A negative double converted to unsigned128 is undefined behavior. The first Mac replay's42outputs/extra nonunits were **rejected and preserved**, not treated as exclusions.

For libc++/macOS use the separately corrected `poly_remainder` sources in the archive's `preparation-validation/portable_source/`. The optional guarded AArch64 PMULL product was compared with exact software carryless multiplication on1,000,000full-width operand pairs. The subsequent corrected full replay passed. Original historical Linux/GCC evidence was not overwritten.

## Limited formalization

Lean4.9.0 accepts54theorem declarations: terminal arithmetic, explicitly conditional exclusion interfaces, numeric identities, eight literal pairs' binary entries/lengths/lag4, and all105positive-lag modulo32conditions plus existence for **one** explicit pair. The global enumeration, completeness, classification and nonexistence theorem remain outside this formalization. Ordinary `decide` is used, not `native_decide`; foundational dependencies are audited and no extra axioms or unfinished proofs are introduced.

## Provenance and privacy

The sole human contributor selected the problem and directed the research. Research/text were primarily AI-generated. Author-reported tools: ChatGPT (Chat), GPT-6 Pro, research; Gemini3.1 Pro, internal review; ChatGPT (Aside), GPT-6.1 Sol Max, internal review and preparation. AI reviews are not human peer review. Private prompts, conversation exports, private handoff instructions, and third-party paper PDFs are intentionally excluded.

## Prior methods

Quad/successive congruence reductions and standard Golay symmetries are established methods: P.B.Borwein and R.A.Ferguson, *A complete description of Golay pairs for lengths up to100*, Mathematics of Computation73(2004),967–985, https://doi.org/10.1090/S0025-5718-03-01576-X.

The general linear-consequence/substitution principle is ElimLin-style: N.T.Courtois, P.Sepehrdad, P.Sušil and S.Vaudenay, *ElimLin Algorithm Revisited*, FSE2012, LNCS7549,306–325, https://doi.org/10.1007/978-3-642-34047-5_18. No claim is made to invent these established methods.
