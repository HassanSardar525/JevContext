# JevContext

**Query-aware context selection for coding tasks using Jev.**

JevContext is a small learning and engineering project built to explore how Jev can be used as a fast decision layer inside an AI coding workflow.

Instead of sending every available file, log, diff, or code chunk to a final LLM, JevContext asks Jev which pieces of context matter for the current coding question. The project then constructs a smaller context and compares the result with a simple broad-context baseline.

## Why this project exists

Coding workflows often accumulate much more context than a model needs for one question. This project explores a narrow idea:

> Can Jev help decide what an LLM should see for a coding task while reducing unnecessary context without making the answer worse?

This is intentionally **not** a full coding agent. It is a focused project for learning Jev and producing a useful, measurable portfolio project.

## Planned flow

```text
Coding task
    ↓
Small repository / files / logs
    ↓
Chunk ingestion
    ↓
Candidate chunks
    ↓
Jev visibility decisions
    ↓
HIDE / SHORT / LONG / FULL
    ↓
Context builder + token budget
    ↓
Final LLM
    ↓
Answer + metrics
```

A baseline path sends the same candidate set without Jev filtering so the two approaches can be compared.

## Version 1 goals

- Load a small repository or directory.
- Represent source material as addressable chunks.
- Call Jev with the task and chunk information.
- Convert Jev decisions into `HIDE`, `SHORT`, `LONG`, or `FULL` visibility.
- Build final context under a token budget.
- Send the context to one LLM.
- Record tokens, latency, estimated cost, and task outcome.
- Compare against a broad-context baseline.
- Run a small benchmark of approximately 8–15 tasks.
- Package the result as a clean Python project with documentation and tests.

## Non-goals

Version 1 will not build a full autonomous coding agent, vector database, multi-agent system, model router, permission engine, or hosted product.

## Current status

**Planning / Phase 0.** No implementation should begin until the first phase has been explained to the user and approved.

See [`docs/PROGRESS.md`](docs/PROGRESS.md) for the live project status.

## Documentation map

- [`AGENTS.md`](AGENTS.md) — instructions for Codex and other coding agents.
- [`ARCHITECTURE.md`](ARCHITECTURE.md) — planned system design.
- [`docs/PROJECT_PROPOSAL.md`](docs/PROJECT_PROPOSAL.md) — full project proposal.
- [`docs/IMPLEMENTATION_PLAN.md`](docs/IMPLEMENTATION_PLAN.md) — phased execution plan.
- [`docs/PROGRESS.md`](docs/PROGRESS.md) — current progress and next step.
- [`docs/DECISIONS.md`](docs/DECISIONS.md) — architecture and project decisions.
- [`docs/LEARNING_LOG.md`](docs/LEARNING_LOG.md) — concepts explained during development.
- [`docs/BENCHMARK_PLAN.md`](docs/BENCHMARK_PLAN.md) — experiment design.
- [`docs/REFERENCES.md`](docs/REFERENCES.md) — references and documentation links.

## Planned repository structure

```text
jev-context/
├── AGENTS.md
├── README.md
├── ARCHITECTURE.md
├── CODEX_KICKOFF.md
├── .env.example
├── .gitignore
├── pyproject.toml                 # created in Phase 1
├── src/
│   └── jev_context/
│       ├── __init__.py
│       ├── models.py
│       ├── ingestion.py
│       ├── jev_client.py
│       ├── selector.py
│       ├── representations.py
│       ├── builder.py
│       ├── metrics.py
│       └── pipeline.py
├── examples/
│   └── basic_demo.py
├── benchmarks/
│   ├── tasks/
│   ├── run_baseline.py
│   ├── run_jev.py
│   └── analyze_results.py
├── tests/
└── docs/
    ├── PROJECT_PROPOSAL.md
    ├── IMPLEMENTATION_PLAN.md
    ├── PROGRESS.md
    ├── DECISIONS.md
    ├── LEARNING_LOG.md
    ├── BENCHMARK_PLAN.md
    └── REFERENCES.md
```

The exact module split may change slightly during implementation. Any meaningful change should be recorded in `docs/DECISIONS.md`.

## Learning mode

This repository is intentionally configured so the coding agent acts as both an engineer and a teacher. Before each phase it must explain the concept, the reason for the change, the expected files, and the success criteria, then wait for approval before coding.

## Expected final portfolio result

The final project should be easy to describe in one sentence:

> Built a Jev-powered query-aware context manager for coding tasks and compared it with a broad-context baseline using real measurements of context size, latency, cost, and task success.

Actual benchmark numbers must come from the project. Do not invent improvement percentages.

