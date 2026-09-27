# Benchmark Plan

## Purpose

The benchmark exists to answer a simple question:

> When the same coding task and candidate context are used, what changes when Jev chooses context visibility before the final LLM call?

This is a small engineering comparison, not a claim of universal model superiority.

## Compared paths

### Baseline

```text
task + candidate chunks
        ↓
broad context
        ↓
final LLM
        ↓
answer
```

### Jev path

```text
task + same candidate chunks
        ↓
Jev visibility decisions
        ↓
constructed context
        ↓
final LLM
        ↓
answer
```

## Task count

Target **8–15 good tasks** for Version 1.

Do not expand the benchmark merely to make the project look bigger. Prefer tasks with clear expected evidence or outcomes.

## Suggested task types

- Locate which file/function handles a feature.
- Explain a small failing test.
- Trace a function call.
- Identify the likely source of a simple error.
- Explain a small piece of code using multiple files.
- Make or describe a small bounded code change.

## Per-task record

Each task should record something like:

```yaml
id: auth-001
repository: sample-auth-app
task: Why does this login path return HTTP 401?
expected_sources:
  - src/auth.py
  - src/token.py
notes: The benchmark should not reveal the answer to the model.
```

The exact schema can be adjusted during implementation.

## Metrics

Record where available:

- candidate context tokens;
- final context tokens;
- final LLM input tokens;
- final LLM output tokens;
- Jev input/usage;
- Jev latency;
- final LLM latency;
- end-to-end latency;
- estimated total cost;
- task success.

## Cost rule

Do not report only the reduction in final LLM input. If Jev itself introduces measurable usage or latency, include that overhead when discussing the whole system.

## Success evaluation

Keep evaluation simple.

Prefer objective checks when possible:

- expected source/function identified;
- test passes after a bounded change;
- answer contains required evidence;
- manual pass/fail rubric for explanation tasks.

Do not add a complicated judge model unless there is a clear reason later.

## Results table

The final README may contain a table similar to this, using real values only:

| Task | Baseline context | Jev context | Baseline latency | Jev total latency | Baseline result | Jev result |
| --- | ---: | ---: | ---: | ---: | --- | --- |
| auth-001 | TBD | TBD | TBD | TBD | TBD | TBD |

## Interpretation

Useful outcomes include both:

- Jev reduces total work while maintaining useful answers;
- Jev filtering or overhead hurts some tasks, revealing where the approach is not worthwhile.

Both should be documented honestly.

