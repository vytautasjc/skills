# Roadmaps

This document defines the `ROADMAP.md` artifact — the delivery coordinator for a multi-stage effort. Read it whenever you create, revise, or resume a ROADMAP. The effort's agreed outcome lives in one permanent SPEC governed by [`SPECS.md`](SPECS.md). Work inside the current stage follows the `plan-tasks` skill and its `PLANS.md` reference.

## What a ROADMAP is

A ROADMAP maps the effort SPEC onto small **stages**, tracks accepted results, and carries delivery knowledge later stages need without opening earlier stage trees.

## Stage decomposition

A stage delivers one coherent responsibility end-to-end across all required implementation areas, with a focused observable outcome and its own acceptance criteria. Separate responsibilities become separate stages, even when they affect the same user journey: Google authentication and authentication rate limiting are separate stages.

Before Roadmap/Spec approval, split stages that combine separate responsibilities; record a narrow exception only when separation would leave an invalid intermediate state, naming the reason and affected boundary. Record dependencies between stages and prerequisites for production release. Stages may depend on accepted outcomes or be independent. Acceptance in development leaves production release subject to those prerequisites.

Assign each stage's acceptance slice using [SPECS.md Stable IDs and traceability](SPECS.md#stable-ids-and-traceability). Decompose the current stage into tasks using [PLANS.md Decomposition](../../plan-tasks/references/PLANS.md#decomposition).

## Artifact ownership

Use [SPECS.md Canonical ownership](SPECS.md#canonical-ownership) when recording agreements or delivery decisions, and [Stable IDs and traceability](SPECS.md#stable-ids-and-traceability) when assigning coverage. The skeleton below defines the ROADMAP's structure.

## Lean and routable

A context-blind agent with only the ROADMAP must understand the effort's delivery shape, each stage's focused observable outcome, order and dependencies, current status, and which SPEC IDs to retrieve next. The ROADMAP does not restate requirements or implementation detail.

Use the shortest wording that passes that routing test. Keep each stage entry compact; state each fact once; omit generic introductions, repeated SPEC prose, routine narration, ornamental examples, and empty optional sections. Expand only when a real dependency, risk, ambiguity, or delivery decision needs explanation. Define delivery-level terms in plain language.

## Living document

At each Stage gate, check the shipped stage's box, record outcomes needed by later stages, and reassign unchanged SPEC IDs among remaining unstarted stages when evidence warrants it. If a delivery-only change cannot safely wait for a Stage gate, use the Roadmap amendment gate before entering the affected stage's Map gate or resuming implementation. Keep shipped stage coverage fixed. Record every delivery change and its rationale in the Decision Log.

A semantic change belongs in the SPEC and passes the Spec amendment gate. When it affects delivery, update ROADMAP coverage in the same amendment and point the ROADMAP Decision Log entry to the SPEC revision rather than copying its rationale.

When superseding decisions or compacting the ROADMAP, follow [History and preservation](SPECS.md#history-and-preservation); keep the ROADMAP a direct index to governing delivery agreements.

## Resume state and retrieval

Near the top, record `Current stage`, `State`, and `Remaining`. States are `awaiting-roadmap-spec-review`, `ready-to-plan`, `working-stage`, `awaiting-stage-review`, `awaiting-roadmap-amendment-review`, `awaiting-spec-amendment-review`, and `complete`. Amendment states also name the state to resume after approval. During `working-stage`, the PLAN's explicit task state selects the action. Requested stage revisions return to `working-stage`, reopen affected tasks in the PLAN, clear their accepted checkboxes, and record remaining work. A checkbox means accepted delivery; approval gates remain pending until explicitly accepted.

Retrieve complete stage SPEC coverage for decomposition and stage acceptance. During task planning and execution, retrieve only the current task's assigned entries, referenced contracts and invariants, and necessary glossary entries. Maintain the complete coverage map across all phases. At an accepted result, preserve the contracts later work needs in the appropriate parent handoff and recommend a fresh conversation for the next task or stage.

## Size and decomposition review

Use roughly 50–150 words per stage entry as a soft routing target. Larger entries trigger review for duplicated SPEC content, independent responsibilities, and clearer dependency references. Never drop agreements or hide necessary detail in another mandatory document to meet a target. Required shared contracts and integration work have explicit owners in the current stage task map.

## Formatting

Use compact plain prose or bullets, whichever is clearer. Use one blank line after headings and correct list syntax. Write every path relative to the repository root. Status boxes are mandatory in `Stages`. Omit optional sections and placeholder text. When the file's whole content is the ROADMAP, omit surrounding code fences.

## Skeleton

    # <Effort name> Roadmap

    Current stage: <NN-slug | none>
    State: <state from Resume state and retrieval>
    Remaining: <exact next action or approval; state to resume after amendment>
    Spec: <repository-relative SPEC path>
    Method: <repository-relative path to ROADMAPS.md, only when checked in>

    ## Delivery Goal

    Summarize how the focused stages combine to realize the SPEC. Keep detailed behavior in the SPEC.

    ## Stages

    The delivery sequence and full coverage map. One entry per stage: status box, completion timestamp once accepted, ordinal, slug, one-line focused observable outcome, assigned SPEC IDs with acceptance portions and final ownership when shared, and a PLAN pointer once implementation planning begins. The explicit state above selects the resume action.

    - [x] (2026-06-20 14:00Z) 01 google-authentication — controlled Google sign-in reaches a protected page and logout revokes access
          Coverage: R001-R004, C001, I001, A001-A005
          Plan: docs/plans/<effort-slug>/stages/01-google-authentication/PLAN.md
    - [ ] 02 authentication-rate-limiting — authentication limits enforce safe HTTP outcomes and browser retry handling
          Coverage: R005-R008, C002, A006-A010, Q001
    - [ ] 03 multi-instance-collaboration — clients on separate replicas edit the same durably committed document
          Coverage: R009-R011, C003, I002, A011-A014

    When a normative ID applies to multiple stages, list it in each contributing stage. Apply SPECS.md Stable IDs and traceability to shared acceptance coverage. List an open-question ID in every stage whose planning or implementation its answer could affect; its latest safe gate must be no later than the earliest affected stage's Map gate. Retain the coverage pointer after resolution.

    ## Dependencies and Release Prerequisites

    Describe dependencies between stages in terms of accepted outcomes or SPEC IDs. Identify production release prerequisites separately from implementation order. Explain the order without opening prior stage trees.

    ## Decision Log

    Record current delivery decisions under stable IDs or named anchors: stage boundaries, ordering, dependency changes, and reassignment of unchanged SPEC IDs. For semantic changes, point to the SPEC Revision Log; for decision history, apply PLANS.md Current instructions and history.

    - D001: …
      Rationale: …
      Date/Author: (2026-06-20 14:00Z) / <git username>

    ## Outcomes and Retrospective

    Per accepted stage, record a short handoff as defined in PLANS.md Current instructions and history, with any remaining obligations later stages need.

    - Stage 01: …

    ## Audit References

    Direct file and ID/anchor pointers to superseded decisions, review records, and shipped evidence. Label history for audit or investigation. Record the preservation-check result when compacting the ROADMAP.
