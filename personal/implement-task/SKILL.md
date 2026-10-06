---
name: implement-task
description: Implement one task from a task file, plan file, or plan directory. Use for task execution, review corrections, or resume under the to-tasks workflow. Require human result review.
---

# Implement Task

Implement one authorized task and return its result for human review. Accept a task file, a `PLAN.md` file, or a directory containing `PLAN.md` and `tasks/`.

Read repository guidance, the task, its plan, linked spec sections, and relevant code. Do not convert artifacts from another workflow.

## Implementation

1. Use the named task or select the first unchecked task in plan order. For task input, find the plan at `../PLAN.md` from `tasks/` and verify plan membership. State the selected task. Resume unfinished implementation or review corrections. If the result waits for human review, do not make more changes without feedback. Do not skip blocked work.
2. Require approval of the applicable spec, plan, and task content. Require completed dependencies and passed preceding stage checkpoints. Resolve material open questions before implementation. If approval is missing, hand off to `to-spec` or `to-tasks` as applicable and stop.
3. Implement only the selected task. Run task and repository checks. Run the stage or plan checkpoint when this task completes it. Report existing failures and require no new failures.
4. Record changes, check results, remaining work, and review notes in the task. When acceptance criteria pass, return the result for human review. Mark the task complete and check its plan checkbox only after human acceptance. Stop after one task.

## Review feedback

- Review all feedback before changing code or handing off. Evaluate each comment instead of applying it automatically.
- Challenge feedback when a clearly better approach exists, when the requested change would reduce performance, quality, maintainability, correctness, or security, or when it conflicts with established project conventions or official documentation. Explain the tradeoff, recommend the better approach, and ask the human to choose before implementation.
- If comments conflict, identify the conflicting comments and incompatible outcomes, recommend one outcome, and ask the human to choose before implementation.
- Code correction: If the feedback is consistent with the approved task, the correction request authorizes the fix. Repeat affected checks and return to human review.
- Plan or task change: Stop affected implementation. Hand off to `to-tasks`. Resume after approval.
- Spec change: Stop affected implementation. Hand off to `to-spec`, then `to-tasks` for affected planning changes. Resume after all affected changes are approved.

Resume only the authorized task. Acceptance does not authorize the next task.

This skill may update implementation results, check results, review notes, task status, and plan checkboxes. Changes to task, plan, or spec meaning belong to the owning skill.

Never change requirements or acceptance criteria to make existing code pass. If a required skill is unavailable, report it and stop the affected work.
