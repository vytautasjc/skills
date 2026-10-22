# Skills
Collection of personal agent skills.

Skill dependencies form an acyclic graph: skills reference their dependencies, while dependencies remain independent of their callers.

The planning hierarchy is `to-spec` → `to-tasks` → `implement-task`, from top to bottom. References point from bottom to top.

## Spec Driven Development skills

`grill-with-docs` → `to-spec` → `to-tasks` → `implement-task`

1. Use [grill-with-docs](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs) to clarify requirements and decisions. Confirm the shared understanding.
2. Use [to-spec](./personal/to-spec/SKILL.md) to turn the agreed conversation into a spec. Review and approve the spec.
3. Use [to-tasks](./personal/to-tasks/SKILL.md) to split the approved spec into an implementation plan and small, verifiable tasks. Tasks use vertical slices. Review and approve the plan and task files.
4. Use [implement-task](./personal/implement-task/SKILL.md) with a task file, plan file, or plan directory. Implement one task. Review the code and validation evidence. Explicitly accept the result before the task becomes done.

For plan input, the agent selects the first unfinished task in plan order. The agent resumes an active task or waits for its review. It does not skip blocked tasks or start the next task after acceptance.

The document skills permit implicit invocation. When result review requires a spec change, the agent uses `to-spec` and waits for spec approval. It then uses `to-tasks` and waits for plan and task approval. A change limited to the plan or tasks uses `to-tasks` directly. Code corrections under unchanged requirements return to human result review. Changes to accepted work use new tasks and preserve earlier acceptance records.

Approval evidence and result review notes remain in the files. Plan checkboxes record task completion. Skill dependencies remain in one direction: `implement-task` → `to-tasks` → `to-spec`. The execution skill can also use `to-spec` directly.

```text
/implement-task docs/features/registration/tasks/01-register.md
/implement-task docs/features/registration/PLAN.md
/implement-task docs/features/registration/
```

### Installation

```sh
npx skills add vytautasjc/skills --skill to-spec to-tasks implement-task
```