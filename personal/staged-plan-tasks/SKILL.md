---
name: staged-plan-tasks
description: Plan work that is too large for one plan. Use for multiple responsibilities, multiple agent runs, or future work that depends on earlier delivered results. Keep the full agreement in a SPEC. Control delivery through a ROADMAP. Offer staged planning for work with multiple milestones.
---

Plan and deliver work as small **stages**. Each stage delivers one responsibility from start to end. A permanent `SPEC.md` holds the agreed outcome. A short `ROADMAP.md` gives that outcome to stages. Prepare a `plan-tasks` tree when necessary for the current stage.

# When to use

Use this skill when a stage map is necessary for multiple responsibilities. Also use it when planning is necessary across multiple runs as results become available. To find the work size, read [Stage decomposition](references/ROADMAPS.md#stage-decomposition). It gives rules for stages, boundaries, dependencies, and release prerequisites. For one responsibility, use a standalone `plan-tasks` PLAN.

**Offer staged planning to the user.** Explain why stages can help. For example: "This work has N focused stages. I recommend stages. You can also choose one plan." Let the user choose. Use a single plan by default.

# Instructions

Use [ste-writing-skill](../ste-writing-skill/SKILL.md) for all explanations, approval requests, review reports, documentation, comments, and user-facing text.

- To create, revise, review, or keep the effort SPEC, read [`SPECS.md`](references/SPECS.md). Also read it to give SPEC coverage to stages or tasks. It gives rules for document ownership, ID traceability, retrieval scope, and changes to agreed meaning. During task execution, use the approved coverage references.
- To create, revise, or continue a ROADMAP, read [`ROADMAPS.md`](references/ROADMAPS.md). It gives rules for ROADMAP content, stage-to-SPEC coverage, formatting, size, and the skeleton.
- To deliver a stage, use `plan-tasks` at the stage directory. Use the staged additions below. Load necessary repository references. Keep sibling files closed with the context rules.
- During initial decomposition, create the effort SPEC and ROADMAP. Map the current stage's tasks. Use accepted results to detail and review the next task or small approved concurrent set.
- Get acceptance of the assembled stage before you detail the next stage. Keep existing future agreements through references to current contracts. Keep agreed future outcomes in the SPEC and coverage map. Prepare their implementation detail when needed.

# Artifacts

First, get the layout from the nearest applicable `AGENTS.md`. Its instructions override the default layout. The default has one tree per effort:

    docs/plans/<plan-slug>/
      SPEC.md                    # full agreed outcome for the effort
      ROADMAP.md                 # stage coverage, order, status, decisions, and outcomes
      stages/
        01-<stage-slug>/
          PLAN.md                # stage delivery plan, prepared when needed
          tasks/
            01-<task-slug>.md

Keep future stages as ROADMAP entries until their planning starts.

For all staged artifacts, use [Formatting](../plan-tasks/references/PLANS.md#formatting).
This includes SPECs, ROADMAPs, stage PLANs, task briefs, handoffs, history records, and supporting planning documents.

# Staged overlay

Use `plan-tasks` for standalone work. For staged work, add this context and these fields:

- Add SPEC and ROADMAP references to the stage PLAN introduction. The SPEC owns agreed meaning. The PLAN owns stage implementation with [Canonical ownership](references/SPECS.md#canonical-ownership).
- In PLAN `Progress`, add `Coverage`. Give each task's assigned normative and acceptance SPEC IDs and acceptance portions. Include shared constraints in each applicable task.
- In `Validation and Acceptance`, refer to SPEC scenarios. Keep acceptance IDs in the SPEC. Add only implementation-specific validation.
- In task `Outcome and scope`, cite assigned normative and acceptance IDs. Identify the task's assigned acceptance portions.
- In `Required contracts and dependencies`, refer to applicable SPEC entries, contracts, invariants, terms, and decisions. In `Acceptance and validation`, write acceptance IDs and evidence.
- Give task-boundary validation and implementation checks across tasks to task Result gates. Give the full assembled-stage demonstration to the Stage gate. PLAN state `complete` means all task results have acceptance. Write stage acceptance in the ROADMAP as a separate approval.
- Add the ROADMAP and applicable SPEC entries to task context as specified below. For SPEC ID retirement, use [Stable IDs and traceability](references/SPECS.md#stable-ids-and-traceability). For changes to meaning, use [Lifecycle](references/SPECS.md#lifecycle).

# Context isolation across stages

Use the same context isolation between ROADMAP stages as between PLAN tasks:

- **Initial decomposition:** examine each discovery source necessary to capture the agreement. Create the SPEC and ROADMAP. After Roadmap/Spec approval, use the approved documents as execution references. Keep transcripts, chats, and scratch notes outside execution dependencies.
- **Stage decomposition:** load the ROADMAP and each SPEC entry assigned to the stage. Use referenced contracts and invariants. Load necessary glossary entries. Get answers for applicable open questions by their latest safe gate before you decompose affected tasks.
- **Task planning and execution:** load the ROADMAP's current state and dependency entry. Load the stage PLAN and current task, if it exists. Load the task's assigned SPEC entries, referenced contracts and invariants, and necessary glossary entries. Give shared constraints to each applicable task. Stage membership alone does not establish task coverage. Keep sibling task and stage trees closed.
- **Stage acceptance:** load full stage coverage. Compare evidence with each assigned obligation and acceptance portion with [Stable IDs and traceability](references/SPECS.md#stable-ids-and-traceability). Keep the full traceability map when you load only task context. Give each stage obligation to tasks.
- To write or move a decision or finding, use [Canonical ownership](references/SPECS.md#canonical-ownership). Before you make documents shorter, use [History and preservation](references/SPECS.md#history-and-preservation).
- If a sibling stage outcome or implementation contract fails, first examine ROADMAP evidence. Reopen its files only if that evidence is insufficient.
- Keep the ROADMAP short. Keep the agreed outcome in the SPEC. Keep implementation detail in stage plans. Include enough ROADMAP context for an agent without conversation history to understand delivery and select the next stage. Include direct references to that stage's SPEC coverage.

# Flow

Specify the full effort. Map it to stages. Plan and deliver each stage when its turn starts. Use the initial, amendment, and delivery gates around the Map, Plan, and Result gates in `plan-tasks`. At each gate, stop for explicit user approval.

1. **Specify and decompose.** Examine the repository. Read the full discovery record. Write `SPEC.md` with the rules in `SPECS.md`. Write `ROADMAP.md` with the rules in `ROADMAPS.md`. Keep PLAN and task files for later planning.

   Before the gate, complete [Stage decomposition](references/ROADMAPS.md#stage-decomposition). Meet the [SPEC completeness bar](references/SPECS.md#completeness-bar). Audit the stage coverage map against these conditions:

   - Each normative and acceptance ID has at least one ROADMAP stage assigned. Existing behavior can supply coverage if a named stage validates it. Use [Stable IDs and traceability](references/SPECS.md#stable-ids-and-traceability) for shared acceptance portions and final ownership.
   - Each open-question ID appears in each stage whose planning or implementation its answer can affect. Its latest safe gate is at or before the earliest affected stage's Map gate.
   - Each stage can proceed without transcripts, chats, scratch notes, or sibling stage trees.

   **Roadmap/Spec gate.** Set the state to `awaiting-roadmap-spec-review`. Show the agreed outcome, stage breakdown, order, ID coverage, open questions, and traceability result. Wait for approval before you set the first stage to `ready-to-plan`.

2. **Plan and deliver the current stage.** Use full stage coverage for decomposition. Get answers for open questions through the Spec amendment gate when their latest safe gate arrives. Use `plan-tasks` at `stages/NN-slug/`. Use its task sequence and gates.

   For proposed concurrent tasks, use [Parallel execution](../plan-tasks/references/PLANS.md#parallel-execution). Before the Map gate, audit task coverage for each assigned normative ID and acceptance portion. Include all applicable shared constraints. Make sure each task's context references reach its applicable agreements.

   Cite IDs in PLANs and tasks. Keep their definitions in the SPEC. Write the ROADMAP's `Plan:` reference. Keep its state current as work proceeds.

   **Stage gate.** When the PLAN state is `complete`, set the ROADMAP state to `awaiting-stage-review`. Load full stage coverage. Demonstrate the milestone. Show evidence for each assigned obligation and acceptance portion. Wait for acceptance or revision before you set the stage's box to checked.

   After acceptance, write a short handoff. Include delivered contracts and evidence references necessary for future work. With approval, reassign unchanged SPEC IDs among stages that have not started. Keep delivered coverage and evidence fixed. Write delivery decisions and their reasons.

   Set the next stage to `ready-to-plan`, or set the effort to `complete`. Recommend a new conversation for the next stage.

3. **Amend when necessary.** If approved documents no longer describe the intended work, stop.

   - **Delivery-only change outside a Stage gate:** update ROADMAP boundaries, order, dependencies, or assignment of unchanged SPEC IDs. Set the state to `awaiting-roadmap-amendment-review`. Write the state to resume after approval.

     **Roadmap amendment gate.** Show the delivery change and its reason. Wait for approval before you enter a Map gate or continue implementation.

   - **Semantic change:** update the SPEC for changes to accepted behavior, constraints, contracts, invariants, or acceptance. Use the SPEC lifecycle rules. If delivery also changes, update ROADMAP coverage. Set the state to `awaiting-spec-amendment-review`. Write the state to resume after approval.

     **Spec amendment gate.** Show the full change to meaning and its reason. Identify affected IDs and effects on acceptance and delivery. Wait for approval before you enter a Map gate or continue implementation.

Do only work for the current stage. Reassign unchanged work only at a Stage or Roadmap amendment gate. Change the agreed outcome only at a Spec amendment gate. Keep PLANs and tasks consistent with the SPEC.

# Resuming

Read the ROADMAP's `Current stage`, `State`, and `Remaining` fields. Select the applicable action:

- `working-stage`: continue the named PLAN from its task state and task-level SPEC coverage.
- `ready-to-plan`: load full stage coverage for decomposition when the user authorizes continuation.
- `awaiting-stage-review`: load full stage coverage and evidence references for review. An unchecked stage box does not authorize implementation.
- Initial or amendment gate pending: keep the gate pending.
- Recorded approval: keep the approval valid.

For earlier documents, find the correct state from recorded approvals and evidence. Write that state. Get the user's decision only when you cannot find approval. Keep sibling stage trees closed unless their recorded outcome or contract fails.

# Gate discipline

Write the active gate and necessary approval. Keep all approval types separate:

| Gate | Approval scope |
| --- | --- |
| Roadmap/Spec | The initial agreement and delivery map. |
| Roadmap amendment | Delivery-only changes between Stage gates. |
| Spec amendment | Changes to agreed meaning. |
| Map, Plan, Result | The current stage's internal task gates, with `plan-tasks`. |
| Stage | Demonstrated delivery. This gate can also reassign unchanged future work. |

Keep gate messages short. Identify the gate. Give only decisions, changes, risks, coverage gaps, open questions, or evidence necessary for review. Tell the user which approval is necessary. Use one line when no more explanation is necessary for review.
