---
name: staged-plan-tasks
description: Use when an effort is too large for a single plan — it delivers two or more sequential, independently shippable milestones, spans multiple agent runs, or cannot be detailed up front because later work depends on the results of earlier shipped work. Decomposes the effort into a ROADMAP of stages, each milestone delivered as its own plan-tasks tree, planned and executed one stage at a time. Offer it instead of a flat plan when sizing up multi-milestone work.
---

Plan and deliver a large effort as a sequence of independently-shippable **stages**, each its own `plan-tasks` tree, coordinated by a lean `ROADMAP.md`.

# When to use

A **stage** is a milestone: a vertical slice that ends in demonstrable, observable behavior a human can run, not a horizontal layer. The vertical-capability rule governing tasks governs stages one level up — a stage delivers a capability end-to-end and never a layer pre-built for later stages; the mechanism-vs-content distinction and walking-skeleton fallback in `plan-tasks`'s `PLANS.md` (`## Tasks`) apply here at stage granularity. Reach for this skill only when the effort spans **two or more sequential milestones** — a later one building on an earlier *shipped* one — or is too large to detail at once because later stages depend on outcomes you will not know until earlier stages ship (the just-in-time smell). One milestone is a flat `plan-tasks` plan, not a roadmap.

**Offer, do not impose.** When sizing up an effort that meets the bar, state the case — "this looks like N milestones; I would stage it, or we can keep it one plan" — and let the user choose. The default is a single plan.

# Instructions

1. Read [`ROADMAPS.md`](references/ROADMAPS.md) when creating, revising, or resuming a ROADMAP. It defines the ROADMAP's content, structure, formatting, leanness bar, and skeleton.
2. A stage is delivered with the `plan-tasks` skill, rooted at the stage directory. This skill owns only the stage layer; it never restates the per-task flow.
3. Plan and execute stages just-in-time: one stage is fully planned and shipped before the next is planned.

# Artifacts

Resolve the layout from the nearest `AGENTS.md` first; it overrides the default below. Default, one tree per effort:

    docs/plans/<plan-slug>/
      ROADMAP.md                 # this skill's artifact: stages, status, cross-stage log
      stages/
        01-<stage-slug>/         # one ordinary plan-tasks tree per stage
          PLAN.md
          tasks/
            01-<task-slug>.md
        02-<stage-slug>/
          ...

Use the current git username as author where a section needs one. Treat these as public documents: no secrets.

# Context isolation across stages

A stage is to the ROADMAP what a task is to a PLAN — the same isolation, one level up:

- When working a stage, load `ROADMAP.md` and that stage's tree **only**. Never load a sibling stage's `PLAN.md` or tasks.
- Cross-stage knowledge flows **only through the ROADMAP's `Decision Log` and `Outcomes and Retrospective`**, never by reading a sibling stage. A decision, outcome, or cross-cutting observation the next stage needs is *promoted* up the two-level chain — task → stage `PLAN` → `ROADMAP` — when the stage ships. At each link the entry keeps one canonical home at the highest scope that consumes it, and the level below replaces it with a one-line pointer; never duplicate the full text across levels.
- Reopen a sibling stage's files only when a **contract** changes — a stage's promised interface or outcome that a later stage relies on stops holding.
- Keep the ROADMAP lean. Detail belongs in stage plans; the ROADMAP holds only what a context-blind agent needs to grasp the whole effort and pick the next stage (see `ROADMAPS.md`).

# Flow

Decompose the roadmap, then plan and ship each stage just-in-time. Two stage-level gates wrap `plan-tasks`'s own three gates (Map, Plan, Result). At every gate, stop and wait for an explicit instruction to continue.

1. **Decompose.** Inspect the repository, then write `ROADMAP.md` following `ROADMAPS.md`: the Purpose, and each stage as an ordinal, slug, one-line milestone, and an unchecked status box. Do not detail any stage.
   → **Roadmap gate.** Present the stage breakdown and order. Wait for approval before planning any stage.

2. **Plan and ship the next stage.** Apply `plan-tasks` rooted at `stages/NN-slug/`: it runs its full Map → Plan → Result cycle, producing the stage's `PLAN.md` and tasks and executing them. Fill the stage's `Plan:` pointer in the ROADMAP when planning begins.
   → **Stage gate.** Demonstrate the stage's milestone — the exact commands or behavior proving it ships, not merely that code compiles. Check the stage's box, promote cross-stage decisions and outcomes to the ROADMAP, and re-scope the remaining (not-yet-started) stages if what you learned warrants it. A shipped stage is frozen; never re-scope it. Name the next stage and wait.

Execute only the current stage. Never cross a gate, plan the next stage, or expand a shipped stage without an explicit instruction. If a discovery invalidates a not-yet-started stage, revise the ROADMAP at the Stage gate rather than pressing on.

# Resuming

Read `ROADMAP.md`; the first unchecked stage is the next. If it has a `PLAN.md`, resume `plan-tasks` inside it (its Progress → first unchecked task). If it has no `PLAN.md`, it is the next stage to plan. Open no other stage's files unless a **contract** changes.

# Gate discipline

A gate is a hard stop. State plainly which gate you are at and what you need approved. Do not bundle the Roadmap gate, a stage's internal gates, and the Stage gate into one sign-off. Record resolved questions and re-scopes in the ROADMAP's `Decision Log` with rationale as they settle.
