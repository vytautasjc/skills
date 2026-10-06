# Skills
Collection of personal agent skills together with their [third-party](#third-party-skills) dependencies.

Skill dependencies form an acyclic graph: skills reference their dependencies, while dependencies remain independent of their callers.

The planning hierarchy is `senior` → `staged-plan-tasks` → `plan-tasks`, from top to bottom. References point downward; `senior` may also route standalone work directly to `plan-tasks`. Each layer is usable without the layers above it.

## Spec and task workflow

`grilling` → `to-spec` → `to-tasks` → `implement-task`

1. Use [grilling](./third-party/grilling/SKILL.md) to clarify requirements and decisions. Confirm the shared understanding.
2. Use [to-spec](./personal/to-spec/SKILL.md) to turn the agreed conversation into a spec. Review and approve the spec.
3. Use [to-tasks](./personal/to-tasks/SKILL.md) to split the approved spec into an implementation plan and small, verifiable tasks. Tasks use vertical slices. Review and approve the plan and task files.
4. Use [implement-task](./personal/implement-task/SKILL.md) with a task file, plan file, or plan directory. Implement one task. Review the code and validation evidence. Explicitly accept the result before the task becomes done.

For plan input, the agent selects the first unfinished task in plan order. The agent resumes an active task or waits for its review. It does not skip blocked tasks or start the next task after acceptance.

The document skills permit implicit invocation. When result review requires a spec change, the agent uses `to-spec` and waits for spec approval. It then uses `to-tasks` and waits for plan and task approval. A change limited to the plan or tasks uses `to-tasks` directly. Code corrections under unchanged requirements return to human result review. Changes to accepted work use new tasks and preserve earlier acceptance records.

Approval evidence and result review notes remain in the files. Plan checkboxes record task completion. Skill dependencies remain in one direction: `implement-task` → `to-tasks` → `to-spec`. The execution skill can also use `to-spec` directly.

```text
$implement-task docs/features/registration/tasks/01-register.md
$implement-task docs/features/registration/PLAN.md
$implement-task docs/features/registration/
```

### Installation

```sh
npx skills add vytautasjc/skills --skill grilling to-spec to-tasks implement-task
```

## [setup-senior-skill](./personal/setup-senior-skill/SKILL.md)

Checks whether a repository has `senior` and its phase skills installed, reports missing skills by affected phase, then recommends the repository-level `AGENTS.md` guidance for using that workflow. This skill is available only when explicitly invoked.

### Installation

```sh
npx skills add vytautasjc/skills --skill setup-senior-skill
```

## [plan-tasks](./personal/plan-tasks/SKILL.md)

Plan Tasks is a skill heavily inspired by [Codex Exec Plans](https://developers.openai.com/cookbook/articles/codex_exec_plans) to create local feature scoped plans split into smaller tasks. Works wonderfully together with [grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling) skill to keep you in the driving seat while planning.

Approve the task map, then detail, approve, implement, and review one task before detailing its successor. Future tasks keep their agreed outcomes, scope boundaries, dependencies, and acceptance IDs in the map. Explicit state and remaining work support resume across sessions; accepted contracts pass through short parent handoffs. Start the next task in a fresh conversation to bound earlier context.

### Installation

```sh
npx skills add vytautasjc/skills --skill plan-tasks
```

### Example

<details>
<summary>💬 Input</summary>

```sh
codex >  $plan-tasks Update AGENTS.md with security guidelines

• I’m using the explicitly requested plan-tasks skill. I’ll inspect the repository guidance and planning templates, then create only the task map and stop at the Map gate—no security-guideline edits yet.

[...]

The task map is ready in docs/plans/agents-security-guidelines/PLAN.md.

  It contains one independently reviewable task:

  - 01 security-guidelines — add concise, actionable, repository-wide security rules to root AGENTS.md, then validate the documentation diff.

  The existing uncommitted AGENTS.md change is explicitly preserved. No security-guideline edits have been made yet.

  Map gate: Please approve the single-task breakdown and ordering. After approval, I’ll detail task 01 and stop at its Plan gate.

codex > ok

[...]
```
</details>

<details>
<summary>📦 Output</summary>

```sh
docs/plans
└── agents-security-guidelines
    ├── PLAN.md
    └── tasks
        └── 01-security-guidelines.md
```

</details>

## [staged-plan-tasks](./personal/staged-plan-tasks/SKILL.md)

Staged Plan Tasks is built on top of [plan-tasks](#plan-tasks) to tackle broader tasks, large features composed of multiple tasks.

The SPEC retains the complete agreed outcome, and the ROADMAP maps it to small stages, each delivering one responsibility end-to-end. Tasks own bounded implementation areas within a stage; backend and frontend work are separate tasks. Decompose and accept a stage using its complete SPEC coverage; execute each task using its assigned agreements, required contracts, invariants, and terms. Detail the next task just in time, or the small approved set intended for concurrent work, then accept the assembled stage before planning the next. Compaction preserves every agreement in a canonical home with explicit references.

### Installation

```sh
npx skills add vytautasjc/skills --skill plan-tasks staged-plan-tasks
```

### Example

<details>
<summary>💬 Input</summary>

```sh
codex > $staged-plan-tasks Limit authentication requests and show browser users when to retry. Also cap API request body sizes.

• I’m using staged-plan-tasks. I’ll capture the agreed behavior in the SPEC and map focused stages in the ROADMAP.

[...]

• Created docs/plans/api-request-limits/SPEC.md and ROADMAP.md.

  Proposed stages:

  1. authentication-rate-limiting — excess authentication requests return HTTP 429 with Retry-After, and the browser shows when the user can retry.
  2. request-body-limits — oversized API request bodies receive the agreed rejection response.

  Roadmap/Spec gate: Approve the agreed limits, rejection behavior, and two-stage coverage map. Then I’ll map Stage 01’s tasks.

codex > ok

• Stage 01’s task map is ready in docs/plans/api-request-limits/stages/01-authentication-rate-limiting/PLAN.md.

  - 01 backend-enforcement — enforce the authentication limit and validate HTTP rejection and recovery behavior.
  - 02 browser-retry-handling — show retry guidance using the backend’s accepted response contract; validate the UI against controlled API responses.

  Stage 01 acceptance will verify the assembled browser/API behavior. Task 02 depends on Task 01’s accepted contract. Stage 02 remains a ROADMAP entry.

  Stage 01 Map gate: Approve the task boundaries and order. Then I’ll detail Task 01.

codex > ok

[...]

• Task 01’s execution brief is ready in docs/plans/api-request-limits/stages/01-authentication-rate-limiting/tasks/01-backend-enforcement.md.

  It owns backend enforcement, the HTTP 429 and Retry-After response contract, and behavioral validation against the agreed SPEC acceptance IDs. Browser behavior belongs to Task 02.

  Task 01 Plan gate: Approve this brief to implement Task 01. After its result is accepted and continuation is authorized, I’ll detail Task 02 using the accepted contract.

codex > ok

[...]
```
</details>

<details>
<summary>📦 Output</summary>

Artifacts at Task 01’s Plan gate. Future tasks and stages remain mapped in PLAN.md and ROADMAP.md.

```sh
docs/plans/api-request-limits
├── SPEC.md
├── ROADMAP.md
└── stages
    └── 01-authentication-rate-limiting
        ├── PLAN.md
        └── tasks
            └── 01-backend-enforcement.md
```
</details>

## [senior](./personal/senior/SKILL.md)

Senior is a routing skill that is build on top of [plan-tasks](#plan-tasks), [staged-plan-tasks](#staged-plan-tasks), and third party skills.

It can be used for planning, implementation, code review. And it is made to follow plans made using the skills mentioned before.

Load skills by phase, with the governing planning skills also required when executing, reviewing results, or resuming a plan. Add ponytail and TDD for implementation and code review, domain modeling when meaning changes, and grilling for unresolved decisions. A missing skill blocks only the work requiring it. Resuming approved work uses its recorded state and remaining obligations.

Keep every governing agreement in a durable, identifiable canonical home. Compact task briefs reference current contracts; superseded decisions retain directly linked history records with replacement, rationale, approval, and affected contracts or evidence. A preservation check precedes compaction. Git history keeps ordinary edits, while agreed decisions remain directly retrievable.

### Installation

With dependency snapshots:
```sh
npx skills add vytautasjc/skills --skill plan-tasks staged-plan-tasks tdd ponytail grilling domain-modeling senior
```

With newest dependency versions:
```sh
npx skills add mattpocock/skills --skill tdd grilling domain-modeling

npx skills add dietrichgebert/ponytail --skill ponytail

npx skills add vytautasjc/skills --skill plan-tasks staged-plan-tasks senior
```

### Example

<details>
<summary>💬 Input</summary>

```sh
codex > $senior Let's implement a dummy API endpoint that returns 200 OK. Interview me    

• I’m using the senior workflow because you named it. I’ll load plan-tasks for this milestone and grilling for the interview. Implementation will load ponytail and TDD after the task plan is approved.

• The API already exposes GET /internal/health, which returns 200 with { "status": "ok" }.

  Does the caller require a distinct URL, or could the existing health route satisfy the need?

  My recommendation: reuse /internal/health unless /internal/dummy is itself part of the required contract; a second behavior-free success route otherwise adds no capability.

codex > ok

[...]

```
</details>

## Third-Party Skills

- [mattpocock/skills/domain-modeling](./third-party/domain-modeling/UPSTREAM.md)
- [mattpocock/skills/grilling](./third-party/grilling/UPSTREAM.md)
- [mattpocock/skills/tdd](./third-party/tdd/UPSTREAM.md)
- [DietrichGebert/skills/ponytail](./third-party/ponytail/UPSTREAM.md)
