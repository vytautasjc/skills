# Effort Specifications

This document defines the permanent `SPEC.md` artifact for one staged effort. Read it whenever you create, revise, review, or consume an effort SPEC. Delivery coordination is governed by [`ROADMAPS.md`](ROADMAPS.md). Just-in-time implementation planning follows the `plan-tasks` skill and its `PLANS.md` reference.

## What a SPEC is

The SPEC is the durable source of truth for the complete agreed **what** across the effort. It preserves accepted behavior and product decisions from discovery while delivery partitioning and implementation details remain separate. Create one SPEC beside the ROADMAP during initial decomposition and keep it for the life of the effort.

A complete SPEC lets a context-blind agent understand any stage's assigned outcome without reopening a transcript, chat, scratch document, or sibling stage tree. It states the overall outcome, scope, domain language, requirements, contracts, invariants, acceptance scenarios, and unresolved product questions. It does not assign work to stages, decompose tasks, prescribe file edits, list commands, or predict implementation details.

## Canonical ownership

Keep each meaning in one authoritative place:

- `SPEC.md` owns the complete agreed behavior, constraints, contracts, invariants, acceptance, domain meaning, and unresolved product questions across every stage.
- `ROADMAP.md` owns delivery: stage boundaries and order, dependencies, SPEC-ID coverage, status, delivery decisions, and shipped outcomes needed later.
- A stage's `PLAN.md` owns implementation strategy shared by that stage's tasks. A task file owns task-local implementation detail.

Pointers may repeat stable IDs, but prose and rationale retain one canonical home. When an item's scope or delivery stage changes, update pointers rather than moving or copying its definition.

## Stable IDs and traceability

Use IDs that survive delivery re-planning:

- `R001`, `R002`, … for required behavior or constraints.
- `C001`, `C002`, … for externally relevant interface, data, protocol, compatibility, or recovery contracts.
- `I001`, `I002`, … for invariants that must remain true.
- `A001`, `A002`, … for acceptance scenarios or validation rules.
- `Q001`, `Q002`, … for unresolved product questions.

Every normative ID (`R`, `C`, or `I`) must be covered by one or more `A` IDs. When direct behavioral observation is impossible, the acceptance entry names the exact inspection, analysis, or test evidence that proves the obligation. Acceptance entries cite every normative ID they cover.

IDs remain stable when wording is clarified without changing meaning. When meaning changes after approval, mark the old entry `Retired`, point it to its replacement when one exists, and add a new ID; never reuse an identifier. This lets a requirement move between stages without changing identity and preserves the meaning of evidence produced by shipped stages.

The ROADMAP assigns normative, acceptance, and relevant open-question IDs to stages. A stage PLAN assigns its normative and acceptance coverage to tasks, and task results record evidence against acceptance IDs. Open-question IDs route unresolved decisions to every stage they could affect and are resolved before the earliest affected Map gate. Repeating IDs along this chain is a pointer, not duplicated specification prose.

An open-question ID remains stable when answered. Mark the entry `Resolved`, record the answer and the normative or acceptance IDs it added or clarified, and preserve the original question. Because answering a product question changes or completes the agreed outcome, pass the resolution through the Spec amendment gate before affected planning or implementation continues.

## Completeness bar

Before the Roadmap/Spec gate, compare every discovery source against the SPEC and ROADMAP. Confirm that:

- Every accepted behavior and product decision has one canonical durable home.
- Every required happy path, error path, edge case, failure mode, security or privacy constraint, compatibility or migration concern, operational expectation, and recovery behavior is captured when applicable.
- Every normative ID is covered by acceptance evidence.
- Every delivery dependency is represented in the ROADMAP without copying SPEC prose.
- Every open question states what resolves it and the latest safe gate for deciding it, and its ID appears in the ROADMAP coverage of every stage it could affect. The latest safe gate is no later than the earliest affected stage's Map gate.
- A future planner needs no transcript, conversation memory, or sibling-stage file.

## Lifecycle

The initial Roadmap/Spec gate approves both the agreement and its first delivery mapping. After that gate, changes follow one of two paths:

- Reassigning unchanged SPEC IDs among unstarted stages is a delivery change. Make it at a Stage gate when reviewing a shipped milestone, or at a Roadmap amendment gate when the change cannot safely wait. Update the ROADMAP and record the rationale in its Decision Log.
- Changing agreed behavior, constraints, contracts, invariants, or acceptance, including resolving an open product question, is a semantic change. Retire and add normative or acceptance IDs as needed; retain a resolved question under its existing ID. Add a SPEC Revision Log entry, update ROADMAP coverage when affected, and stop at the Spec amendment gate before planning or implementation continues.

Shipped stage coverage and evidence stay fixed. A later semantic change adds new IDs for future delivery rather than rewriting what a shipped stage proved. Clarifications that preserve meaning may keep the existing ID, but the Revision Log must make the clarification and its rationale visible.

## Formatting

Use plain prose, two newlines after every heading, and correct list syntax. Write every filesystem path relative to the repository root; absolute paths never appear in the SPEC. Define each domain term at first use. Treat the file as public: no secrets. Omit optional sections that add no value instead of writing `N/A`, but retain every section needed to satisfy the completeness bar. When the file's whole content is the SPEC, omit surrounding code fences.

## Template

    # <Effort name> Specification

    This SPEC is the durable source of truth for the effort's agreed outcome. It is maintained in accordance with SPECS.md. The ROADMAP, stage PLANs, and tasks cite IDs from this document rather than duplicate their prose.

    ## Purpose / Big Picture

    State what someone can do when the effort is complete and how a human can recognize that outcome. Keep delivery order and implementation choices out.

    ## Ubiquitous Language

    Define the domain terms needed to interpret the specification. Keep implementation-only terminology in the relevant PLAN, task, or code context document.

    ## Scope

    ### Included

    State the behaviors, users, data, and operating conditions covered by the effort.

    ### Excluded

    State nearby behavior deliberately deferred or rejected.

    ## Requirements

    Record every accepted behavior and constraint. Include rationale where the reason prevents future reinterpretation.

    - R001: …
      Rationale: …

    ## Contracts

    Define externally relevant interfaces, data or protocol rules, compatibility boundaries, and failure or recovery guarantees.

    - C001: …

    ## Invariants

    Define the truths implementation must preserve across all relevant states and transitions.

    - I001: …

    ## Acceptance Scenarios

    Describe observable scenarios or exact validation rules that collectively prove every normative ID, including relevant errors and edge cases.

    - A001 (covers R001, C001, I001): Given …, when …, then …

    ## Open Questions

    Include only genuinely unresolved product points. State why each is unresolved, what resolves it, and the latest safe gate. Implementation choices that do not affect the agreed outcome belong in the future PLAN instead.

    - Q001 [Open]: …
      Why unresolved: …
      Resolution condition: …
      Latest safe gate: …

    When answered, retain the entry as `Q001 [Resolved]` and add its resolution plus the normative or acceptance IDs it added or clarified.

    ## Revision Log

    Append every post-approval clarification or semantic amendment. Preserve prior entries.

    - Revision: …
      Affected IDs: …
      Rationale: …
      Approval gate: Roadmap/Spec | Spec amendment
      Date/Author: (2026-06-20 14:00Z) / <git username>
