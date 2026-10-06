---
name: setup-senior-skill
description: Examine the repository's senior skill installation and recommend AGENTS.md workflow guidance.
---

# Setup Senior Skill

Audit the current repository only. Use the [Vytautas skills README](https://github.com/vytautasjc/skills#readme) as the installation source of truth.

## Examine the installation

1. Find the repository root. Find repository-local skills by the `name` in each `SKILL.md` frontmatter. Search hidden agent directories. Exclude `.git`. Count only skills in the repository.
2. Look for `senior` and its phase skills: `plan-tasks`, `staged-plan-tasks`, `ponytail`, `domain-modeling`, `grilling`, and `tdd`.
3. If `senior` is present, read its `Phase loading` table. For an earlier installation, use `Prerequisites`. If its skill selection rules differ, use those rules. Count a skill as installed only if its `SKILL.md` is present in the repository.

If `senior` is missing, ask the user to follow the README's installation instructions before you recommend guidance.
If a phase skill is missing, list the skill and affected phase. Other installed phases remain usable.
Recommend installation of missing skills from the README. Continue the guidance review for the installed router.

## Recommend repository guidance

Once `senior` is installed, examine the root `AGENTS.md`. Recommend the following block without changes.
Edit the file only if the user asks for the change:

```markdown
## Engineering Workflow

Use the `senior` skill for complex engineering work. Follow its skill selection rules and approval gates.
```

If the file does not exist, recommend a new file with this block.
If an `Engineering Workflow` section exists, show how to add the guidance to that section.
If the guidance is already present, report that no `AGENTS.md` change is necessary.

Finish with a short status: installed skills, missing skills, and the proposed `AGENTS.md` action.
