# Implementation Plan

The project should be built in small phases. Each phase begins with a teaching explanation and explicit user approval.

## Phase 0 — Planning and repository setup

### Goal

Make the project easy for both the user and Codex to understand before implementation begins.

### Tasks

- Confirm scope and non-goals.
- Verify official Jev API/SDK documentation.
- Confirm Python and package-management choices.
- Create `pyproject.toml` and minimum developer tooling.
- Create `.env.example` without secrets.
- Ensure test and lint commands work.

### Teaching topic

Explain the difference between:

- Jev making a structured decision;
- normal Python control flow;
- an LLM generating text.

### Acceptance criteria

- Project installs locally.
- `uv run pytest` works, even if only a smoke test exists.
- `uv run ruff check .` works.
- No API key is committed.

---

## Phase 1 — First Jev call

### Goal

Make the smallest possible real Jev request and inspect its structured result.

### Tasks

- Add a tiny Jev client wrapper.
- Read API key from the environment.
- Send a simple state and one structured decision question.
- Parse/validate the response.
- Add a small test around internal response handling where practical.
- Create an example script.

### Teaching topic

Explain Jev's mental model:

```text
state + typed question → structured decision
```

Explain whichever official question type is used in the first call and why.

### Acceptance criteria

- User can run one command and see a real Jev decision.
- Errors are readable when the API key is missing.
- No final LLM is involved yet.

---

## Phase 2 — Chunks and simple HIDE/FULL selection

### Goal

Connect Jev to the actual project idea.

### Tasks

- Define a simple `Chunk` model.
- Load text/code files from a small directory.
- Split them into manageable chunks.
- Preserve source and line metadata.
- Ask Jev whether candidate chunks should be `HIDE` or `FULL` for a query.
- Print decisions in an understandable form.

### Teaching topic

Explain why chunks are addressable state and why selection depends on the current query.

### Acceptance criteria

Given a small example repository and a question, the program prints a visibility decision for each candidate chunk.

---

## Phase 3 — Four visibility levels and context builder

### Goal

Turn decisions into final LLM context.

### Tasks

- Expand visibility to `HIDE`, `SHORT`, `LONG`, `FULL`.
- Implement a deliberately simple representation policy for `SHORT` and `LONG`.
- Add a token-budget setting.
- Build one final context from selected chunks.
- Preserve source labels so the result is inspectable.

### Teaching topic

Explain the difference between:

- selection: "how useful is this chunk?";
- representation: "how much of this chunk do we include?";
- budgeting: "how much total context can we afford?"

### Acceptance criteria

The user can inspect:

- original candidates;
- Jev visibility choices;
- final context;
- approximate before/after token counts.

---

## Phase 4 — Final LLM and baseline

### Goal

Make the full useful demo work.

### Tasks

- Add one final LLM provider/configuration.
- Implement a broad-context baseline using the same candidates.
- Run both paths for the same task.
- Capture response and usage metadata.
- Keep provider code small and isolated.

### Teaching topic

Explain why the baseline must use the same task, candidate set, and final model.

### Acceptance criteria

One command or example can show:

```text
Baseline → context → final answer
Jev      → selected context → final answer
```

with basic metrics for both.

---

## Phase 5 — Measurement and small benchmark

### Goal

Produce real evidence for the README and portfolio.

### Tasks

- Create approximately 8–15 small coding tasks.
- Keep repository state and expected outcome documented.
- Run baseline and Jev path on the same tasks.
- Record:
  - final LLM input tokens;
  - final LLM output tokens;
  - Jev usage where available;
  - total/end-to-end latency;
  - estimated cost where possible;
  - simple task success.
- Export results in a simple machine-readable format.

### Teaching topic

Explain the difference between context reduction and **net system improvement**.

### Acceptance criteria

At least 8 tasks have comparable baseline/Jev runs with real recorded results.

---

## Phase 6 — Polish and release

### Goal

Turn the learning project into something another person can understand and run.

### Tasks

- Clean public API and examples.
- Improve error messages.
- Complete tests.
- Update README with actual results.
- Document limitations and failure cases.
- Add a small architecture diagram if useful.
- Ensure all setup steps are reproducible.
- Prepare a concise resume bullet and LinkedIn-ready project summary based on actual results.

### Acceptance criteria

A new developer can clone the repository, follow the README, run the example, and understand what was learned.

## Scope-control rule

Do not start model routing, sub-agents, permission systems, vector search, or a web UI during these phases. Finish this core project first.

