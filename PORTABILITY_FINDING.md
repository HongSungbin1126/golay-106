# Rejected libc++ replay and exact correction

Date:2026-11-05. No original source, historical campaign or manifest was overwritten.

## Observed failure

A fresh Apple Clang21/libc++ arm64 build of frozen primary source SHA256 `3154f3816e12d8476df26a8e736fe26cbbd520e74238f842e853b9bfc379163f` traversed all67,108,864 H indices, but reported33,554,433 nonunits and only42 orientation outputs instead of the mathematically required one nonunit and archived102 outputs. That run is **rejected** and retained in `fresh_primary_rejected_libcpp/`. It is not evidence for nonexistence.

## Root cause, not a theorem counterexample

The file declares `static U remainder(W a,U f)` for polynomial reduction, where W is unsigned128 and U unsigned64. At original line69, `remainder(a,f)` has arguments U,U. Under this libc++ environment a globally exposed arithmetic-template mathematical `remainder(U,U)` is a better overload than the intended W,U helper. Its return type is double.

Minimal p13,h1: H=4097,J=8191. Unqualified U,U mathematical remainder is -4094; explicitly selecting polynomial remainder with W(H),J yields4094. Converting the negative floating value to unsigned128 is out of representable range and undefined behavior. UBSAN reports that conversion, and AST/type diagnostics independently identify the selected double overload. Both O0 and O3 reproduce the defect. This is an identifier/overload portability defect, not an optimization-only compiler defect or a counterexample to irreducibility.

The independent multiplication-matrix inverse gives2731 for this case; an explicit-cast corrected Euclid inverse agrees. Full p13 inversion has63units,1nonunit and no matrix mismatch. First128p53 cases have127units,1nonunit and no mismatch. The broken build rejects odd H because their numerical values exceed half the floating divisor.

## Corrections and validation

`portable_source/exact_orientation_fibers_portable.cpp` changes only the five identifier tokens `remainder` to `poly_remainder`; SHA256 `ab05bda65f61d741c69bab3e8be917c82d25704acdcfb093475474bb5665f66b`.

`portable_source/exact_orientation_fibers_arm.cpp` additionally uses guarded AArch64 PMULL for the same carryless polynomial product; SHA256 `bd567766ec3848c9da55d41e97f5c41766659fc0874f37ef447713b53a455b2d`. Its products matched the exact software shift/XOR routine on1,000,000 deterministic full64-bit operand pairs. This is an implementation test, not a formal proof of the intrinsic.

Both corrected builds give18 first-parity orientations and exactly1nonunit on the full n26 domain, and19 orientations with1nonunit on the first65,536 n106 H values. Earlier tiny rename-only diagnostic reports containing the temporary source label60a8 are regression diagnostics, NOT accepted provenance-pinned campaign evidence.

A new full corrected execution is kept separately in `fresh_primary_corrected/`. Its actual complete/failure status must be read from the strict final audit, not inferred from this note. The frozen Linux/GCC campaigns and their exact hashes are retained as historical evidence; the portable fix does not rewrite them. The secondary implementation uses separately named matrix inversion and is not assumed to share this particular overload defect.

The paper must disclose this portability defect and use the corrected source for libc++/macOS reproduction. No corrected full result is accepted until every interval, unit count, literal output and exact102-candidate set has passed the strict auditor.
