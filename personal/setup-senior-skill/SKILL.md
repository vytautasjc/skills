---
name: setup-senior-skill
description: Check a repository's senior skill by vytautasjc installation and recommend its AGENTS.md workflow setup.
---

# Setup Senior Skill

Audit the current repository only. Treat the [Vytautas skills README](https://github.com/vytautasjc/skills#readme) as the installation source of truth.

## Check the installation

1. Resolve the repository root and find repository-local skills by the `name` in each `SKILL.md` frontmatter. Include hidden agent directories in the search and exclude `.git`. Do not count user-level or globally installed skills.
2. Check for `senior` and its phase skills: `plan-tasks`, `staged-plan-tasks`, `ponytail`, `domain-modeling`, `grilling`, and `tdd`.
3. When `senior` is present, read its `Phase loading` table and use that routing instead if it differs (use `Prerequisites` for a legacy installation). A skill is installed only when its `SKILL.md` is present in the repository.

If `senior` is missing, ask the user to follow the README's installation instructions before recommending guidance. If a phase skill is missing, list it and the affected phase; other installed phases remain usable. Recommend installing the missing skills from the README, and continue the guidance check for the installed router.

## Recommend repository guidance

Once `senior` is installed, inspect the root `AGENTS.md`. Recommend adding the following block verbatim; do not edit the file unless the user separately asks for the change:

```markdown
## Engineering Workflow

Follow the `senior` skill — it routes each phase of non-trivial work (plan · domain language · implement · review) to
the repo's skills and gates.
```

If the file does not exist, recommend creating it with this block. If it already has an `Engineering Workflow` section, show a merge into that section instead of proposing a duplicate heading. If the guidance is already present, report that no `AGENTS.md` change is needed.

Finish with a compact status: installed skills, missing skills, and the proposed `AGENTS.md` action.
