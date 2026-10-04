---
name: senior
description: Route non-trivial work by phase. Use when planning, implementing, reviewing, or resuming a change, changing domain meaning, or when another skill needs the repo's phase-to-skill wiring.
---

# Senior

Workflow router. Match the work to its phase and run that phase's skills; each phase is a **gate**, not a suggestion — the phase is not done until its gate holds.

Repository `AGENTS.md` files invoke this workflow through a short `senior` pointer. Keep reusable workflow rules here and in the routed skills; repository guidance owns only repository-specific context and overrides.

## Phase loading

Load every matching row: the governing planning skills remain required during task execution and result review, alongside the phase skills. Load references at their stated triggers. A missing skill blocks only the work requiring it; report the skill and affected phase.

| Phase or trigger | Load |
| --- | --- |
| Plan one responsibility delivered end-to-end | `plan-tasks` |
| Map multiple responsibilities to stages | `staged-plan-tasks`; `plan-tasks` when decomposing the current stage |
| Execute, review results, or resume an existing PLAN or ROADMAP | `plan-tasks`; also `staged-plan-tasks` when governed by a ROADMAP |
| Implement | `ponytail` and `tdd` |
| Review code | `ponytail` and `tdd`; its `tests.md` for test quality |
| Change domain meaning or resolve conflicting terms | `domain-modeling` |
| Resolve an unsettled consequential decision | `grilling`, unless instructed to work autonomously |

On resume, load the governing planning skills before using the PLAN or ROADMAP's explicit state to select the phase. Continue the approved remaining work through that skill's resume procedure; recorded approvals persist. Replanning and grilling activate only for a material change or an unresolved decision. Read established vocabulary through its canonical references without activating domain modeling.

## Communication

Respond in ASD-STE100 Simplified Technical English. Never pad a simple answer to sound thorough. Be concise.

## Plan

Plans live under `docs/`. Follow the selected planning skill's flow and approval gates. Before Roadmap/Spec approval, read [Stage decomposition](../staged-plan-tasks/references/ROADMAPS.md#stage-decomposition) for boundaries, dependencies, and release prerequisites. Before task map approval, read [Decomposition](../plan-tasks/references/PLANS.md#decomposition) for task boundaries and ownership. Before concurrent work, apply [Parallel execution](../plan-tasks/references/PLANS.md#parallel-execution). Use `grilling` for unresolved decisions.

When recording or moving agreements, follow [Current context and ownership](../plan-tasks/references/PLANS.md#current-context-and-ownership); staged ownership is defined in [SPECS.md](../staged-plan-tasks/references/SPECS.md#canonical-ownership). Before compaction, run [Preservation check](../plan-tasks/references/PLANS.md#preservation-check).

## Keep domain language sharp

When domain meaning changes, use `domain-modeling` to build and challenge the ubiquitous language. Route resolved terms by where the feature lives:

- Standalone effort with no `CONTEXT.md` yet → hold terms in the PLAN's `Context and Contracts` section. When scaffolding creates a feature `CONTEXT.md`, move the definitions there without changing meaning, replace PLAN definitions with direct pointers, and update affected references through the preservation check.
- Staged effort, including scaffolding → route terms through [SPECS.md Canonical ownership](../staged-plan-tasks/references/SPECS.md#canonical-ownership).
- A relevant parent `CONTEXT.md` exists → record only broad terms shared by the parent and its siblings there; keep promised feature meaning in the governing PLAN or SPEC.

## Implement

Not done until **both** gates hold:

- Lazy pass — `ponytail` skill: the simplest thing that works, no speculative code.
- Test-first cycle — `tdd` skill: red → green per behavior, regression test first for a bug.

## Code Review

Treat every review comment as a proposal to evaluate, not an instruction to apply. Check every comment against the requirements, code, tests, and the rest of the review. When a different solution is materially better, challenge the comment with evidence, explain the trade-off, and recommend the concrete alternative.

Reconcile the complete set of comments before changing code. For each contradiction, name the conflicting comments and their incompatible outcomes, recommend which one should govern, then use the `grilling` skill to ask the user which to apply. Wait for that decision before implementing either outcome.

Unless specifically instructed to work autonomously, also use `grilling` when review questions or comments leave scope, design, or intended behavior unsettled. Prefix every grilling question with `Review comment:` followed by a short quote and its file/line or comment identifier when available. Three required lenses on the diff:

- Over-engineering — `ponytail` skill.
- Test quality — `tdd` skill, judged against the good/bad examples in its `tests.md`.
- Shared understanding — activate `grilling` only for outstanding decisions.
