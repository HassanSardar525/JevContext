# Code Review Checklist

Use this checklist after each implementation step. Keep it lightweight.

## Correctness

- Does the change do only what the current phase requires?
- Are edge cases that matter for the current step handled?
- Are failures understandable rather than silently ignored?

## Simplicity

- Is there an easier design that would teach the same concept?
- Did we avoid adding future-phase abstractions?
- Are functions and modules small enough to explain clearly?

## Jev integration

- Are API/SDK details based on current official TypeSafe documentation?
- Is Jev being used for a structured decision rather than text generation?
- Are response types validated or handled safely?
- Are secrets excluded from source control and logs?

## Tests

- Do relevant tests pass?
- Does the example still run?
- Did we test the behavior introduced by this step?

## Learning

- Can the user explain what this change does and why?
- Was `docs/LEARNING_LOG.md` updated when a new concept was taught?

## Documentation

- Does `docs/PROGRESS.md` match reality?
- Was `docs/DECISIONS.md` updated if architecture changed?
- Does README setup remain accurate?

