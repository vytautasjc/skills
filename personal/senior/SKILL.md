---
name: senior
description: Select skills for each phase of complex work. Use to plan, implement, review, or continue a change. Also use for changes to domain meaning. Use when another skill needs the repository's phase-to-skill rules.
---

# Senior

Select the skills for the current phase. Use each selected skill. Each phase has a **gate**: a condition that must hold before the phase is completed.

Repository `AGENTS.md` files refer to this workflow through a short `senior` reference. Keep shared workflow rules here and in the selected skills. Keep repository context and overrides in repository guidance.

## Phase loading

Load the skills from each applicable row. Keep the planning skills active during task execution and result review. Load references when their stated conditions apply.

If a skill is missing, stop only the work for which it is necessary. Identify the missing skill and affected phase.

| Phase or condition | Skills to load |
| --- | --- |
| Write explanations, documentation, comments, or user-facing text | [ste-writing-skill](../ste-writing-skill/SKILL.md) |
| Plan one responsibility from start to end | `plan-tasks` |
| Divide multiple responsibilities into stages | `staged-plan-tasks`. Also load `plan-tasks` to divide the current stage into tasks. |
| Execute, review results, or continue an existing PLAN or ROADMAP | `plan-tasks`. Also load `staged-plan-tasks` if a ROADMAP controls the work. |
| Implement | `ponytail` and `tdd` |
| Review code | `ponytail` and `tdd`. Load the `tdd` reference `tests.md` for test quality. |
| Change domain meaning or resolve conflicting terms | `domain-modeling` |
| Resolve an open decision with important effects | `grilling`, unless the user instructs you to work independently. |

To continue work, first load the applicable planning skills. Then use the PLAN or ROADMAP state to select the phase. Use the skill's resume procedure for the remaining approved work. Keep recorded approvals valid.

Prepare a new plan or use `grilling` only for an important change or an open decision. Read established terms through their canonical references. Use `domain-modeling` only when the domain meaning changes or has conflicts.

## Plan

Keep plans in `docs/`. Use the selected planning skill's procedure and approval gates.

- Before Roadmap/Spec approval, read [Stage decomposition](../staged-plan-tasks/references/ROADMAPS.md#stage-decomposition).
- Before task map approval, read [Decomposition](../plan-tasks/references/PLANS.md#decomposition).
- Before concurrent work, use [Parallel execution](../plan-tasks/references/PLANS.md#parallel-execution).
- For open decisions, use `grilling`.

To write or move agreements, use [Current context and ownership](../plan-tasks/references/PLANS.md#current-context-and-ownership). For staged work, use [Canonical ownership](../staged-plan-tasks/references/SPECS.md#canonical-ownership). Before you make documents shorter, complete the [Preservation check](../plan-tasks/references/PLANS.md#preservation-check).

## Keep domain language sharp

When domain meaning changes, use `domain-modeling` to prepare and examine the shared domain language. Keep agreed terms in the applicable location:

- **Standalone work without a feature `CONTEXT.md`:** keep terms in the PLAN's `Context and Contracts` section. When scaffolding creates `CONTEXT.md`, move the definitions there. Keep their meaning unchanged. Replace the PLAN definitions with direct references. Update affected references through the preservation check.
- **Staged work, including scaffolding:** use [Canonical ownership](../staged-plan-tasks/references/SPECS.md#canonical-ownership).
- **Work with an applicable parent `CONTEXT.md`:** keep broad terms shared by the parent and its siblings there. Keep promised feature meaning in the applicable PLAN or SPEC.

## Implement

Complete implementation only when the two conditions hold:

- **Lazy pass, `ponytail`:** use the simplest solution that works. Add code only for current needs.
- **Test-first cycle, `tdd`:** write a failing test for each behavior. Then make that test pass. For a bug, start with a regression test.

## Code Review

Examine each review comment as a proposal. Compare each comment with the requirements, code, tests, and other comments. If a different solution is much better, give evidence for it. Show the trade-off. Recommend the specified alternative.

Review all comments together before you change code. For each contradiction, identify the conflicting comments and incompatible results. Recommend which comment to use. Use `grilling` to get the user's decision about which result to use. Wait for that decision before you implement either result.

Unless the user instructs you to work independently, use `grilling` for open review decisions about scope, design, or intended behavior. Start each question with `Review comment:`. Add a short quotation and the file/line or comment identifier, if available.

Examine the diff for all three areas:

- Unnecessary complexity: use `ponytail`.
- Test quality: use `tdd` and the good and bad examples in its `tests.md`.
- Shared understanding: use `grilling` only for open decisions.
