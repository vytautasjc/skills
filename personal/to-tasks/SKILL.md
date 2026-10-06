---
name: to-tasks
description: Create or update an implementation plan and task files from a spec or a clear conversation. Use to break work into small, verifiable vertical slices.
disable-model-invocation: true
---

# To-Tasks

Create `PLAN.md` and all task files. Never create specs or write implementation code.

Do not create a plan for a trivial change unless the user explicitly requests one. A trivial change is clear, has low risk, and has no material unknowns or dependent work. Invoking `$to-tasks` counts as an explicit request for a plan.

## Workflow

1. Read the input, repository guidance, and relevant code. Preserve agreed requirements and decisions.
2. Ask about missing decisions that change scope, dependencies, or acceptance criteria. Continue planning work that does not depend on those decisions. Record remaining questions and assumptions in the plan.
3. Use the requested output directory. Otherwise, place the plan beside the input spec. For conversation input, use `docs/features/<feature>/` from the repository root.
4. Read [PLAN.md](templates/PLAN.md) when drafting or changing the plan structure. Read [TASK.md](templates/TASK.md) when drafting or changing task files. Use neither template for status-only updates.
5. Save the draft `PLAN.md` in the output directory and task files in its `tasks/` directory. Name tasks `01-<outcome>.md`, `02-<outcome>.md`, and so on. Within dependency constraints, place tasks that resolve major technical risks or unknowns as early as possible.
6. Summarize the output and unresolved items. Request one review of the complete output. Revise the same files as needed. Treat the output as final only after explicit user approval.

## Plan

- Keep the overview to one short paragraph. Link to the input spec without repeating its requirements. For conversation input, use agreed decisions directly. Do not add conversation quotes or references.
- Include architecture decisions only when they add implementation detail to the source.
- Use stages when grouping helps. Name stages for the actual work. Foundation, Core Features, and Polish are examples, not required stages.
- Keep one ordered task list across stages. Link each task file. Use `[ ]` for not done and `[x]` for done.
- Give each stage a checkpoint with specific checks and expected results. For an ungrouped task list, use one completion checkpoint.
- Include risks and open questions when needed. Omit empty optional sections.

## Tasks

- State an observable outcome. Add a description of one or two sentences for context and purpose.
- Define concrete requirements, acceptance criteria, dependencies, and verification checks with expected results. Include applicable repository checks. Report existing failures and require no new failures.
- Each task must leave the repository in a valid, verifiable state when complete. Do not rely on later tasks to restore working behavior.
- Link to relevant spec sections when available. Omit the source field for conversation input.
- Do not prescribe implementation steps, code, or new detailed technical designs. Preserve established implementation constraints and architecture decisions that are required for the task. Include estimated file paths only as optional references.
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

## Updates and shared rules

- Before saving, check for an existing plan. Never overwrite a plan for unrelated work. Report the conflict and use another location only after the user resolves the conflict.
- Keep task completion status in `PLAN.md`. Mark a task done only after its acceptance criteria pass.
- Preserve completed task records and existing filenames. Add or revise unfinished tasks when requirements change.
- Do not repeat rules from `AGENTS.md` or other repository guidance in the plan or tasks. Include only feature-specific additions, explicit changes, or exceptions.
