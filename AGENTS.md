# Repository Rules

These rules are mandatory for all skill changes.

## Writing style

Use [ste-writing-skill](personal/ste-writing-skill/SKILL.md) for all explanations, documentation, comments, and user-facing text. Apply the skill to frontmatter descriptions, instructions, reference files, and templates.

Before you complete a skill change, review all changed prose against the skill.

## Skill dependencies

Keep skill dependencies in an acyclic graph. Do not add direct or indirect circular dependencies between skills.

Count invocations and references in supporting files and templates as dependencies of their owning skill. Keep each dependency independent of its callers and their artifacts.

Keep artifact definitions and lifecycle rules in the skill that owns the artifact. Keep shared rules independent of callers. Use a dependency or a plain reference file for shared rules without a return dependency.

Keep the planning direction: `senior` → `staged-plan-tasks` → `plan-tasks`. `senior` can also use `plan-tasks` directly.

Before you complete a skill change, examine its direct and indirect dependencies for cycles.
