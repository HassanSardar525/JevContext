# Decision Log

This is a lightweight architecture decision log. Add an entry only when a decision affects the shape of the project or future work.

Use this format:

```text
## D-XXX — Decision title
Date:
Status: Accepted / Replaced / Proposed

Context:

Decision:

Why:

Consequences:
```

---

## D-001 — Keep Version 1 focused on context management

**Status:** Accepted

### Context

The wider Jev coding-agent architecture includes routing, permissions, tools, sub-agents, and shared retrieval. Building all of that would hide the main learning goal and make a one-person project unnecessarily large.

### Decision

Version 1 will implement only the context-selection path, baseline comparison, and basic measurement.

### Why

This is enough to explore Jev in a real workflow and produce measurable portfolio evidence.

### Consequences

Future features stay out of scope until the core experiment is complete.

---

## D-002 — Use Python 3.11+ and `uv`

**Status:** Accepted

### Context

The project needs a small, modern Python setup that is easy to reproduce.

### Decision

Use Python 3.11+ with `uv` for dependency and environment management.

### Why

It keeps setup simple and is appropriate for a small Python package.

### Consequences

The README and automated checks should use `uv` commands consistently.

---

## D-003 — Keep AGENTS.md small and docs as the source of truth

**Status:** Accepted

### Context

Long monolithic agent instruction files waste context and become stale.

### Decision

Use `AGENTS.md` as a concise operating guide and navigation map, with detailed project knowledge stored in versioned Markdown documents.

### Why

This keeps agent instructions readable while preserving durable project context.

### Consequences

When architecture, scope, progress, or benchmarks change, update the relevant document instead of bloating `AGENTS.md`.

---

## D-004 — Teach before implementing each phase

**Status:** Accepted

### Context

The user is building this project primarily to explore and understand Jev, not just to obtain generated code.

### Decision

Before each phase, the coding agent must explain the concept, data flow, files, and success criteria and wait for user approval.

### Why

The learning process is a first-class deliverable.

### Consequences

The project may progress more slowly than a fully autonomous build, but the user should understand the system they eventually present publicly.

