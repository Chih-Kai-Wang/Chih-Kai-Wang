# HonestCI: a green process can contain zero tests

[Repository](https://github.com/Chih-Kai-Wang/honest-ci) · [Reproducible demo](https://github.com/Chih-Kai-Wang/honest-ci/blob/main/launch/DEMO.md) · [npm 1.0.4](https://www.npmjs.com/package/honest-ci/v/1.0.4)

HonestCI is a TypeScript command-line tool and GitHub Action that checks the test evidence behind a successful run. It reads JUnit reports and flags missing files, stale results, zero tests and unexpected drops in the test count compared with a trusted baseline.

## Problem and observable result

The launch demo deliberately writes a JUnit report that contains zero tests, then exits with code 0. A workflow that looks only at the exit code reports success.

When the same runner is wrapped with HonestCI, the run reports `HCI004_ZERO_TESTS` and exits with code 1. The demo's verifier checks both exit codes and the error code. It also checks that the failure is not wrongly blamed on a stale report.

## Engineering decisions

- **Treat reports as evidence.** An exit code and a report's test count answer different questions. A false green result can only be diagnosed when both are kept.
- **Keep the baseline out of reach of the change under review.** The reference count comes from a trusted revision. This way a pull request cannot quietly lower the number of tests it is expected to run.
- **Ship bundles that can be rebuilt.** The Action and the CLI include built artifacts. CI rebuilds them and checks that the committed package matches the source and the dependency lockfile.
- **Test the installed package.** Smoke checks run against the package as installed, because some failures do not show up in source-level tests.

## Maintenance example: September 2026

A dependency PR passed the execution checks but failed the package consistency check, because its generated bundles had not been updated. Rebuilding the Action and the CLI in the PR environment brought the package back in line with its source. The full verification command then passed 54 tests, type checks, documentation checks, seven demonstration scenarios and the package smoke checks. [PR #26](https://github.com/Chih-Kai-Wang/honest-ci/pull/26) passed its required checks after that and was merged.

In a separate incident, an earlier macOS / Node 24 build failed with a segmentation fault. Rerunning the failed jobs at the same commit succeeded. This shows that the check recovered, but it does not identify the root cause.

## Limits

A fresh, non-empty test report does not show that the assertions are useful, that coverage is adequate or that the software is correct. HonestCI checks only that the evidence is intact, within the report and baseline rules it declares.

## Next useful experiment

The next step is to collect a few real configuration mistakes from a small repository. For each one, the question is whether the error report alone tells a maintainer enough to fix it without reading the implementation.
