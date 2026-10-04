---
name: plan-tasks
description: Plan, review, execute, or continue complex coding work for one responsibility from start to end. Write tasks with clear boundaries. Prepare each task before execution, with separate approvals for the map, plan, and result. Use for small local fixes only on explicit request.
---

Plan and deliver work as a sequence of **tasks**. Give each task a result with its own review.

# Instructions

Use [ste-writing-skill](../ste-writing-skill/SKILL.md) for all explanations, approval requests, review reports, documentation, comments, and user-facing text.

To create, revise, validate, execute, or continue a plan, read [`PLANS.md`](references/PLANS.md). It gives rules for tasks, decomposition, context ownership, preservation, concurrency, task size, and resume states. This skill gives rules for the procedure and approval gates.

To write or restructure the parent plan, load [`PLAN-SKELETON.md`](references/PLAN-SKELETON.md). To detail or restructure a task, load [`TASK-SKELETON.md`](references/TASK-SKELETON.md). For execution, use the approved task brief and `PLANS.md`. Load templates only when the structure must change.

# Artifacts

For all planning artifacts, use [Formatting](references/PLANS.md#formatting).

First, get the document layout from the nearest applicable `AGENTS.md`. Its instructions override the default layout. The default has one tree per feature:

    docs/plans/<plan-slug>/
      PLAN.md            # parent plan
      tasks/
        01-backend.md    # task with a clear implementation boundary
        02-frontend.md

# Context isolation

Use [Current context and ownership](references/PLANS.md#current-context-and-ownership) to select task context and move shared knowledge to its canonical location. Before you make a document shorter, use [Current instructions and history](references/PLANS.md#current-instructions-and-history). Complete its preservation check.

# Flow

First, map all tasks. Then prepare the current task brief. Get plan approval. Implement the task. Get result acceptance. Use accepted predecessor results to detail the next task. At each gate, stop for explicit approval. Keep earlier approvals valid when you continue work.

1. **Decompose.** Examine the repository. Write `PLAN.md`. Before map approval, complete the checks in [Discovery capture](references/PLANS.md#discovery-capture), [Decomposition](references/PLANS.md#decomposition), and [Task map](references/PLANS.md#task-map). Keep future tasks as map entries until their turn. Set the state to `awaiting-map-review`.

   **Map gate.** Show the task breakdown. Show the discovery capture check result. Wait for approval of the tasks and their order before you detail a task.

2. **Detail the current task.** After map approval, set the state to `detailing`. Retrieve the agreements mapped to the current task. Use [Discovery capture](references/PLANS.md#discovery-capture). Write `tasks/NN-slug.md` as a short execution brief. For proposed concurrent work, detail only that small set. Use accepted predecessor contracts and the current repository. Use the task-size check in `PLANS.md`. Agree the behavioral test seams. Write the remaining implementation work. Set the state to `awaiting-plan-review`.

   **Plan gate.** Show the task plan and the scope-review conclusion, if applicable. Get answers for open decisions. Wait for approval before you change source for this task. After approval, set the state to `implementing`.

3. **Implement and review the current task.** Make only the approved task changes. Use TDD and behavioral acceptance. Keep status and remaining work current. For each acceptance ID, write the latest applicable validation evidence. Include full commands, observed results, and the tested revision. Set the state to `awaiting-result-review`. Keep its PLAN checkbox unchecked.

   **Result gate.** Report the completed behavior, important findings, and validation evidence. Wait for acceptance or a revision request.

   For requested changes, set the state to `reopened`. Complete the requested work. Go to this gate again with current evidence.

   After acceptance, set the task state to `accepted`. Identify the task as completed. Set its PLAN checkbox to checked. Write a short PLAN handoff with only the contracts and evidence references necessary for dependent tasks.

   Set the next task to `ready-to-detail`. When all results have acceptance and no planned work is unfinished, set the plan state to `complete`. Set `Current task: none`.

   Recommend a new conversation for the next task. Do the procedure again from step 2 when the user authorizes continuation.

Do only work for the approved current task or concurrent set. Get an explicit instruction before you continue after a gate, increase scope, or prepare the next task brief. If scope or design has an important change during a task, stop. Change the plan before you continue.

# Parallel execution

Before you propose or execute a concurrent set, use [Parallel execution](references/PLANS.md#parallel-execution). Each task must pass its own Plan and Result gates.

# Resuming

Read the root `PLAN.md`. Read its `Current task`, `State`, and `Remaining` fields. Use the `PLANS.md` state definitions to select detailing, implementation, approval, or reopened result work.

Open only the named task, if its file exists, and necessary references. Keep recorded approvals valid. Keep sibling files closed unless a contract changes.

If an earlier plan has no state, compare recorded approvals with current evidence. Write the correct state. Get the user's decision only when you cannot find the applicable approval. An unchecked box alone does not authorize implementation.

# Gate discipline

At a gate, stop. Write the active gate and the necessary approval. Keep task map, task plan, and task result approvals separate.

Write current assumptions and resolved decisions at their canonical scope. Include reasons only when they change implementation or prevent a possible mistake.

If a change makes the approved map invalid, change the map. Go to the Map gate again before more detail or implementation.

Keep gate messages short. Identify the gate. Give only the decisions, changes, risks, or evidence necessary for review. Tell the user which approval is necessary. Use one line when no more explanation is necessary for review.
