# AGENTS.md — JevContext

## Mission

Build a small, understandable, working project that explores **Jev as a decision layer for coding-agent context selection**.

The goal is not to build a complete coding agent. The goal is to learn Jev, use it in a real workflow, and produce a project that can be explained clearly in a README, interview, resume, or LinkedIn post.

## Read this first

Before changing code, read:

1. `README.md` — human-facing project overview.
2. `ARCHITECTURE.md` — system boundaries and data flow.
3. `docs/PROJECT_PROPOSAL.md` — scope, goals, and non-goals.
4. `docs/IMPLEMENTATION_PLAN.md` — ordered phases and acceptance criteria.
5. `docs/PROGRESS.md` — current status and next task.
6. `docs/DECISIONS.md` — decisions already made.
7. `docs/LEARNING_LOG.md` — concepts already explained to the user.
8. `docs/BENCHMARK_PLAN.md` — how results will be measured.
9. `docs/REFERENCES.md` — source material and official documentation.

Treat the repository documentation as the source of truth. Keep this file short; put detailed knowledge in `docs/`.

## Scope guardrails

Version 1 includes:

- Python package structure.
- Repository/file ingestion for small codebases.
- Chunk representation and metadata.
- Jev integration using structured decisions.
- Query-aware visibility decisions.
- Visibility levels: `HIDE`, `SHORT`, `LONG`, `FULL`.
- Context construction under a configurable token budget.
- One final LLM call using the constructed context.
- A broad-context baseline.
- Basic measurement of tokens, latency, estimated cost, and task success.
- A small benchmark of roughly 8–15 tasks.
- Tests, documentation, and an example/demo.

Version 1 does **not** include:

- A full autonomous coding agent.
- Vector databases or production repository indexing.
- Multi-agent orchestration.
- Dynamic model routing.
- Permission engines.
- Complex tool routing.
- Hosted SaaS infrastructure.
- Premature framework integrations.

Do not add future-phase features unless the user explicitly asks for them.

## Learning-first workflow — mandatory

The user is learning Jev while building this project. Do not silently implement large pieces.

Before starting a new phase or introducing a new important concept:

1. Explain in simple language what will be built.
2. Explain why it exists in this project.
3. Explain the relevant Jev concept.
4. Show the intended data flow with a small example.
5. List the files you expect to create or modify.
6. State the acceptance criteria.
7. Ask the user to approve moving forward.

Only after approval should implementation begin.

After implementing a step:

1. Summarize what changed.
2. Explain the important code in teaching language.
3. Show how to run it.
4. Run relevant tests/checks.
5. Record the result in `docs/PROGRESS.md`.
6. Record meaningful architecture choices in `docs/DECISIONS.md`.
7. Record the concept taught in `docs/LEARNING_LOG.md`.

Do not jump multiple phases ahead in one turn unless the user explicitly requests it.

## Jev-specific rules

- Jev is used for **structured decisions**, not free-form text generation.
- Do not pretend Jev writes summaries or code unless official capabilities explicitly support that.
- Keep the Jev integration behind a small internal interface so the rest of the project remains understandable.
- Verify the current official TypeSafe API/SDK before writing integration code. Do not guess package names, models, fields, or response shapes.
- Store API keys only in environment variables. Never commit secrets.
- Start with the simplest working decision flow before optimizing it.

## Implementation style

- Python 3.11+.
- Prefer standard library and small dependencies.
- Use type hints for public functions and important data structures.
- Keep modules small and responsibilities obvious.
- Prefer readable code over clever abstractions.
- Avoid unnecessary design patterns.
- Add tests for behavior that matters to the learning goal.
- Keep public APIs small.

## Suggested commands

Once the project is initialized, keep these commands working and document any change:

```bash
uv sync
uv run pytest
uv run ruff check .
```

If the project does not yet have these tools configured, explain and add them during the appropriate setup phase rather than assuming they exist.

## Documentation rules

- `README.md` is for people discovering the project.
- `AGENTS.md` is for coding-agent operating instructions and navigation.
- `ARCHITECTURE.md` explains stable system structure.
- `docs/PROJECT_PROPOSAL.md` defines project intent and scope.
- `docs/IMPLEMENTATION_PLAN.md` defines ordered work.
- `docs/PROGRESS.md` is the live status board.
- `docs/DECISIONS.md` records important decisions and reasons.
- `docs/LEARNING_LOG.md` records what was explained and learned.
- `docs/BENCHMARK_PLAN.md` defines experiments before results are collected.

Update docs as part of the same change when reality changes.

## Definition of done for a task

A task is complete only when:

- The requested behavior works.
- Relevant tests pass.
- The user can understand what was added.
- Documentation matches the implementation.
- `docs/PROGRESS.md` reflects the new state.

