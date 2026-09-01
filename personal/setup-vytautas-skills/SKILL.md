---
name: setup-vytautas-skills
description: Check a repository's Vytautas skills installation and recommend its AGENTS.md workflow setup.
---

# Setup Vytautas Skills

Audit the current repository only. Treat the [Vytautas skills README](https://github.com/vytautasjc/skills#readme) as the installation source of truth.

## Check the installation

1. Resolve the repository root and find repository-local skills by the `name` in each `SKILL.md` frontmatter. Include hidden agent directories in the search and exclude `.git`. Do not count user-level or globally installed skills.
2. Check for `senior` and its expected prerequisites: `plan-tasks`, `staged-plan-tasks`, `ponytail`, `domain-modeling`, `grilling`, and `tdd`.
3. When `senior` is present, read its `Prerequisites` section and use that list instead if it differs. A skill is installed only when its `SKILL.md` is present in the repository.

If `senior` or any prerequisite is missing, list the missing skill names and ask the user to follow the README's installation instructions first. Stop before recommending an `AGENTS.md` change because the workflow is not ready to reference.

## Recommend repository guidance

Once `senior` and every prerequisite are installed, inspect the root `AGENTS.md`. Recommend adding the following block verbatim; do not edit the file unless the user separately asks for the change:

```markdown
## Engineering Workflow

Follow the `senior` skill — it routes each phase of non-trivial work (plan · domain language · implement · review) to
the repo's skills and gates.
```

If the file does not exist, recommend creating it with this block. If it already has an `Engineering Workflow` section, show a merge into that section instead of proposing a duplicate heading. If the guidance is already present, report that no `AGENTS.md` change is needed.

Finish with a compact status: installed skills, missing skills, and the proposed `AGENTS.md` action.
