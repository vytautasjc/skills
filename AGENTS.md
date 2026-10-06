# Repository Rules

These rules are mandatory for all skill changes.

## Communication

Use ASD-STE100 Simplified Technical English for:
- user communication
- specifications
- implementation plans
- task descriptions
- documentation
- skills

Use concise text, but keep all required information.
Keep the source meaning, requirements, and constraints unchanged when you revise prose.

- Use short, direct sentences with one instruction or idea each.
- Use active voice and explicit subjects and objects.
- Use common words and consistent terms.
- Use pronouns only when their references are clear.
- Remove unnecessary words.
- Use literal language. Do not use idioms or slang.

Keep code identifiers, API names, commands, paths, and state values unchanged.
Keep error messages, quoted text, and established technical terms unchanged.

Do not apply these language rules to text that must remain verbatim.
If the user requests another language, use that language instead.

## Skill dependencies

Keep skill dependencies in an acyclic graph. Do not add direct or indirect circular dependencies between skills.

Count invocations and references in supporting files and templates as dependencies of their owning skill. Keep each dependency independent of its callers and their artifacts.

Keep artifact definitions and lifecycle rules in the skill that owns the artifact. Keep shared rules independent of callers. Use a dependency or a plain reference file for shared rules without a return dependency.

Keep the planning direction: `senior` → `staged-plan-tasks` → `plan-tasks`. `senior` can also use `plan-tasks` directly.

Before you complete a skill change, examine its direct and indirect dependencies for cycles.
