---
name: to-tasks
description: Create or update an implementation plan and task files from a spec or a clear conversation. Use to break work into small, verifiable vertical slices. Also update existing plans and tasks with new context.
---

# To-Tasks

Create `PLAN.md` and all task files. Never create specs or write implementation code, except `Required implementation:` blocks under the Design rules.

Do not create a plan for a trivial change unless the user explicitly requests one. A trivial change is clear, has low risk, and has no material unknowns or dependent work. Invoking `$to-tasks` counts as an explicit request for a plan.

## Workflow

1. Read the input, repository guidance, and relevant code. Preserve agreed requirements and decisions. Require approval of the relevant spec scope before finalizing the plan and tasks.
2. Ask about missing decisions that change scope, dependencies, or acceptance criteria. Continue planning work that does not depend on those decisions. Record remaining questions and assumptions in the plan.
3. Use the requested output directory. Otherwise, place the plan beside the input spec. For conversation input, use `docs/features/<feature>/` from the repository root.
4. Read [PLAN.md](templates/PLAN.md) when drafting or changing the plan structure. Read [TASK.md](templates/TASK.md) when drafting or changing task files. Use neither template for status-only updates.
5. Save the draft `PLAN.md` in the output directory and task files in its `tasks/` directory. Name tasks `01-<outcome>.md`, `02-<outcome>.md`, and so on. Within dependency constraints, place tasks that resolve major technical risks or unknowns as early as possible.
6. Summarize the output and unresolved items. List contract changes in one line per task and link to the Design sections. Request one review of the complete output. Revise the same files as needed. Treat the output as final only after explicit user approval. Record the human approval in `PLAN.md`.

## Plan

- Keep the overview to one short paragraph. Link to the input spec without repeating its requirements. For conversation input, use agreed decisions directly. Do not add conversation quotes or references.
- Include architecture decisions only when they add implementation detail to the source. Record task-local decisions in the plan too. Write each decision as one line: `ADRn: decision and rationale`. Do not use code. Do not reuse or renumber IDs. Mark a replaced decision `Superseded by ADRn`.
- Use stages when grouping helps. Name stages for the actual work. Foundation, Core Features, and Polish are examples, not required stages.
- Keep one ordered task list across stages. Link each task file. Use `[ ]` for not done and `[x]` for done.
- Give each stage a checkpoint with specific checks and expected results. For an ungrouped task list, use one completion checkpoint.
- Include risks and open questions when needed. Omit empty optional sections.

## Tasks

- State an observable outcome. Add a description of one or two sentences for context and purpose.
- Define concrete requirements, acceptance criteria, dependencies, and verification checks with expected results. Include applicable repository checks. Report existing failures and require no new failures.
- When behavior has edge cases, exact outputs, or error cases, state acceptance criteria as concrete input → expected output pairs.
- Each task must leave the repository in a valid, verifiable state when complete. Do not rely on later tasks to restore working behavior.
- Link to relevant spec sections when available. Omit the source field for conversation input.
- Show contracts and any required implementations in the Design section under the [Design](#design) rules. Otherwise, do not prescribe implementation steps or function bodies. Put rationale in the plan Architecture Decisions. Preserve established implementation constraints and architecture decisions that are required for the task. Include estimated file paths only as optional references.
- When existing code establishes the pattern to follow, reference it with what to mirror. Do not write new example code to show a pattern that already exists in the repository.
- Keep feature migrations, configuration changes, and tests with the slice that needs them.
- Allow separate technical tasks only for required foundation work. Feature database changes and backend work are not foundation by default.
- Resolve technical risks through vertical slices or required foundation tasks.

### Vertical slices

**Bad: horizontal slices**

```text
1. Build the database schema.
2. Build all API endpoints.
3. Build all UI components.
4. Connect the layers.
```

**Good: vertical slices**

```text
1. User can register (schema + API + UI for registration).
2. User can log in (schema + API + UI for login).
3. User can create a task (schema + API + UI for creation).
4. User can view tasks (query + API + UI for the list).
```

### Task size

Use file counts as estimates. Prefer XS, S, and M. Allow L when a smaller split prevents separate verification. Split XL tasks. Do not separate layers to reduce file counts.

| Size | Estimated files | Scope |
|------|-----------------|-------|
| XS | 1 | One rule or configuration change |
| S | 1–2 | One small behavior |
| M | 3–5 | One feature slice |
| L | 6–8 | One larger, verifiable slice |
| XL | 9+ | Too large; split further |

## Design

Plans and tasks show contracts in a `## Design` section for human review.

- Include a Design section when the work adds or changes one of these items:
  - an exported API or signature
  - a module boundary or abstraction
  - a database schema or migration
  - a configuration or environment shape
  - a CLI, HTTP, or event contract
  - a file or directory layout
  - a test harness structure
  - an error type, error code, or failure response shape
- Omit the Design section for internal-only changes.
- Put the overall structure in the plan: boundaries, layout, flow, and contracts that two or more tasks use. Put contracts that only one task uses in that task. Refer to plan decisions by `ADRn`. Link to shared plan contracts. Do not copy them.
- Use sketch blocks and one-line shape bullets. A shape bullet states what exists, where, and its lifetime or ownership. Do not give rationale.
- Write sketches in the project language. Show signatures and types only. Do not write function bodies. Use comments only to state intent.
- Include error types or failure shapes in signatures when callers depend on them.
- Exception: when a specific implementation is required, include it in a block labeled `Required implementation:` and record the rationale as an ADR. Use this only when a different implementation would be rejected in review. Never include implementation code as an unlabeled example.
- Show file layout as a tree delta: `+` new, `~` changed, `-` removed. Use a small Mermaid or ASCII diagram only for a flow or lifecycle. Show changed contracts as before → after.
- Keep each block to approximately 20 lines. This limit does not apply to required implementations.
- Declarative schemas (DDL, OpenAPI, JSON Schema, config shapes) are contracts and may be shown in full. They may exceed the 20-line guideline when they cannot be split by entity or endpoint.
- Implementation must match the public names, signatures, and boundaries in the sketches. Implementation can change private internals. Do not add public units outside the sketches. A contract change is a plan or task change.

## Updates and shared rules

- Before saving, check for an existing plan. Never overwrite a plan for unrelated work. Report the conflict and use another location only after the user resolves the conflict.
- Task completion status is recorded in `PLAN.md` only. Mark a task done only after its acceptance criteria pass and the human explicitly accepts the implementation result.
- Preserve completed task records and existing filenames. Add or revise unfinished tasks when requirements change.
- Do not repeat rules from `AGENTS.md` or other repository guidance in the plan or tasks. Include only feature-specific additions, explicit changes, or exceptions.

- For updates, read the existing plan, task files, and new context.
- Obtain explicit human approval of changed plan and task scope. Do not change criteria to excuse failing code.
- Add a new task for changes or defects in accepted work. Link the new task to the earlier task. Update affected checkpoints.
- Keep check results, human review feedback, acceptance evidence, and remaining work in the task. These notes and plan checkbox updates do not require new document approval.
