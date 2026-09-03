---
name: staged-plan-tasks
description: Use when an effort is too large for a single plan — it delivers two or more sequential, independently shippable milestones, spans multiple agent runs, or cannot be implementation-planned up front because later work depends on earlier shipped outcomes. Captures the complete agreed outcome in one effort SPEC and coordinates delivery through a ROADMAP, then plans and ships each stage just in time. Offer it instead of a flat plan when sizing up multi-milestone work.
---

Plan and deliver a large effort as independently-shippable **stages**. A permanent `SPEC.md` holds the agreed outcome, a lean `ROADMAP.md` assigns it to stages, and the current stage gets a just-in-time `plan-tasks` tree. Use the shortest output that remains complete and unambiguous; expand only for genuine complexity.

# When to use

A **stage** is a milestone: a vertical slice that ends in demonstrable, observable behavior a human can run, not a horizontal layer. The vertical-capability rule governing tasks governs stages one level up — a stage delivers a capability end-to-end and never a layer pre-built for later stages; the mechanism-vs-content distinction and walking-skeleton fallback in `plan-tasks`'s `PLANS.md` (`## Tasks`) apply here at stage granularity. Reach for this skill only when the effort spans **two or more sequential milestones** — a later one building on an earlier *shipped* one — or is too large to detail at once because later stages depend on outcomes you will not know until earlier stages ship. One milestone is a flat `plan-tasks` plan, not a roadmap.

**Offer, do not impose.** When sizing up an effort that meets the bar, state the case — "this looks like N milestones; I would stage it, or we can keep it one plan" — and let the user choose. The default is a single plan.

# Instructions

1. Read [`SPECS.md`](references/SPECS.md) when creating, revising, reviewing, or consuming the effort SPEC. It defines the SPEC's ownership, traceability model, lifecycle, formatting, and template.
2. Read [`ROADMAPS.md`](references/ROADMAPS.md) when creating, revising, or resuming a ROADMAP. It defines the ROADMAP's content, stage-to-SPEC coverage map, formatting, leanness bar, and skeleton.
3. Deliver a stage with the `plan-tasks` skill rooted at the stage directory. For a staged effort, this skill explicitly replaces `plan-tasks`'s standalone PLAN-and-current-task context boundary: the required execution context is the ROADMAP, the stage-assigned SPEC entries, the stage PLAN, and the current task. Those four artifacts together satisfy `plan-tasks`'s self-containment rule; sibling-task and sibling-stage isolation and all other `plan-tasks` rules still apply. Keep `plan-tasks` generic: this skill alone overlays specification traceability by linking the governing SPEC and ROADMAP in the PLAN preamble, appending assigned normative and acceptance IDs to each task in PLAN `Progress`, citing normative IDs in task `Purpose`, and citing acceptance IDs in task `Validation / Acceptance`.
4. Create the effort SPEC and ROADMAP during initial decomposition. Plan and execute implementation just in time: one stage is fully planned and shipped before the next stage's PLAN or tasks are created.

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
        02-<stage-slug>/
          ...

Write every filesystem path in every staged-planning artifact relative to the repository root. This applies to SPECs, ROADMAPs, stage PLANs, tasks, commands, working directories, examples, logs, and evidence; absolute paths never appear in these artifacts.

Use the current git username as author where a section needs one. Treat these as public documents: no secrets.

# Context isolation across stages

A stage is to the ROADMAP what a task is to a PLAN — the same isolation, one level up:

- During initial decomposition, inspect every discovery source needed to capture the agreement, then create the SPEC and ROADMAP. After the Roadmap/Spec gate, transcripts, chats, and scratch notes are no longer execution dependencies.
- When working a stage, load the ROADMAP, the stage's PLAN and current task when they exist, and the SPEC entries named by the stage's `Coverage` field. Follow pointers from those entries to shared SPEC terms or contracts as needed. Resolve covered open questions by their latest safe gate before decomposing affected tasks. Keep sibling stage trees closed.
- Accepted behavior, constraints, contracts, invariants, acceptance scenarios, and unresolved product questions live in the SPEC. Stage assignment, order, dependencies, delivery decisions, status, and shipped outcomes live in the ROADMAP. Shared implementation strategy lives in the stage PLAN; task-local implementation detail lives in the task.
- A decision or discovery keeps one canonical home. Promote cross-task implementation knowledge to the PLAN, cross-stage delivery knowledge to the ROADMAP, and proposed changes to the agreed outcome to the SPEC through the Spec amendment gate. Lower artifacts retain only stable-ID pointers.
- Reopen a sibling stage's files only when its recorded outcome or implementation contract stops holding and the ROADMAP does not contain enough evidence to recover.
- Keep the ROADMAP lean. The SPEC carries the agreed what; stage plans carry implementation detail. The ROADMAP carries only what a context-blind agent needs to understand delivery, select the next stage, and retrieve its SPEC coverage.

# Flow

Specify the complete effort, map it to stages, then plan and ship each stage just in time. Initial, amendment, and delivery gates surround `plan-tasks`'s Map, Plan, and Result gates. Every gate is a hard stop for explicit user approval.

1. **Specify and decompose.** Inspect the repository and the full discovery record. Write `SPEC.md` following `SPECS.md`, then write `ROADMAP.md` following `ROADMAPS.md`. Create no PLAN or task files yet.

   Before the gate, perform a traceability audit:

   - Every accepted behavior, constraint, contract, invariant, and unresolved product question has exactly one canonical home in the SPEC; delivery-only decisions have one canonical home in the ROADMAP.
   - Every normative SPEC ID (`R`, `C`, or `I`) is covered by at least one acceptance ID (`A`); when direct behavioral observation is impossible, that acceptance entry names the exact validation rule and evidence.
   - Every normative and acceptance ID is assigned to at least one ROADMAP stage or to existing behavior that a named stage will validate. When coverage spans stages, identify the stage that provides final acceptance evidence.
   - Every open-question ID appears in the Coverage of each stage whose planning or implementation its answer could affect. Its latest safe gate is no later than the earliest affected stage's Map gate.
   - No stage depends on reopening a transcript, chat, scratch note, or sibling stage tree.

   → **Roadmap/Spec gate.** Present the agreed outcome, stage breakdown and order, ID coverage, open questions, and traceability result. Wait for approval before planning any stage.

2. **Plan and ship the next stage.** Retrieve every SPEC entry assigned by the stage's `Coverage` field. Before decomposing tasks, resolve each covered open question whose latest safe gate has arrived and pass the resulting semantic change through the Spec amendment gate. Then apply `plan-tasks` rooted at `stages/NN-slug/`. It runs its full Map → Plan → Result cycle, producing the stage PLAN and tasks and executing them. PLANs and tasks cite normative and acceptance IDs instead of copying their prose. Fill the stage's `Plan:` pointer in the ROADMAP when planning begins.
   → **Stage gate.** Demonstrate the stage's milestone with the exact commands or behavior proving it ships. Check the stage's box, record shipped outcomes needed by later stages in the ROADMAP, and reassign unchanged SPEC IDs among remaining unstarted stages if evidence warrants it. Keep shipped stage coverage fixed. Record delivery changes and rationale in the ROADMAP Decision Log. Name the next stage and wait.

3. **Amend when necessary.** Stop as soon as the approved artifacts no longer describe the intended work.

   - For a delivery-only change outside a Stage gate, update stage boundaries, order, dependencies, or assignment of unchanged SPEC IDs in the ROADMAP.
     → **Roadmap amendment gate.** Present the delivery change and rationale. Wait for approval before entering a Map gate or resuming implementation.
   - For a semantic change to accepted behavior, constraints, contracts, invariants, or acceptance, update the SPEC according to its lifecycle rules and update ROADMAP coverage when delivery also changes.
     → **Spec amendment gate.** Present the exact semantic change, rationale, affected IDs, acceptance impact, and delivery impact. Wait for approval before entering a Map gate or resuming implementation.

Execute only the current stage. Reallocate unchanged work only at a Stage or Roadmap amendment gate, and change the agreed outcome only at a Spec amendment gate. A PLAN or task may not silently override the SPEC.

# Resuming

Read `ROADMAP.md`; the first unchecked stage is next. Retrieve that stage's assigned entries from `SPEC.md`. If the stage has a PLAN, resume `plan-tasks` at its first unchecked task. If it has no PLAN, plan it from its coverage. Open no sibling stage tree unless its recorded outcome or contract no longer holds.

# Gate discipline

State plainly which gate is active and what requires approval. Keep the Roadmap/Spec gate, Roadmap amendment gate, Spec amendment gate, each stage's internal gates, and the Stage gate as separate sign-offs. The initial gate approves the agreement and initial delivery mapping; a Roadmap amendment gate approves delivery-only changes made between Stage gates; a Spec amendment gate approves semantic changes; a Stage gate approves demonstrated delivery and may also reallocate unchanged future work.

Gate messages are concise: name the gate, summarize only decisions, changes, risks, coverage gaps, open questions, or evidence needed for review, and ask for the specific approval. Do not restate the artifacts, narrate routine work, add generic preambles, or pad a simple answer. A one-line gate message is sufficient when no complexity needs explanation.
