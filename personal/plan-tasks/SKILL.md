---
name: plan-tasks
description: Plan, review, execute, or resume non-trivial coding work within one end-to-end responsibility. Map bounded implementation tasks, then detail and implement just in time with separate map, plan, and result approvals. Not for small localized fixes unless explicitly requested.
---

Plan and deliver an effort as a sequence of independently-reviewable **tasks**. Use the shortest output that remains complete and unambiguous; add detail only when the work's complexity requires it.

# Instructions

Read [`PLANS.md`](references/PLANS.md) when creating, revising, validating, executing, or resuming a plan; it owns task definitions, decomposition, context ownership, preservation, concurrency, task size, and resume states. This skill owns the flow and gates below. Load [`PLAN-SKELETON.md`](references/PLAN-SKELETON.md) when authoring or restructuring the parent plan, or [`TASK-SKELETON.md`](references/TASK-SKELETON.md) when detailing or restructuring a task. Execution uses the approved brief and `PLANS.md`; templates are needed only when its structure must change.

# Artifacts

Resolve the planning artifact layout from the nearest applicable `AGENTS.md` first; it overrides the default below. Default layout, one tree per feature:

    docs/plans/<plan-slug>/
      PLAN.md            # parent plan
      tasks/
        01-backend.md    # bounded implementation tasks
        02-frontend.md

# Context isolation

Use [Current context and ownership](references/PLANS.md#current-context-and-ownership) to select task context and promote shared knowledge. Before compacting any artifact, follow [Current instructions and history](references/PLANS.md#current-instructions-and-history) and complete its preservation check.

# Flow

Map the plan's tasks, then detail → approve → implement → review the next task just in time. Detail the next task using the accepted result of its predecessors. Three gate types; at every gate, stop and wait for explicit approval. Prior approvals persist on resume.

1. **Decompose.** Inspect the repository, then write `PLAN.md`. Complete [Decomposition](references/PLANS.md#decomposition) and the [Task map](references/PLANS.md#task-map) coverage before map approval. Future tasks remain map entries, without detailed task files. Set state to `awaiting-map-review`.
   → **Map gate.** Present the breakdown and wait for approval of the tasks and their order before detailing anything.

2. **Detail the current task.** After map approval, set state to `detailing` and write `tasks/NN-slug.md` as a compact execution brief, or detail only the small set proposed for concurrent work. Use accepted predecessor contracts and the current repository. Apply the task-size check in `PLANS.md`, agree the behavioral test seams, and record the remaining implementation work. Set state to `awaiting-plan-review`.
   → **Plan gate.** Present this task's plan and any scope-review conclusion. Resolve unsettled decisions, then wait for approval before modifying source for this task. Approval moves it to `implementing`.

3. **Implement and review the current task.** Make only its approved changes, use TDD and behavioral acceptance, and keep its status and remaining work current. Record the latest relevant validation against each acceptance ID; include the exact commands, observed results, and tested revision. Set state to `awaiting-result-review`; its PLAN checkbox remains unchecked.
   → **Result gate.** Report the completed behavior, material discoveries, and validation evidence. Wait for acceptance or revision. Requested follow-up moves it to `reopened`; after addressing it, return to this gate with current evidence. Acceptance sets its state to `accepted`, marks the task complete and its PLAN checkbox checked. Promote only the contracts and evidence pointers later tasks need into a short PLAN handoff. Set the next task to `ready-to-detail`. When all task results are accepted and no planned work remains, set the plan to `complete` and `Current task: none`. Recommend starting the next task in a fresh conversation, then repeat from step 2 when authorized to continue.

Execute only the approved current task or concurrent set. Never cross a gate, expand scope, or detail the next task without an explicit instruction to continue. If scope or design changes materially mid-task, stop and revise the plan rather than pressing on.

# Parallel execution

Before proposing or executing a concurrent set, apply [Parallel execution](references/PLANS.md#parallel-execution). Each task still passes its own Plan and Result gates.

# Resuming

Read the root `PLAN.md` and its `Current task`, `State`, and `Remaining` fields. Use the state definitions in `PLANS.md` to distinguish detailing, implementation, pending approval, and reopened result work. Open only the named task when its file exists, plus required references. An approval already recorded remains valid. If a legacy plan lacks state, reconcile its recorded approvals and current evidence, write the exact state, and ask only when the governing approval cannot be established; an unchecked box alone does not authorize implementation. Keep sibling files closed unless a contract changes.

# Gate discipline

A gate is a hard stop. State which gate is active and what needs approval. Task map, each task's plan, and each task's result are separate sign-offs. Record current assumptions and resolved decisions at their canonical scope, with rationale only when it changes implementation or prevents a likely mistake. If a change invalidates the approved map, revise it and return to the Map gate before further detail or implementation.

Gate messages are concise: name the gate, summarize only the decisions, changes, risks, or evidence needed for review, and ask for the specific approval. Do not restate the artifact, narrate routine work, add generic preambles, or pad a simple answer. A one-line gate message is sufficient when no complexity needs explanation.
