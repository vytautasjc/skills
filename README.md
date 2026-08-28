# Skills
Collection of personal agent skills together with their [third-party](#-third-party-skills) dependencies.

## [plan-tasks](./personal/plan-tasks/SKILL.md)

Plan Tasks is a skill heavily inspired by [Codex Exec Plans](https://developers.openai.com/cookbook/articles/codex_exec_plans) to create local feature scoped plans split into smaller tasks. Works wonderfully together with [grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling) skill to keep you in the driving seat while planning.

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
```
</details>

<details>
<summary>📦 Output</summary>

```sh
docs/plans
└── agents-security-guidelines
    └── PLAN.md
```

</details>

## [staged-plan-tasks](./personal/staged-plan-tasks/SKILL.md)

Staged Plan Tasks is built on top of [plan-tasks](#-plan-tasks) to tackle broader tasks, large features composed of multiple tasks.

### Installation

```sh
npx skills add vytautasjc/skills --skill plan-tasks staged-plan-tasks
```

### Example

<details>
<summary>💬 Input</summary>

```sh
codex > $staged-plan-tasks Update AGENTS.md with security guidelines. Update existing backend api code according to these guidelines.

• I’m using staged-plan-tasks as requested, with the repository’s senior workflow governing this planning phase. I’ll inspect the backend and planning conventions, then create only the lean roadmap and stop at the required Roadmap gate—no stage implementation yet.

[...]

• I’ve scoped this as two milestones.

• Created the docs/plans/api-security-hardening/ROADMAP.md.

  The proposed delivery order is:

  1. secure-api-baseline — add shared and API-specific security guidelines, then enforce safe production configuration, trusted browser origins, security headers, and HTTP input limits.
  2. hardened-sessions-and-auth-endpoints — protect Dummy User login/session/logout against cross-site requests and automated abuse, harden cookies, and prevent reusable session credentials from being stored in PostgreSQL.
  
  Roadmap gate: Please approve the two-stage breakdown and order. Once approved, I’ll plan Stage 01 and stop at its Map gate before detailing tasks or changing source code.

codex > ok

• Roadmap approved. I’m now applying plan-tasks to Stage 01 only: I’ll map its vertical tasks, add the stage plan pointer to the roadmap, and stop at the Stage 01 Map gate before detailing any task or editing guidelines/source.

[...]

  Stage 01 Map gate: Approve this task breakdown and order, and I’ll detail Task 01 only.

codex > ok

[...]

• Task 01 is fully detailed in docs/plans/api-security-hardening/stages/01-secure-api-baseline/tasks/01-secure-runtime-contract.md.

  Key decisions:

  - Production rejects Dummy User login and non-HTTPS API/frontend URLs.
  - Root AGENTS.md gains cross-cutting security rules.
  - No dependencies, database schema, routes, sessions, or OAuth semantics change in this task.

  No source or AGENTS.md changes have been made yet.

  Task 01 Plan gate: Approve this task plan, and I’ll detail Task 02. All Stage 01 tasks must pass their individual Plan gates before implementation begins.

codex > ok

[...]
```
</details>

<details>
<summary>📦 Output</summary>

```sh
docs/plans/api-security-hardening
├── ROADMAP.md
└── stages
    ├── 01-secure-api-baseline
    │   ├── PLAN.md
    │   └── tasks
    │       ├── 01-secure-runtime-contract.md
    │       ├── 02-trusted-browser-boundary.md
    │       └── 03-bounded-http-input.md
    └── 02-hardened-sessions-and-auth-endpoints
        ├── PLAN.md
        └── tasks
            ├── 01-harden-auth-endpoints.md
            └── 02-improve-session-handling.mdp
```
</details>

## [senior](./personal/senior/SKILL.md)

Senior is a routing skill that is build on top of [plan-tasks](#-plan-tasks), [staged-plan-tasks](#-staged-plan-tasks), and third party skills.

It can be used for planning, implementation, code review. And it is made to follow plans made using the skills mentioned before.

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

• I’m using the senior workflow because you named it. Since you asked for an interview, I’ll first load its required planning, grilling, simplicity, TDD, and domain-language gates; then I’ll ask one focused question at a time before we write or change anything.

• The API already exposes GET /internal/health, which returns 200 with { "status": "ok" }.

  Does the caller require a distinct URL, or could the existing health route satisfy the need?

  My recommendation: reuse /internal/health unless /internal/dummy is itself part of the required contract; a second behavior-free success route otherwise adds no capability.

codex > ok

[...]

```
</details>

## Third-Party Skills

- [mattpocock/skills/domain-modeling](./third-party/domain-modeling/UPSTREAM.md)
- [mattpocock/skills/grill-with-docs](./third-party/grill-with-docs/UPSTREAM.md)
- [mattpocock/skills/grilling](./third-party/grilling/UPSTREAM.md)
- [mattpocock/skills/tdd](./third-party/tdd/UPSTREAM.md)
- [DietrichGebert/skills/ponytail](./third-party/ponytail/UPSTREAM.md)