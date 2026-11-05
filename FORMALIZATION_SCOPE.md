# Bounded Lean 4 terminal arithmetic

**This is not a formal verification of the main enumeration or of the global nonexistence claim at length 106.** It is an AI-authored internal formalization. No human authorship, review, certification, or public upload is asserted.

## Verification status

**Compiled successfully on 2026-11-05** with Lean 4.9.0, commit `8f9843a4a5fe`, official arm64 macOS release. `verify.sh` completed with exit status zero; `verification.log` records the version, dependency audit, and final `VERIFICATION COMPLETE` marker. The theorem statements in these modules were accepted by Lean's kernel. This statement is confined to those statements, not the external enumeration. No mathlib or external Lean package is needed. Only the installed Lean core module `Lean.Elab.Tactic.Omega` and its core dependencies are imported. Lean 4.9.0 does not bundle the later `Std` umbrella package.

## Theorems and their exact scope

`TerminalArithmetic.lean` proves:

- An integer equal to 16 or -16 is not divisible by 32. This includes 16*s and -16*s when the supplied sign satisfies s=1 or s=-1.
- -160 is not divisible by 64; its Euclidean remainder modulo 64 is 32.
- If `(r24-r28) % 32 = 16`, then r24 and r28 cannot both be divisible by 32.
- Divisibility by 64 implies divisibility by 32. An exactly zero residual implies divisibility by every integer modulus, and in particular remainder zero modulo 64.
- `ValidLag k` means precisely 1 <= k <= 105. `ExactResidual r` means r(k)=0 at these lags only. It does not incorrectly constrain lag zero.
- `TerminalObstruction r` is the disjunction of a valid lag with residual +/-16, a valid lag with residual -160, or the stated difference congruence at lags 24 and 28. A **supplied** such obstruction contradicts both divisibility by 64 at all valid lags and exact residual zero.
- The integer/natural-number identities
  `4*2^4 + 2*2^20 + 2*2^26 = 136314944`,
  `8*(4*2^4 + 2*2^20 + 2*2^26) = 1090519552`,
  `8*8 = 64`, `8*2^156 = 2^159`, and
  `8*(102*2^52) = 102*2^55`.
  These are **numeric identities only**, not cardinality theorems and not proofs that normalization has multiplier eight.

### Conditional interfaces: all assumptions are explicit

`conditional_no_exact_residual` takes the following data and hypothesis:

1. `Candidate : Type`, an arbitrary candidate type;
2. `admissible : Candidate -> Prop`, an arbitrary admissibility predicate;
3. `residual : Candidate -> (Nat -> Int)`, an arbitrary supplied residual map;
4. `exhaustive_terminal_reduction : forall c, admissible c -> TerminalObstruction (residual c)`.

Its conclusion is that no admissible candidate has `ExactResidual`. No actual Golay candidate type, coverage proof, or exhaustive terminal reduction is supplied.

`conditional_no_target` additionally takes an arbitrary predicate `isTarget` and both hypotheses:

- `target_coverage : forall c, isTarget c -> admissible c`;
- `target_residual_soundness : forall c, isTarget c -> ExactResidual (residual c)`.

It concludes that no `isTarget` candidate exists **conditional on all those hypotheses**. It is not an unconditional theorem about binary Golay pairs.

## Eight finite literal-pair checks

`WitnessChecks.lean` copies the eight A,B arrays from
`research_bundle/golay_research/results/algebra_mod32_witnesses.json`, in source row order. It defines direct integer aperiodic correlation by summing products over the non-wrapping overlap. For **each of these eight literal pairs**, it checks in Lean:

- both lists have length 106;
- every list entry satisfies the Boolean test `x == 1 || x == -1`;
- the directly computed combined residual at lag 4 is -160;
- therefore that particular residual vector is not exact.

`FullWitness0.lean` additionally proves `witness0_all_positive_lags_mod32`: for every `k : Fin 105`, the directly computed residual `combined witness0 (k.val + 1)` has remainder zero modulo 32. This covers exactly lags 1 through 105, using ordinary `decide`. `explicit_mod32_witness_exists` packages this with the length and binary-alphabet checks to prove existence of one binary length-106 modulo-32 witness.

For the other seven literal pairs, the other 104 residuals and all-lag divisibility by 32 are **not** formally checked here. Even for witness0, no full list of exact residual values or energy 56320 is proved. Orbit membership, generation from masks, the JSON parser, and completeness of the eight rows are also not formally verified. The JSON-to-Lean transcription is a generation step outside Lean. The kernel checks the explicit Lean literals, not a claim that they exhaust any search. Row comments and source digests are provenance data, not proof terms.

## Not proved

The full orientation enumeration, its domain coverage, parity/mirror and normalization reductions, all affine-space dimensions/ranks/completeness, reconstruction from q/t/sign masks, character-polynomial identities, linkage of actual source residuals to terminal cases, the factor-eight orbit argument, exact pair counts, the complete modulus-32 classification, the global modulus-64 obstruction, and nonexistence of length-106 binary Golay pairs remain outside this formalization. Existing executable checkers and mathematical documents are not converted into formally verified proofs by these files.

## Reproduce locally

From any directory, without a package manager or a global installation:

```sh
bash verify.sh /absolute/path/to/lean-4.9.0/bin/lean
```

Or supply another compatible local binary explicitly. The script writes `.olean` files and `verification.log` only beside these sources. It uses ordinary `decide` for finite computations and `omega` for elementary integer arithmetic. It does not use `native_decide`, admit incomplete proofs, or declare extra axioms. `Audit.lean` prints the actual axiom dependencies of principal results. The integer obstruction and conditional results use Lean's foundational `propext` and, for `omega`-based results, `Quot.sound`. No extra axioms are declared. The finite numeric identities, the -160 remainder computation, all eight direct lag-four computations, and both witness0 all-positive-lag modulo-32/existence results have empty axiom dependency lists. Thus "no extra axioms" must not be misreported as "no foundational axiom dependencies".

There are **54 theorem declarations**: 20 terminal/arithmetic, 32 finite literal-pair checks, and two all-positive-lag modulo-32/existence results for witness0.

Files: `TerminalArithmetic.lean`, `WitnessChecks.lean`, `FullWitness0.lean`, `Audit.lean`, `verify.sh`, this README, `metadata.json`, and `LICENSE.md`; successful execution additionally creates the compiled `.olean` files and `verification.log`. Temporary diagnostic logs may also be present.

## License and provenance

License selected by the user: **Creative Commons Attribution 4.0 International (CC BY 4.0)**, SPDX `CC-BY-4.0`. See `LICENSE.md` and `metadata.json`. Date: 2026-11-05. This is internal AI-authored work; there is no claim of human review. Licensing does not constitute public submission or publication.
