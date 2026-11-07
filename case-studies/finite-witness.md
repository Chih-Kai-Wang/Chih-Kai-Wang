# Finite Witness: make a counterexample inspectable

[Live workbench](https://f0909172434.github.io/finite-witness-webmcp/) · [Source](https://github.com/f0909172434/finite-witness-webmcp) · [CV](../cv/CV.md)

Finite Witness is a browser workbench for testing conjectures about finite graphs. When a claim fails, it returns the graph that breaks it and the properties that show why that graph is a counterexample. A person using the page and an agent using WebMCP drive the same application.

## Problem and observable result

Take the claim that every simple graph with at least three vertices and minimum degree at least two contains a triangle.

With the default search range of 3–6 vertices, the recorded run examined 39 candidates before it found the four-cycle C₄. This graph has four vertices, four edges, degree sequence `[2, 2, 2, 2]` and zero triangles. It meets every assumption and violates the conclusion. Its deterministic certificate is `fw-b20670c4`.

A single counterexample is enough to disprove a universal claim. The reverse does not hold. A search that finds no counterexample shows only that no witness exists in the range it actually searched.

## Engineering decisions

- **Keep search off the UI thread.** Graph enumeration runs in a Web Worker, so the page stays responsive while a bounded exhaustive search is running.
- **Use one engine for people and agents.** Eight WebMCP operations expose the same behavior as the visible workbench. Because there is no separate agent implementation, an agent's answer is less likely to disagree with what a person sees.
- **Record the prefix that was actually searched.** Search stops at the first witness in vertex-count and edge-mask order. The certificate keeps the requested range apart from the part that was visited, so finding C₄ does not imply that every six-vertex graph was checked.
- **Let users check proposed repairs.** Each suggested change to the assumptions excludes the current witness, and the user can run the search again on the repaired claim. Excluding one witness does not prove the repaired claim.

## Verification

The repository's nine tests cover graph properties, known counterexamples, bounded claim formatting, round-trips of shareable experiments, repair behavior, handling of damaged evidence and deterministic certificates. The suite passed locally on September 5, 2026. Earlier in the same review, a live browser check confirmed that the visible result, the WebMCP search response and the certificate agreed with each other.

Source pointers: [graph engine](https://github.com/f0909172434/finite-witness-webmcp/blob/main/src/graph-engine.js), [worker](https://github.com/f0909172434/finite-witness-webmcp/blob/main/src/search-worker.js), [WebMCP adapter](https://github.com/f0909172434/finite-witness-webmcp/blob/main/src/webmcp.js), [tests](https://github.com/f0909172434/finite-witness-webmcp/tree/main/tests).

## Next useful experiment

The next step is to watch a first-time user check a conjecture and then explain the difference between a requested range and an exhausted range. Wherever the interface fails to get that distinction across, the failure should be recorded before anything is changed.
