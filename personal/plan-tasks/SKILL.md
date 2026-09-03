---
name: plan-tasks
description: Use when planning, reviewing, or executing any non-trivial coding work — multi-file features, risky refactors, migrations, architecture changes. Decomposes the effort into sequential child tasks, all planned before any are implemented (a later task's plan may depend on an earlier task's planned changes), with stop-and-review gates between decomposition, each task's plan, and each task's result. Not for small localized fixes unless explicitly requested.
---

Plan and deliver an effort as a sequence of independently-reviewable **tasks**. Use the shortest output that remains complete and unambiguous; add detail only when the work's complexity requires it.

# Instructions
1. Read [`PLANS.md`](references/PLANS.md) when creating, revising, validating, or executing an executable plan; it defines plan and task content, formatting, and method. Load the structural template for the artifact in hand: [`PLAN-SKELETON.md`](references/PLAN-SKELETON.md) when authoring or revising the parent plan, [`TASK-SKELETON.md`](references/TASK-SKELETON.md) when detailing or executing a task.
2. Each task is detailed and executed one at a time, stopping at a gate for user review between each.
3. Another task's file is loaded only when a **contract** changes (see Context isolation).

# Artifacts

Resolve the planning artifact layout from the nearest applicable `AGENTS.md` first; it overrides the default below. Default layout, one tree per feature:

    docs/plans/<plan-slug>/
      PLAN.md            # parent plan
      tasks/
        01-config.md     # child tasks
        02-prisma.md

Write every filesystem path in every planning artifact relative to the repository root. This applies to PLANs, tasks, commands, working directories, examples, logs, and evidence; absolute paths never appear in these artifacts.

Use the current git username as author where a section needs one. Treat these as public documents: no secrets.

# Context isolation

This is the point of the skill. Hold the minimum in context:

- When working on a task, load the root `PLAN.md` and that task's file **only**. Never load a sibling task's file — task 02 must not pull task 01's rationale into context.
- Cross-task influence flows **only through the parent plan's `Decision Log`**, never by reading a sibling task. When a task-local decision affects another task, *promote* it from the task file up to the `Decision Log`; the next task reads it there. This is how a later task's plan depends on an earlier task's planned changes without loading the earlier task.
- *Promotion* covers any cross-cutting entry the same way — a `Decision Log` decision or a `Surprises & Discoveries` observation that outlives its task. The entry keeps one canonical home (the highest scope that consumes it); the originating task replaces it with a one-line pointer back. Interface signatures follow the same fan-out rule: shared/cross-stage contracts in the parent, single-consumer contracts in the source task. Never paste the same text in both.
- Reopen a sibling task file only when a **contract** changes — a contract being a task's promised interfaces, types, or outcomes that another task relies on (e.g. a plan revision, new requirement, or scope change), or when a described outcome does not work as expected.
- Keep the parent plan lean. Detail belongs in task files; the parent plan holds only what every task genuinely needs.

# Flow

Decompose first, then detail every task, and finally execute the tasks one at a time. **All task files are detailed and Plan-gated before any source is touched**, because a later task's plan may depend on an earlier task's planned changes. Three gate types; at every gate, stop and wait for an explicit instruction to continue.

1. **Decompose.** Inspect the repository, then write the `PLAN.md` following `PLANS.md`. Split into **vertical capabilities, never horizontal layers** — each task the smallest end-to-end slice that yields observable behavior, owning its own content across every layer it touches (see `PLANS.md`, `## Tasks`). Add each task as a title, a one-line scope, and an unchecked status box. Do not detail tasks yet.
   → **Map gate.** Present the breakdown and wait for approval of the tasks and their order before detailing anything.

2. **Detail every task.** Write `tasks/NN-slug.md` in full: task-specific details following `PLANS.md`, leave progress section empty. Touch no source files.
   → **Plan gate.** Present the task plan. This is the moment to review or grill it. Wait for approval. Source is never modified before this gate passes. Once approved, move to detailing the next task on the list. Repeat until every task is detailed; only then begin execution.

3. **Execute every task, one at a time.** Execute the next unchecked task: make the changes and keep the task's live sections current as you go.
   → **Result gate.** Report which task completed, what changed, surprises, and **validation evidence** — the exact commands or tests run and their output, proving the task works (not merely that code compiles). Update the task's progress section, the parent plan's progress section, and any decisions or observations — promote cross-cutting ones to the parent plan and leave a one-line pointer in the task, never a full duplicate. Name the next task. Wait before executing it.

Execute only the current task. Never cross a gate, expand scope, or detail the next task without an explicit instruction to continue. If scope or design changes materially mid-task, stop and revise the plan rather than pressing on.

# Resuming

Read the root `PLAN.md`; the first unchecked box in plan's progress is the next task. Open that one task file and continue from its progress. Read no other task files unless a **contract** changes (see Context isolation).

# Gate discipline

A gate is a hard stop. At each one, state plainly which gate you are at and what you need approved. Do not bundle approvals — task list, each task's plan, and each task's result are separate sign-offs. Record assumptions and resolved questions in the appropriate decision log section (parent plan if cross-cutting, task if local) as they are settled, with rationale.

Gate messages are concise: name the gate, summarize only the decisions, changes, risks, or evidence needed for review, and ask for the specific approval. Do not restate the artifact, narrate routine work, add generic preambles, or pad a simple answer. A one-line gate message is sufficient when no complexity needs explanation.
