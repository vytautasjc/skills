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
| Write explanations, documentation, comments, user-facing text, or planning artifacts | [ste-writing-skill](../ste-writing-skill/SKILL.md) |
| Plan one responsibility from start to end | `plan-tasks` |
| Divide multiple responsibilities into stages | `staged-plan-tasks`. Also load `plan-tasks` to divide the current stage into tasks. |
| Execute, review results, or continue an existing PLAN or ROADMAP | `plan-tasks`. Also load `staged-plan-tasks` if a ROADMAP controls the work. |
| Implement code | `ponytail` and `tdd` |
| Review code | `ponytail` and `tdd`. Load the `tdd` reference `tests.md` for test quality. |
| Change domain meaning or resolve conflicting terms | `domain-modeling` |
| Plan work or clarify review comments or areas | `grilling` |

To continue work, first load the applicable planning skills. Then use the PLAN or ROADMAP state to select the phase. Use the skill's resume procedure for the remaining approved work. Keep recorded approvals valid.

Prepare a new plan when an important change requires one. Read established terms through their canonical references. Use `domain-modeling` only when the domain meaning changes or has conflicts.

Apply `ste-writing-skill` to all text in planning artifacts generated or revised through `plan-tasks` or `staged-plan-tasks`, in files and in chat. This includes SPECs, ROADMAPs, PLANs, task briefs, handoffs, history records, and supporting planning documents. Review all new or changed artifact text with the skill before you save or present the artifact. Correct each problem found in the review.

## Plan

Keep plans in `docs/`. Use the selected planning skill's procedure and approval gates.

Use `grilling` during every planning phase, including changes to a plan and task or stage detailing. This requirement is mandatory, even when the request appears complete. Examine scope, assumptions, design choices, boundaries, dependencies, and acceptance with the user. Resolve each unclear point through the skill's question rounds. Complete planning only after the user confirms shared understanding and all decisions necessary for the current planning gate are resolved. Keep earlier approved decisions valid.

- Before Roadmap/Spec approval, read [Stage decomposition](../staged-plan-tasks/references/ROADMAPS.md#stage-decomposition).
- Before task map approval, read [Decomposition](../plan-tasks/references/PLANS.md#decomposition).
- Before concurrent work, use [Parallel execution](../plan-tasks/references/PLANS.md#parallel-execution).

To write or move agreements, use [Current context and ownership](../plan-tasks/references/PLANS.md#current-context-and-ownership). For staged work, use [Canonical ownership](../staged-plan-tasks/references/SPECS.md#canonical-ownership). Before you make documents shorter, complete the [Preservation check](../plan-tasks/references/PLANS.md#preservation-check).

## Keep domain language sharp

When domain meaning changes, use `domain-modeling` to prepare and examine the shared domain language. Keep agreed terms in the applicable location:

- **Standalone work without a feature `CONTEXT.md`:** keep terms in the PLAN's `Context and Contracts` section. When scaffolding creates `CONTEXT.md`, move the definitions there. Keep their meaning unchanged. Replace the PLAN definitions with direct references. Update affected references through the preservation check.
- **Staged work, including scaffolding:** use [Canonical ownership](../staged-plan-tasks/references/SPECS.md#canonical-ownership).
- **Work with an applicable parent `CONTEXT.md`:** keep broad terms shared by the parent and its siblings there. Keep promised feature meaning in the applicable PLAN or SPEC.

## Implement

Before you change implementation code, load and use `ponytail` and `tdd`. Both skills are mandatory for every feature, logic change, and bug fix. This rule also applies to small changes, resumed work, and fixes from code review.

TDD is mandatory even for a one-line change. Use `ponytail` to simplify the implementation without removing required tests.

Use one TDD cycle for each new or changed behavior:

1. **Red:** write a test through an agreed public interface. For a bug fix, write a regression test that reproduces the bug. Run the test before you change implementation code. Confirm that the test fails because the behavior is missing or incorrect.
2. **Green:** use `ponytail` to select the simplest solution that works. Add only the code necessary to make the test pass. Run the test and confirm that it passes.
3. Repeat the cycle for the next behavior.

Complete implementation only after you record Red and Green test results for each new or changed behavior. All required checks must pass. If you cannot run a required test, stop the affected implementation. Report why you cannot run the test.

## Code Review

Examine each review comment as a proposal. Compare each comment with the requirements, code, tests, and other comments. If a different solution is much better, give evidence for it. Show the trade-off. Recommend the specified alternative.

Review all comments together before you change code. For each contradiction, identify the conflicting comments and incompatible results. Recommend which comment to use. Use `grilling` to get the user's decision about which result to use. Wait for that decision before you implement either result.

Use `grilling` whenever a review comment or reviewed area is not fully clear. This requirement is mandatory, including for small points. Clarify meaning, scope, design, intended behavior, and acceptance as applicable. Wait for the user's answers before you implement the affected change or complete its review. Start each question about a comment with `Review comment:`. Add a short quotation and the file/line or comment identifier, if available. For an unclear area without a comment, identify the area and the unclear point.

Examine the diff for all three areas:

- Unnecessary complexity: use `ponytail`.
- Test quality: use `tdd` and the good and bad examples in its `tests.md`.
- Shared understanding: apply the clarification requirement above to each unclear comment or area.
