# SAIR Proof Press: retain a checkable answer through bounded search

[Public repository](https://github.com/Chih-Kai-Wang/sair-stage2-proof-press) · [Interactive site](https://chih-kai-wang.github.io/sair-stage2-proof-press/) · [English paper](https://chih-kai-wang.github.io/sair-stage2-proof-press/paper/sair_stage2_solver_research.pdf)

This public companion repository documents solvers for equational implication,
which asks whether one magma identity implies another. A "true" answer must come
with a Lean proof that replays, and a "false" answer must come with a finite
countermodel that Lean can check.

## Problem and engineering approach

Candidate search can produce answers that look right and then fail when Lean
replays them. A Marathon solver has a second problem. It shares one time budget
across many inputs, so it has to keep its best verified answers as that budget
runs out.

The solver tries several bounded routes, including short proofs, finite
countermodels, proof-producing paramodulation and symbolic search. These routes
only propose candidates, and Lean decides whether each certificate is accepted.
The Marathon path does cheap deterministic work first. It keeps every verified
answer and never replaces one with a worse candidate. The aggressive variant also
has a bounded waypoint fallback.

## Published evidence

| Public workload | Recorded result |
|---|---|
| Released Normal/Hard inputs | All four frozen Solo/Marathon × Safe/Aggressive artifacts accepted 1,669 / 1,669 inputs; no actual model calls in the final runs |
| Released Order-5 | Marathon Safe 198 / 200; Aggressive 200 / 200 |
| Same-host released Marathon batch | Safe 169.00 s; Aggressive 152.23 s |

The records tie these results to evaluator commit
`817a4653bf762584931d49c6714c9fcfab7df66a` and Lean 4.33.1. The batch timing
describes this one workload. It is not a causal estimate of improvement on the
private set. On September 5, 2026, the byte sizes and SHA-256 hashes of the four
public solver files were read back and matched the published manifest. That
portfolio maintenance check did not rerun the full competition evaluation.

Sources: [aggregate results](https://github.com/Chih-Kai-Wang/sair-stage2-proof-press/blob/main/docs/results.md),
[machine-readable evidence](https://github.com/Chih-Kai-Wang/sair-stage2-proof-press/tree/main/docs/evidence),
[frozen solver files](https://github.com/Chih-Kai-Wang/sair-stage2-proof-press/tree/main/dist/final).

## What this demonstrates

The work connects search, certificate replay, budget management, file identity
and cautious reporting. Negative results stay in the public research timeline,
so anyone can still read how a failed experiment went.

The records show coverage of the released inputs. They do not include a private
score or rank published by the organizers. The portal's participation readback
records that a submission was delivered, not that it scored well. The full
private research history is not part of this public companion. The
[claim boundaries](https://github.com/Chih-Kai-Wang/sair-stage2-proof-press/blob/main/docs/claim-boundaries.md)
document lists what these records do and do not support.
