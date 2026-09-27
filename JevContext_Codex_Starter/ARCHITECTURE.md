# Architecture

## Design goal

Keep the system small enough to understand completely while still demonstrating a real use of Jev.

The project has one main job: **decide how much of each candidate context chunk should be shown to the final LLM for one coding task.**

## High-level architecture

```text
                  ┌─────────────────┐
                  │   Coding Task   │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ File Ingestion  │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │     Chunks      │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Jev Decisions   │
                  └────────┬────────┘
                           │
                HIDE / SHORT / LONG / FULL
                           │
                           ▼
                  ┌─────────────────┐
                  │ Context Builder │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │    Final LLM    │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Answer + Metrics│
                  └─────────────────┘
```

## Components

### 1. Chunk model

A chunk is one addressable piece of context. Version 1 should keep this model simple.

Possible fields:

```text
id
source path
chunk type
content
line range
approximate token count
optional metadata
```

Chunks may represent a file section, log output, diff, or instruction.

### 2. Ingestion

The first implementation only needs to work well on small repositories. It should:

- walk allowed files;
- ignore obvious generated/vendor/secret directories;
- split text into manageable chunks;
- preserve source path and line information.

Do not build production indexing in Version 1.

### 3. Jev decision layer

For a coding task, Jev receives enough state to judge how useful each candidate chunk is and returns structured decisions.

Jev does **not** write the final answer. It decides how the program should treat context.

The implementation should begin with a minimal decision shape and only add complexity when required.

### 4. Visibility policy

The target states are:

- `HIDE` — omit the chunk.
- `SHORT` — provide a compact representation.
- `LONG` — provide a larger representation.
- `FULL` — provide the full chunk.

Implementation should be incremental:

1. Make `HIDE` and `FULL` work end-to-end first.
2. Then add `SHORT` and `LONG` using a deliberately simple representation policy.

Jev chooses the visibility state. A separate representation function turns that state into text. This keeps the model decision separate from ordinary program logic.

### 5. Context builder

The context builder:

- applies visibility decisions;
- formats source labels clearly;
- respects a configurable token budget;
- produces one final context string or message list for the LLM.

### 6. Final LLM

Use one fixed LLM/provider for the initial comparison. The LLM receives the task plus the built context and produces the coding answer.

The project is not about model routing, so do not add multiple final models in Version 1.

### 7. Metrics

For each run, record at minimum:

- candidate context size;
- final context size;
- Jev input usage if available;
- final LLM input/output usage if available;
- Jev latency;
- final LLM latency;
- end-to-end latency;
- estimated cost when pricing information is available;
- task success or a simple evaluation result.

## Baseline

The baseline must use the same task and same candidate chunks.

```text
same task + same candidate chunks
            │
     ┌──────┴──────┐
     ▼             ▼
 broad context   Jev selection
     │             │
     ▼             ▼
 final LLM       final LLM
```

This makes the comparison understandable: the main difference is whether Jev chooses context visibility.

## Boundaries

Keep these boundaries explicit:

- Jev makes decisions.
- Python code applies those decisions.
- The final LLM generates the answer.
- Metrics observe the system.

That separation is the core learning value of the project.

