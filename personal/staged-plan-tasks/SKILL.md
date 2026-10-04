---
name: staged-plan-tasks
description: Use when an effort is too large for a single plan — it delivers two or more focused end-to-end responsibilities, spans multiple agent runs, or cannot be implementation-planned up front because later work depends on earlier shipped outcomes. Captures the complete agreed outcome in one effort SPEC and coordinates delivery through a ROADMAP, then plans and ships each stage just in time. Offer it instead of a flat plan when sizing up multi-milestone work.
---

Plan and deliver an effort as small, single-responsibility end-to-end **stages**. A permanent `SPEC.md` holds the agreed outcome, a lean `ROADMAP.md` assigns it to stages, and the current stage gets a just-in-time `plan-tasks` tree. Use the shortest output that remains complete and unambiguous; expand only for genuine complexity.

# When to use

Use this skill for multiple responsibilities requiring a stage map, or work that needs just-in-time planning over multiple runs. Read [Stage decomposition](references/ROADMAPS.md#stage-decomposition) when sizing the effort; it owns stage definitions, boundaries, dependencies, and release prerequisites. One responsibility uses a standalone `plan-tasks` PLAN.

**Offer, do not impose.** When sizing up an effort that meets the bar, state the case — "this looks like N focused stages; I would stage it, or we can keep it one plan" — and let the user choose. The default is a single plan.

# Instructions

1. Read [`SPECS.md`](references/SPECS.md) when creating, revising, reviewing, or checking preservation of the effort SPEC, or assigning SPEC coverage to stages or tasks. It owns staged artifact ownership, ID traceability, retrieval scope, and semantic amendments; task execution follows the approved coverage pointers.
2. Read [`ROADMAPS.md`](references/ROADMAPS.md) when creating, revising, or resuming a ROADMAP. It defines the ROADMAP's content, stage-to-SPEC coverage map, formatting, leanness bar, and skeleton.
3. Deliver a stage with `plan-tasks` rooted at the stage directory. Apply the staged overlay below; required repository references complete its context, and sibling isolation still applies.
4. Create the effort SPEC and ROADMAP during initial decomposition. Map the current stage's tasks, then detail and review the next task, or the small approved concurrent set, using accepted results. Accept the assembled stage before detailing the next stage. Preserve existing agreed future plans through current contract references; do not discard their agreements when deferring detail. Future agreed outcomes remain in the SPEC and coverage map; only implementation detail is deferred.

# Artifacts

Resolve the layout from the nearest `AGENTS.md` first; it overrides the default below. Default, one tree per effort:

    docs/plans/<plan-slug>/
      SPEC.md                    # complete agreed outcome for the whole effort
      ROADMAP.md                 # stage coverage, order, status, decisions, and outcomes
      stages/
        01-<stage-slug>/
          PLAN.md                # current stage's delivery strategy; created just in time
          tasks/
            01-<task-slug>.md

Future stages remain ROADMAP entries until their planning begins.

Apply [Formatting](../plan-tasks/references/PLANS.md#formatting) to all staged artifacts.

# Staged overlay

`plan-tasks` is independently usable. This skill supplies its staged context and artifact additions:

- Link the SPEC and ROADMAP in the stage PLAN preamble. The SPEC owns agreed meaning; the PLAN owns the stage's implementation work under [Canonical ownership](references/SPECS.md#canonical-ownership).
- In PLAN `Progress`, append `Coverage` with each task's assigned normative and acceptance SPEC IDs and acceptance portions, including shared constraints wherever they apply. In `Validation and Acceptance`, reference SPEC scenarios instead of defining new acceptance IDs; add only implementation-specific validation.
- In task `Outcome and scope`, cite assigned normative and acceptance IDs and the task's assigned acceptance portions. In `Required contracts and dependencies`, reference the governing SPEC entries and their required contracts, invariants, terms, and decisions. Record acceptance IDs and evidence in `Acceptance and validation`.
- Assign task-boundary validation and implementation-specific cross-task checks to task Result gates. Assign the complete assembled-stage demonstration to the Stage gate. A PLAN's `complete` state records accepted task delivery; stage acceptance is recorded separately in the ROADMAP.
- Add the ROADMAP and phase-appropriate SPEC entries to task context as defined below. SPEC ID retirement and semantic changes follow [Stable IDs and traceability](references/SPECS.md#stable-ids-and-traceability) and [Lifecycle](references/SPECS.md#lifecycle).

# Context isolation across stages

A stage is to the ROADMAP what a task is to a PLAN — the same isolation, one level up:

- During initial decomposition, inspect every discovery source needed to capture the agreement, then create the SPEC and ROADMAP. After the Roadmap/Spec gate, transcripts, chats, and scratch notes are no longer execution dependencies.
- **Stage decomposition:** load the ROADMAP and every SPEC entry assigned to the stage, following referenced contracts, invariants, and necessary glossary entries. Resolve covered open questions by their latest safe gate before decomposing affected tasks.
- **Task planning and execution:** retrieve the ROADMAP's current state/dependency entry, the stage PLAN, current task when it exists, and that task's assigned SPEC entries. Follow referenced contracts and invariants and load necessary glossary entries. Explicitly assign shared constraints to every applicable task; stage membership alone does not imply task coverage. Keep sibling task and stage trees closed.
- **Stage acceptance:** retrieve complete stage coverage and check evidence against every assigned obligation and acceptance portion under [Stable IDs and traceability](references/SPECS.md#stable-ids-and-traceability). Narrow task retrieval preserves the full traceability map and leaves no stage obligation unassigned.
- When recording or promoting a decision or discovery, use [Canonical ownership](references/SPECS.md#canonical-ownership). Before compaction, follow [History and preservation](references/SPECS.md#history-and-preservation).
- Reopen a sibling stage's files only when its recorded outcome or implementation contract stops holding and the ROADMAP does not contain enough evidence to recover.
- Keep the ROADMAP lean. The SPEC carries the agreed what; stage plans carry implementation detail. The ROADMAP carries only what a context-blind agent needs to understand delivery, select the next stage, and retrieve its SPEC coverage.

# Flow

Specify the complete effort, map it to stages, then plan and ship each stage just in time. Initial, amendment, and delivery gates surround `plan-tasks`'s Map, Plan, and Result gates. Every gate is a hard stop for explicit user approval.

1. **Specify and decompose.** Inspect the repository and the full discovery record. Write `SPEC.md` following `SPECS.md`, then write `ROADMAP.md` following `ROADMAPS.md`. Create no PLAN or task files yet.

   Before the gate, complete [Stage decomposition](references/ROADMAPS.md#stage-decomposition) and the [SPEC completeness bar](references/SPECS.md#completeness-bar). Then audit the stage coverage map:

   - Every normative and acceptance ID is assigned to at least one ROADMAP stage or to existing behavior that a named stage will validate. Check shared acceptance portions and final ownership against [Stable IDs and traceability](references/SPECS.md#stable-ids-and-traceability).
   - Every open-question ID appears in the Coverage of each stage whose planning or implementation its answer could affect. Its latest safe gate is no later than the earliest affected stage's Map gate.
   - No stage depends on reopening a transcript, chat, scratch note, or sibling stage tree.

   → **Roadmap/Spec gate.** Set `awaiting-roadmap-spec-review`; present the agreed outcome, stage breakdown and order, ID coverage, open questions, and traceability result. Wait for approval before setting the first stage to `ready-to-plan`.

2. **Plan and ship the current stage.** Use complete stage coverage for decomposition; resolve open questions whose latest safe gate has arrived through the Spec amendment gate. Apply `plan-tasks` rooted at `stages/NN-slug/`; it owns task sequencing and gates. Proposed concurrent tasks must pass [Parallel execution](../plan-tasks/references/PLANS.md#parallel-execution). Before the Map gate, audit that every stage-assigned normative ID and acceptance portion has task coverage, including all applicable shared constraints, and that each task's context pointers reach its governing agreements. PLANs and tasks cite IDs instead of copying prose. Fill the ROADMAP's `Plan:` pointer and update its explicit state as work advances.
   → **Stage gate.** Once the PLAN is `complete`, set the ROADMAP to `awaiting-stage-review`. Retrieve complete stage coverage, demonstrate the milestone, and present evidence for every assigned obligation and acceptance portion. Wait for acceptance or revision before checking the stage's box. On acceptance, record a short handoff of shipped contracts and evidence references needed later; reassign unchanged SPEC IDs among unstarted stages if approved. Keep shipped coverage and evidence fixed, record delivery decisions with rationale, set the next stage to `ready-to-plan` (or the effort to `complete`), and recommend a fresh conversation for the next stage.

3. **Amend when necessary.** Stop as soon as the approved artifacts no longer describe the intended work.

   - For a delivery-only change outside a Stage gate, update stage boundaries, order, dependencies, or assignment of unchanged SPEC IDs in the ROADMAP. Set `awaiting-roadmap-amendment-review` and record the state to resume after approval.
     → **Roadmap amendment gate.** Present the delivery change and rationale. Wait for approval before entering a Map gate or resuming implementation.
   - For a semantic change to accepted behavior, constraints, contracts, invariants, or acceptance, update the SPEC according to its lifecycle rules and update ROADMAP coverage when delivery also changes. Set `awaiting-spec-amendment-review` and record the state to resume after approval.
     → **Spec amendment gate.** Present the exact semantic change, rationale, affected IDs, acceptance impact, and delivery impact. Wait for approval before entering a Map gate or resuming implementation.

Execute only the current stage. Reallocate unchanged work only at a Stage or Roadmap amendment gate, and change the agreed outcome only at a Spec amendment gate. A PLAN or task may not silently override the SPEC.

# Resuming

Read the ROADMAP's `Current stage`, `State`, and `Remaining`. If it is `working-stage`, resume the named PLAN using its explicit task state and task-level SPEC coverage. If `ready-to-plan`, retrieve complete stage coverage for decomposition when authorized to continue. If `awaiting-stage-review`, load complete stage coverage and the evidence references for review; implementation approval is not inferred from an unchecked stage. Pending initial or amendment gates remain pending, and recorded approvals persist. For legacy artifacts, establish and write the exact state from recorded approvals and evidence; ask only when approval cannot be established. Keep sibling stage trees closed unless their recorded outcome or contract fails.

# Gate discipline

State plainly which gate is active and what requires approval. Keep the Roadmap/Spec gate, Roadmap amendment gate, Spec amendment gate, each stage's internal gates, and the Stage gate as separate sign-offs. The initial gate approves the agreement and initial delivery mapping; a Roadmap amendment gate approves delivery-only changes made between Stage gates; a Spec amendment gate approves semantic changes; a Stage gate approves demonstrated delivery and may also reallocate unchanged future work.

Gate messages are concise: name the gate, summarize only decisions, changes, risks, coverage gaps, open questions, or evidence needed for review, and ask for the specific approval. Do not restate the artifacts, narrate routine work, add generic preambles, or pad a simple answer. A one-line gate message is sufficient when no complexity needs explanation.
