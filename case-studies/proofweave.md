# ProofWeave: certify a formal target without overstating its meaning

[Repository](https://github.com/Chih-Kai-Wang/proofweave-math-lab) · [Actual run and artifacts](https://github.com/Chih-Kai-Wang/proofweave-math-lab/tree/main/docs/walkthroughs/simple-ring)

ProofWeave Core is experimental Python infrastructure for structured
mathematical claims. It writes Lean certification artifacts that a reader can
open and check, and it tracks proof status, semantic alignment and claim
lifecycle separately.

## Problem and observable result

A formal proof can be correct and still prove a different statement from the
one a person meant. A single "verified" label hides that difference.

On September 5, 2026, the bundled integer identity `(x + 1)² = x² + 2x + 1` was
run with pinned Lean/Mathlib 4.32.2 on macOS arm64. Lean certified its one
deductive obligation. The overall result stayed **CERTIFIED + UNCONFIRMED**,
because no person had attested that the Lean target matches the prose. The
first run called the certifier once and called no model. A second, unchanged run
checked and reused the same artifacts with zero certifier calls.

The walkthrough keeps the exact input, the generated Lean source, the
certificate, the coverage file and SHA-256 checksums. Its JSON summary copies
selected fields from the real CLI output and removes absolute host paths.

## Engineering decisions

- **Keep the certificate language small.** Author-supplied targets and allowed
  tactics can be read directly. Obligations the system cannot
  handle stay marked as partial.
- **Tie results to exact bytes and the formal environment.** The input, the
  statement, the certificate and the toolchain each have an identity, so a
  cached result can be checked before it is reused.
- **Keep the status axes independent.** A valid formal proof can never turn
  silently into an alignment attestation or an active claim revision.
- **Test refusals as well as successes.** The released finite corpus includes
  paired negative cases and escape attempts. If the toolchain is missing, the
  run must fail instead of reporting success.

## Scope

This walkthrough records one real run. The separate `v0.1.0` evidence release
reports 42 fixed-corpus cases, and the Core package and protocol version is
2.0.0. Neither result establishes global soundness, formalization of arbitrary
natural language, novelty or peer review. A useful next evaluation would be a
preregistered set of new claims, written by other people, with reviewed formal
alignments.
