---
name: senior
description: Routes each phase of non-trivial work in this repo to the right skill, as paired gates. Use when starting to plan, implement, or review a non-trivial change, or when maintaining domain language — senior decides which skill(s) each phase runs (plan-tasks/staged-plan-tasks, domain-context, ponytail, tdd). Use when another skill needs the repo's phase→skill wiring.
---

# Senior

Workflow router. Match the work to its phase and run that phase's skills; each phase is a **gate**, not a suggestion — the phase is not done until its gate holds.

## Prerequisites

This skill requires the following skills:
- `ponytail`
- `domain-modeling`
- `grilling`
- `tdd`
- `plan-tasks`
- `staged-plan-tasks`

Before performing this workflow:

1. Find the available skills listed above.
2. Load and follow their instructions as a prerequisite.
3. Then continue with the Senior workflow below.
4. If any of the skills listed above is unavailable, stop and report that the required skill is missing.

## Plan

Route by milestone count: `plan-tasks` skill for a single milestone, `staged-plan-tasks` skill for two or more sequential, independently-shippable ones. Grill user using `grilling` skill when planning. Plans live under `docs/`, never the repo root.

## Keep domain language sharp

While planning, grilling, or designing, use `domain-modeling` skill to build and challenge the ubiquitous language. `domain-modeling` skill is plan-agnostic, so route resolved terms by where the feature lives:

- No `CONTEXT.md` yet → hold terms in the plan's `Context and Orientation` section, not a premature `CONTEXT.md` for a feature that does not exist yet.
- Staged effort → effort-wide terms in the `ROADMAP.md` context; stage-specific terms in that stage's `PLAN.md`.
- A relevant parent `CONTEXT.md` exists → record only broad terms shared by the parent and its siblings there; keep feature terms in the plan.
- Scaffolding begins → migrate the plan's terms into the feature's `CONTEXT.md` before writing any source.

## Implement

Not done until **both** gates hold:

- Lazy pass — `ponytail` skill: the simplest thing that works, no speculative code.
- Test-first cycle — `tdd` skill: red → green per behavior, regression test first for a bug.

## Review

Three required lenses on the diff:

- Over-engineering — `ponytail` skill.
- Test quality — `tdd` skill, judged against the good/bad examples in its `tests.md`.
