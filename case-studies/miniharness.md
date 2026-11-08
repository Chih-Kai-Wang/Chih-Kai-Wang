# MiniHarness: turn a curriculum outline into executable lessons

[Repository](https://github.com/Chih-Kai-Wang/miniharness) · [Course website](https://chih-kai-wang.github.io/miniharness/) · [Assessment rubrics](https://github.com/Chih-Kai-Wang/miniharness/blob/main/academy/ASSESSMENT.md)

MiniHarness combines three things: an agent harness written with only the Python
standard library, an eight-step workshop and a curriculum that runs from
computing basics to agent engineering.

## Problem and resulting behavior

The curriculum listed 38 modules, but only two of them were ready. A learner
could see the whole roadmap and still be unable to follow most of it. The
workshop checker also exited successfully when an assignment had failed.

The September 2026 completion added the remaining 36 lessons in Traditional
Chinese. It also added assessment criteria for each goal, 32 concept questions,
five fixed assignment checkers and progress import and export with a version
field. The website now searches the real lesson titles, module IDs and Goal IDs,
and each result links to its source lesson. A failed or missing assignment now
returns a nonzero exit code. Reference solutions and quizzes never mark a
learner's goals as complete.

## Engineering choices and evidence

- **Keep one curriculum manifest.** Readiness counts and website links come from
  the same file that the CLI validates.
- **Give checkers fixed contracts.** The verifier runs known scripts with time
  limits. It never executes command strings stored in lesson metadata.
- **Keep the core small.** The harness depends only on the Python standard
  library. The optional ML examples use a separate environment, so they never
  become runtime dependencies.
- **Keep negative outcomes in view.** A causal Transformer with 14,676 parameters
  learns short phrases
  that the author wrote. Adaptation raised its score
  on two development prompts from 0/2 to 1/2, but held-out perplexity got worse,
  from 2.14 to 16.47. The course reports both results.

Local checks passed 46 core and course tests, four optional ML tests, all five
reference contracts and the eight-step workshop. The ML tests check causal
isolation, finite nonzero gradients, parameter updates and context limits. The
examples ran on CPU, and their tiny fixtures are not a general language
benchmark.

## Limits

All 38 modules now have baseline teaching material in Traditional Chinese.
English module titles exist, but the lessons have not been translated into
English yet. A module marked `ready` has teaching material available. That
status is not evidence that learners completed it or that the teaching works.
Trials with first-time users and learner projects need real participants, and
they are tracked separately.
