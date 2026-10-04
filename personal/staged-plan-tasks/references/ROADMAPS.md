# Roadmaps

This reference gives rules for `ROADMAP.md`, the delivery coordinator for an effort with multiple stages. To create, revise, or continue a ROADMAP, read this file. Keep the agreed outcome in one permanent SPEC with the rules in [`SPECS.md`](SPECS.md). For current stage work, use `plan-tasks` and its `PLANS.md` reference.

## What a ROADMAP is

A ROADMAP maps the effort SPEC to small **stages**. It tracks accepted results. It holds delivery knowledge for remaining stages without dependencies on earlier stage trees.

## Stage decomposition

Decompose stages into **vertical feature slices**. Each feature stage delivers one responsibility from start to end across all necessary implementation areas. Each feature stage has a focused observable outcome and its own acceptance criteria. Give separate responsibilities separate stages, even in the same user journey. For example, user authentication and authentication rate limiting are separate stages.

Keep each feature's data, settings, interfaces, and tests in the stage that delivers the feature. Divide stages by observable feature behavior, not by backend, frontend, storage, or other horizontal layers. Prefer a larger vertical slice to a smaller stage that contains only one layer.

Before Roadmap/Spec approval, check that a human can observe each feature stage working without the next stage. If this check fails, combine the incomplete stage with the stage that makes the feature behavior observable.

The only exception to vertical slicing is a stage for a **shared mechanism**. This stage must have no feature-specific content. Examples include a runtime, storage connection, configuration loader, or test harness. Use this exception only when the mechanism needs a separate boundary from the first feature. Write the reason. Demonstrate that the mechanism starts, connects, loads configuration, or runs tests. Keep future features' data, settings, and interfaces in their feature stages.

If one feature is too large for a stage, first deliver a **walking skeleton**. This is the smallest path through all necessary layers that produces observable behavior. Add more behavior in later vertical slices.

Before Roadmap/Spec approval, divide stages that combine separate responsibilities. Let a narrow exception apply only if separation causes an invalid intermediate state. Write the reason and affected boundary.

Write dependencies between stages. Give production release prerequisites as a separate list. Stages can depend on accepted outcomes or be independent. Acceptance in development does not remove production release prerequisites.

Give each stage's acceptance portion through [Stable IDs and traceability](SPECS.md#stable-ids-and-traceability). Divide the current stage into tasks through [Decomposition](../../plan-tasks/references/PLANS.md#decomposition).

## Artifact ownership

To write agreements or delivery decisions, use [Canonical ownership](SPECS.md#canonical-ownership). To give coverage, use [Stable IDs and traceability](SPECS.md#stable-ids-and-traceability). Use the skeleton below for ROADMAP structure.

## Lean and routable

The ROADMAP must give an agent without conversation history enough information to select work. Include delivery structure, each stage's observable outcome, order, dependencies, current status, and SPEC IDs to read next. Keep requirement definitions and implementation detail in their own documents.

Keep each stage entry short. Write each fact once. Omit empty optional sections. Add detail only for dependencies, risks, unclear meaning, or delivery decisions. Define each delivery term in plain language.

## Living document

At each Stage gate, set the accepted stage's box to checked. Write outcomes necessary for remaining stages. With approval, reassign unchanged SPEC IDs among stages that have not started when evidence shows that the change is necessary.

If a delivery-only change cannot safely wait, use the Roadmap amendment gate. Get approval before the affected Map gate or continued implementation. Keep delivered stage coverage fixed. Write each delivery change and its reason in the Decision Log.

For a semantic change, update the SPEC. Pass the Spec amendment gate. If delivery changes, update ROADMAP coverage in the same amendment. Add a link from the ROADMAP Decision Log entry to the SPEC revision. Keep the reason in that revision.

To replace decisions or make the ROADMAP shorter, use [History and preservation](SPECS.md#history-and-preservation). Keep direct references to applicable delivery agreements.

## Resume state and retrieval

Near the top, write `Current stage`, `State`, and `Remaining`. Use these states:

- `awaiting-roadmap-spec-review`
- `ready-to-plan`
- `working-stage`
- `awaiting-stage-review`
- `awaiting-roadmap-amendment-review`
- `awaiting-spec-amendment-review`
- `complete`

For amendment states, identify the state to resume after approval. During `working-stage`, select the action from the PLAN's explicit task state.

For requested stage revisions, set the state to `working-stage`. Reopen affected tasks in the PLAN. Clear their accepted checkboxes. Write remaining work.

A checked box means accepted delivery. Keep approval gates pending until explicit acceptance.

For decomposition and stage acceptance, load full stage SPEC coverage. For task planning and execution, load only the task's assigned entries, referenced contracts and invariants, and necessary glossary entries. Keep the full coverage map across all phases.

After result acceptance, keep contracts necessary for future work in the applicable parent handoff. Recommend a new conversation for the next task or stage.

## Size and decomposition review

Use approximately 50–150 words per stage entry as a flexible target. For larger entries, examine repeated SPEC content, independent responsibilities, and dependency references.

Keep all agreements and necessary detail available. A target does not justify a new mandatory document that hides necessary detail. Give necessary shared-contract and integration work explicit owners in the current stage task map.

## Formatting

Use short paragraphs or lists, whichever is clearer. Put one blank line after each heading. Use correct list syntax. Write each path relative to the repository root. Use status boxes in `Stages`. Omit unnecessary optional sections and placeholder prose. For a standalone ROADMAP file, omit outer code fences.

## Skeleton

    # <Effort name> Roadmap

    Current stage: <NN-slug | none>
    State: <state from Resume state and retrieval>
    Remaining: <specified next action or approval, and resume state after amendment>
    Spec: <repository-relative SPEC path>
    Method: <repository-relative ROADMAPS.md path, only if stored in the repository>

    ## Delivery Goal

    Write how the stages together deliver the SPEC.
    Keep detailed behavior in the SPEC.

    ## Stages

    Give the delivery sequence and full coverage map.
    Use one entry per stage.
    Include a status box, ordinal, slug, and one-line observable outcome.
    After acceptance, add the completion timestamp.
    Give assigned SPEC IDs.
    For shared acceptance, identify portions and final ownership.
    When implementation planning starts, add the PLAN reference.
    Use the explicit state above to select the resume action.

    - [x] (2026-06-20 14:00Z) 01 google-authentication — controlled Google sign-in opens a protected page and logout removes access
          Coverage: R001-R004, C001, I001, A001-A005
          Plan: docs/plans/<effort-slug>/stages/01-google-authentication/PLAN.md
    - [ ] 02 authentication-rate-limiting — authentication limits produce safe HTTP results and browser retry behavior
          Coverage: R005-R008, C002, A006-A010, Q001
    - [ ] 03 multi-instance-collaboration — clients on separate replicas edit the same durably committed document
          Coverage: R009-R011, C003, I002, A011-A014

    Give a normative ID in each stage where it applies.
    For shared acceptance coverage, use SPECS.md Stable IDs and traceability.
    Give each open-question ID in each stage whose planning or implementation its answer can affect.
    Keep its latest safe gate at or before the earliest affected stage's Map gate.
    Keep the coverage reference after resolution.

    ## Dependencies and Release Prerequisites

    Write dependencies between stages through accepted outcomes or SPEC IDs.
    Give production release prerequisites as a separate list from implementation order.
    Explain the order without dependencies on earlier stage trees.

    ## Decision Log

    Write delivery decisions with stable IDs or named anchors.
    Include stage boundaries, order, dependency changes, and reassignment of unchanged SPEC IDs.
    For semantic changes, refer to the SPEC Revision Log.
    For decision history, use PLANS.md Current instructions and history.

    - D001: …
      Rationale: …
      Date/Author: (2026-06-20 14:00Z) / <git username>

    ## Outcomes and Retrospective

    For each accepted stage, write a short handoff with PLANS.md Current instructions and history.
    Include remaining obligations necessary for remaining stages.

    - Stage 01: …

    ## Audit References

    Give direct references to replaced decisions, review records, and delivered evidence.
    Include the file and ID or anchor.
    Identify history as material for audit or investigation.
    When you make the ROADMAP shorter, write the preservation-check result here.
