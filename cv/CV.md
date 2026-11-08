# Chih-Kai Wang

> Software engineering & AI internship

[f0909172434@gmail.com](mailto:f0909172434@gmail.com) | [github.com/Chih-Kai-Wang](https://github.com/Chih-Kai-Wang) | Taipei, Taiwan

I build Python and TypeScript tools for inspectable AI and math research: a CI check that reads the test report, not the exit code; an audit that ties claims to the bytes of their evidence; a counterexample search that reports the range it searched. I develop with Claude Code and Codex, review every change, and keep negative results public.

## Highlights

- 2 | packages on npm and PyPI
- 3 | pull requests merged upstream
- 1,669 / 1,669 | released inputs accepted
- 4 | negative results kept public

## Education

### National Taipei University of Education | Expected 2028

B.S. student, Mathematics Division, Department of Mathematics and Information Education.

## Projects

### [HonestCI](https://github.com/Chih-Kai-Wang/honest-ci) | v1.0.6 · npm, GitHub Marketplace

TypeScript · Node.js · GitHub Actions

- Checks that JUnit reports are present, fresh, and not below a trusted test-count baseline.
- In the launch demo, a zero-test report with exit code 0 passes a bare workflow; with HonestCI it fails as HCI004_ZERO_TESTS. It does not judge test quality.

### [RigorGraph](https://github.com/Chih-Kai-Wang/rigorgraph) | 1.0.1 · PyPI, public beta

Python · JSON Schema · HTML reports

- Local-first CLI that links research claims to evidence files and independent review records, checks SHA-256 hashes, and writes offline audit reports.
- Changed evidence bytes raise RG_HASH_MISMATCH, and a changed claim invalidates the old acceptance. VERIFIED means accepted by the recorded workflow, not true.

### [Finite Witness](https://github.com/Chih-Kai-Wang/finite-witness-webmcp) | v1.3.0 · browser tool

JavaScript · Web Workers · WebMCP · Python

- Exhaustively searches small graphs (up to 6 vertices) for counterexamples and writes certificates that an independent Python script replays.
- Default run: 39 candidates examined, then a four-cycle with no triangle. Surviving a bounded search is evidence, not proof.

### [SAIR Proof Press](https://github.com/Chih-Kai-Wang/sair-stage2-proof-press) | public companion · frozen artifacts

Python · Lean 4

- Companion to an equational-implication solver: Lean-checked proofs or finite countermodels.
- Frozen artifacts accepted 1,669 / 1,669 released inputs with zero model calls. This is released-input coverage, not a private score or rank.

## Research

- **[RuleDiff negative result](https://github.com/Chih-Kai-Wang/rulediff-negative-result)**: four-page technical report. A lexical predictor scored 0.99 macro-F1 on development data and 0.67 on a held-out packet. Not peer reviewed.
- **[RuleShift](https://github.com/Chih-Kai-Wang/ruleshift)**: research pilot in which simple retrieval matched more complex agent memory strategies.
- **[ProofWeave Core](https://github.com/Chih-Kai-Wang/proofweave-math-lab)**: checks author-written Markdown proofs against pinned Lean 4 / Mathlib and reports certification apart from human-confirmed alignment.

## Merged Upstream

- **[DeepSeek Harness Desktop #740](https://github.com/dsh-tauri/deepseek-harness-desktop/pull/740)**: worktree path normalisation | Sep 2026
- **[dsh-engram #4](https://github.com/kenz1117/dsh-engram/pull/4)**: conservative database migration | Sep 2026
- **[Codex Dream Skin #10](https://github.com/EmiyaKatuz/Codex-Dream-Skin-Needy-Girl-Overdose/pull/10)**: Windows verification failures kept distinguishable | Jul 2026

## Creative Work

ORACLE (short film), The Disease Called AI (song and watercolour MV) and world.execute(me) (terminal PV), October 2026: each rendered entirely from code.

## Skills

- **Languages**: Python, TypeScript, Node.js, Lean 4 (learning), Bash
- **Tools**: GitHub Actions, pytest, Vitest, JSON Schema, MLX, Blender, Claude Code, Codex

_Last updated: October 2026_
