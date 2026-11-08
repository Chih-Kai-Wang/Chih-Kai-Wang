# RigorGraph: keep claims connected to their evidence

[Repository](https://github.com/Chih-Kai-Wang/rigorgraph) · [PyPI 1.0.1](https://pypi.org/project/rigorgraph/1.0.1/)

RigorGraph is a Python command-line tool that stores claims and their evidence as records under version control. Its audits give the same result for the same records, and it writes self-contained HTML reports that open without a network connection. The released package is a public beta.

## Problem and observable result

A review goes out of date when the claim or a supporting file changes after it. A bare "verified" label hides the fact that the review depended on those exact contents.

RigorGraph records each claim, the hashes of its evidence and a snapshot of each review. Its tests show that changing a byte of evidence produces `RG_HASH_MISMATCH`, and that changing the claim invalidates the earlier acceptance snapshot with `RG_SNAPSHOT_MISMATCH`. The audit also checks for dependency cycles, missing evidence requirements, evidence that was never checked and invalid status transitions.

## Engineering decisions

- **Store records as version-controlled data.** Records and schemas are JSON files, so changes to them are reviewed in the same workflow as source code.
- **Keep evidence identity apart from judgment.** A matching hash shows that a file is byte-for-byte the same. Acceptance or rejection, with its scope, lives in the review record, and a hash says nothing about scientific validity.
- **Generate a portable report.** The offline HTML viewer travels with the result and needs no running backend. The cost is one more generated artifact that has to stay reproducible.
- **Keep failures visible.** Missing evidence or an invalid review state produces an audit finding. The tool never keeps an old status quietly in place.

## Verification and maintenance

On September 5, 2026, the local maintenance checks passed 64 tests, lint, schema validation and the full release check, which includes the frontend and plugin builds. The dependency update in [PR #19](https://github.com/Chih-Kai-Wang/rigorgraph/pull/19) required rebuilding the offline viewer from its frontend source. Nobody edited the generated file by hand. The updated PR passed the required checks and was merged.

Source pointers: [audit tests](https://github.com/Chih-Kai-Wang/rigorgraph/blob/main/tests/test_audit.py), [frontend](https://github.com/Chih-Kai-Wang/rigorgraph/tree/main/frontend), [Python implementation](https://github.com/Chih-Kai-Wang/rigorgraph/tree/main/src/rigorgraph).

## Inspect the exported reports

The [valid math report](https://chih-kai-wang.github.io/examples/rigorgraph/math.html) and the [invalid promotion report](https://chih-kai-wang.github.io/examples/rigorgraph/invalid.html) are real self-contained exports of the built-in demo fixtures. The first audit returned PASS with exit code 0, and the second returned FAIL with exit code 1. The invalid fixture reports `RG_EVIDENCE_TYPE_MISSING` and `RG_ACCEPT_EVIDENCE_UNCHECKED`. The [walkthrough](https://github.com/Chih-Kai-Wang/rigorgraph/blob/main/docs/REPORT_WALKTHROUGH.md) gives the commands to reproduce both reports and their snapshot hashes. The demo review records are synthetic and are not new independent reviews of research.

## Limits

The audit checks the workflow and the integrity of the records. It does not decide whether a scientific conclusion is true. A first-user trial should test whether someone can follow a claim to its evidence and explain correctly why the invalid promotion failed.
