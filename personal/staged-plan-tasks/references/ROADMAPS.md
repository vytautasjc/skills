# Roadmaps

This document defines the `ROADMAP.md` artifact — the coordinator for a multi-stage effort. Read it whenever you create, revise, or resume a ROADMAP. The work *inside* a stage is an ordinary `plan-tasks` plan governed by [`PLANS.md`](../../plan-tasks/references/PLANS.md); this document governs only the stage layer above it.

## What a ROADMAP is

A ROADMAP coordinates the just-in-time delivery of an effort too large for one plan. It lists the **stages** — each an independently shippable milestone, and a vertical slice of capability rather than a horizontal layer pre-built for later stages — tracks which have shipped, and carries the cross-stage knowledge a later stage needs without reading an earlier stage's tree. A **stage** is delivered as its own `plan-tasks` tree under `stages/NN-slug/`; the vertical-capability rule it inherits (mechanism vs. content, walking-skeleton fallback) lives in `PLANS.md` (linked above) under `## Tasks`.

## Self-contained at stage granularity

This is the defining constraint, and it pulls against verbosity on purpose. A ROADMAP must be **lean**: a context-blind agent — one who has never seen this repository and has only the ROADMAP in hand — must be able to read it alone and understand the whole effort's shape, what each stage delivers as observable behavior, the order and dependencies between stages, and which stage is next. It must **not** carry a stage's implementation detail: that lives in the stage's `PLAN.md` and is loaded only when the stage is reached.

This is progressive disclosure, not a license to be vague. Keep each stage description to a few sentences. Cut any prose the stage's own PLAN will carry. Define every term of art in plain language or do not use it. The test: a fresh agent can pick up the effort from the ROADMAP alone and route to the right next stage — and no further.

## Living document

A ROADMAP is revised as stages ship. At each Stage gate: check the shipped stage's box, promote its cross-stage decisions, outcomes, and cross-cutting observations up — leaving a one-line pointer below rather than a duplicate — and re-scope the remaining stages if warranted. Re-scoping may only touch **not-yet-started** stages; a shipped stage is frozen. Every re-scope is recorded in the `Decision Log` with its rationale.

## Formatting

Plain prose, two newlines after every heading, correct list syntax. Status boxes are mandatory in `Stages`; keep the other sections narrative. Use repository-relative paths, never full system paths. When the file's whole content is the ROADMAP, omit surrounding code fences.

## Skeleton

    # <Effort name> Roadmap

    This roadmap is a living document, maintained in accordance with ROADMAPS.md. Each stage is an independently shippable milestone, planned and executed one at a time; the sections below are kept current as stages ship.

    ## Purpose / Big Picture

    What someone can do once every stage has shipped, and how to see it working. State the user-visible outcome of the whole effort in a few sentences.

    ## Stages

    The delivery sequence and the resume index — the only place coarse status is tracked. One entry per stage: status box, completion timestamp once shipped, ordinal, slug, a one-line milestone phrased as observable behavior, and a pointer to the stage's plan once it is being planned. The first unchecked box is the next stage.

    - [x] (2026-06-20 14:00Z) 01 api-foundation — a runnable API serving collaboration rooms
          Plan: stages/01-api-foundation/PLAN.md
    - [ ] 02 frontend-migration — the frontend talks to the API rooms
    - [ ] 03 multi-instance — two API processes share one room

    ## Decision Log

    Every decision that affects more than one stage, and every re-scope of a not-yet-started stage, with the reasoning behind it.

    - Decision: …
      Rationale: …
      Date/Author: (2026-06-20 14:00Z) / <git username>

    ## Outcomes and Retrospective

    Per stage, once shipped: what exists now and how the next stage builds on it — enough that the next stage need not read this stage's tree. At full completion, add a final retrospective comparing the result against the Purpose.

    - Stage 01: …
