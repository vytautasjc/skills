# Roadmaps

This document defines the `ROADMAP.md` artifact — the delivery coordinator for a multi-stage effort. Read it whenever you create, revise, or resume a ROADMAP. The effort's agreed outcome lives in one permanent SPEC governed by [`SPECS.md`](SPECS.md). Work inside the current stage follows the `plan-tasks` skill and its `PLANS.md` reference.

## What a ROADMAP is

A ROADMAP maps the effort SPEC onto independently shippable **stages**, tracks which stages have shipped, and carries delivery knowledge a later stage needs without reading an earlier stage's tree. Each stage is a vertical capability milestone rather than a horizontal layer pre-built for later stages. Only the current stage gets a `PLAN.md` and task files; the vertical-capability rule inherited by stages lives in `PLANS.md` under `## Tasks`.

## Artifact ownership

The artifacts form a traceability chain with one canonical home for each meaning:

- `SPEC.md` owns the complete agreed what and gives each normative obligation and acceptance rule a stable ID.
- `ROADMAP.md` owns stage boundaries and order, dependencies, assignment of normative, acceptance, and open-question SPEC IDs to stages, delivery decisions, status, and shipped outcomes needed later.
- A stage's `PLAN.md` maps its assigned normative and acceptance IDs to tasks and owns shared implementation strategy. Assigned open questions resolve before the affected Map gate, so they do not flow into task plans. A task owns task-local implementation detail and evidence.

Discovery transcripts, chats, and scratch notes are inputs, not execution artifacts. After the Roadmap/Spec gate, every accepted meaning has one durable canonical home; pointers repeat IDs rather than prose.

## Lean and routable

A context-blind agent with only the ROADMAP must understand the effort's delivery shape, each stage's observable milestone, order and dependencies, current status, and which SPEC IDs to retrieve next. The ROADMAP does not restate requirements or implementation detail.

Keep each stage entry compact. Define delivery-level terms in plain language. The test is routing: the ROADMAP selects the next stage and its SPEC coverage; the retrieved SPEC entries provide the agreed outcome; the stage PLAN provides implementation.

## Living document

At each Stage gate, check the shipped stage's box, record outcomes needed by later stages, and reassign unchanged SPEC IDs among remaining unstarted stages when evidence warrants it. If a delivery-only change cannot safely wait for a Stage gate, use the Roadmap amendment gate before entering the affected stage's Map gate or resuming implementation. Keep shipped stage coverage fixed. Record every delivery change and its rationale in the Decision Log.

A semantic change belongs in the SPEC and passes the Spec amendment gate. When it affects delivery, update ROADMAP coverage in the same amendment and point the ROADMAP Decision Log entry to the SPEC revision rather than copying its rationale.

## Formatting

Use plain prose, two newlines after every heading, correct list syntax, and repository-relative paths. Status boxes are mandatory in `Stages`; keep other sections narrative. When the file's whole content is the ROADMAP, omit surrounding code fences.

## Skeleton

    # <Effort name> Roadmap

    This roadmap is a living delivery document maintained in accordance with ROADMAPS.md. The complete agreed outcome lives in SPEC.md. Each stage is an independently shippable milestone planned and executed one at a time.

    Spec: SPEC.md

    ## Delivery Goal

    Summarize how the independently shippable stages combine to realize the SPEC. Keep detailed behavior in the SPEC.

    ## Stages

    The delivery sequence and resume index. One entry per stage: status box, completion timestamp once shipped, ordinal, slug, one-line observable milestone, assigned SPEC IDs, and a PLAN pointer once implementation planning begins. The first unchecked box is next.

    - [x] (2026-06-20 14:00Z) 01 api-foundation — a runnable API serving collaboration rooms
          Coverage: R001-R004, C001, I001, A001-A005
          Plan: stages/01-api-foundation/PLAN.md
    - [ ] 02 frontend-migration — the frontend talks to API rooms
          Coverage: R005-R008, C002, A006-A010, Q001
    - [ ] 03 multi-instance — two API processes share one room
          Coverage: R009-R011, C003, I002, A011-A014

    When a normative ID applies to multiple stages, list it in each contributing stage. Assign its acceptance ID to the stage that produces final evidence and mark that stage as the acceptance owner. List an open-question ID in every stage whose planning or implementation its answer could affect; its latest safe gate must be no later than the earliest affected stage's Map gate. Retain the coverage pointer after resolution.

    ## Dependencies

    Describe dependencies between stages in terms of shipped outcomes or SPEC IDs. Explain why the order matters without opening prior stage trees.

    ## Decision Log

    Record delivery decisions: stage boundaries, ordering, dependency changes, and reassignment of unchanged SPEC IDs. For semantic changes, point to the SPEC Revision Log.

    - Decision: …
      Rationale: …
      Date/Author: (2026-06-20 14:00Z) / <git username>

    ## Outcomes and Retrospective

    Per shipped stage, record what exists, acceptance evidence, and what later stages may rely on. At full completion, add a final retrospective comparing delivery with the goal.

    - Stage 01: …
