# JevContext — Project Proposal

## 1. Project summary

**JevContext** is a focused Python project for exploring Jev by using it as a query-aware context-selection layer for coding tasks.

The project will take a coding question plus a collection of source-code or diagnostic chunks, ask Jev how much of each chunk should be visible, build the final context, send that context to an LLM, and compare the result with a broad-context baseline.

The intended output is a working demo, a small reusable package, a benchmark with real measurements, and documentation strong enough to support a resume entry or LinkedIn post.

## 2. Main question

> Can Jev make useful context decisions for coding tasks so that a final LLM receives less unnecessary context while preserving useful answers?

The project does not assume the answer is yes. The purpose is to explore the idea honestly and measure what happens.

## 3. Why this is useful

This project gives hands-on experience with:

- Jev's structured decision interface;
- state and typed decisions;
- context engineering;
- chunk-based state representation;
- token budgeting;
- basic LLM instrumentation;
- controlled baseline comparisons;
- packaging and documenting an AI engineering project.

It also produces something concrete: a small context-management component rather than another generic chatbot.

## 4. Version 1 scope

### Included

- Python 3.11+ project using `uv`.
- Simple ingestion for small repositories/directories.
- Addressable context chunks with metadata.
- Official Jev API/SDK integration.
- Query-aware context visibility decisions.
- `HIDE`, `SHORT`, `LONG`, and `FULL` visibility states.
- A context builder with a token budget.
- One fixed final LLM for experiments.
- Broad-context baseline.
- Token, latency, cost, and simple success measurements.
- Approximately 8–15 benchmark tasks.
- Unit tests for core logic.
- A basic runnable example.
- Clear README and project documentation.

### Explicitly excluded

- Complete autonomous coding agent.
- Embedding database or production search system.
- Sophisticated multi-model routing.
- Permission engine.
- Sub-agent orchestration.
- Shared concurrent agent state.
- Hosted web application or SaaS.
- Large benchmark suite.

These can be explored later only if Version 1 is complete and useful.

## 5. Core workflow

```text
1. User gives a coding task.
2. Project loads a small set of candidate files/artifacts.
3. Files/artifacts become chunks.
4. Jev decides the visibility of each chunk for this task.
5. Python applies those visibility decisions.
6. Context builder respects a token budget.
7. Final LLM receives task + selected context.
8. Metrics are recorded.
9. Same task is run through a broad-context baseline.
10. Results are compared.
```

## 6. Visibility model

The target interface is intentionally easy to explain:

| Visibility | Meaning |
| --- | --- |
| `HIDE` | Exclude the chunk. |
| `SHORT` | Include a compact representation. |
| `LONG` | Include a larger representation. |
| `FULL` | Include the complete chunk. |

Implementation should first prove `HIDE/FULL`, then add `SHORT/LONG` without introducing unnecessary complexity.

## 7. Deliverables

By the end of Version 1, the repository should contain:

- installable/runnable Python project;
- working Jev decision call;
- chunk ingestion and visibility selection;
- final context builder;
- final LLM example;
- baseline runner;
- Jev runner;
- small task set;
- result JSON/CSV or equivalent;
- simple result table/plots if useful;
- tests;
- architecture documentation;
- learning log;
- README with setup, demo, design, limitations, and actual results.

## 8. Definition of success

The project is successful when another developer can:

1. install the repository;
2. configure the required API keys;
3. point the demo at a small codebase or provided sample;
4. submit a coding question;
5. inspect Jev's visibility decisions;
6. inspect the final context;
7. receive a final LLM answer;
8. run the baseline and Jev comparison.

A positive performance result is desirable but not required. An honest finding that Jev overhead or filtering mistakes make the approach less useful is still a valid learning outcome.

## 9. Portfolio positioning

A suitable final description, once implemented and measured, is:

> Built and evaluated a Jev-powered query-aware context manager for coding tasks, using structured visibility decisions to construct token-budgeted LLM context and comparing it with a broad-context baseline on token usage, latency, cost, and task success.

Any numerical improvement must be replaced with actual measured results.

