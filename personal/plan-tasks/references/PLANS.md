# Plan Tasks

This document describes the requirements for an execution plan, a design document that a coding agent can follow to deliver a working feature or system change. Treat the reader as a complete beginner to this repository: they have only the current working tree and the single execution plan file you provide. There is no memory of prior plans and no external context.

## How to use this file

When authoring an executable plan, follow this file _to the letter_. If it is not in your context, refresh your memory by reading the entire file. Be thorough in reading (and re-reading) source material to produce an accurate specification. When creating a plan, start from the relevant skeleton (`PLAN-SKELETON.md` for a plan, `TASK-SKELETON.md` for a task) and flesh it out as you do your research.

When discussing an executable plan, record decisions applicable to all child tasks in a log in the plan for posterity; it should be unambiguously clear why any change to the plan was made. These plans and child tasks are living documents, and it should always be possible to restart from _only_ the plan and its tasks and no other work.

When researching a design with challenging requirements or significant unknowns, use tasks to implement proof of concepts, "toy implementations", etc., that allow validating whether the user's proposal is feasible. Read the source code of libraries by finding or acquiring them, research deeply, and include prototypes to guide a fuller implementation.

## Requirements

NON-NEGOTIABLE REQUIREMENTS:

* Every Plan in combination with its child tasks must be fully self-contained. Self-contained means that in its current form it contains all knowledge and instructions needed for a novice to succeed.
* Every Plan and Task is a living document. Contributors are required to revise it as progress is made, as discoveries occur, and as design decisions are finalized. Each revision must remain fully self-contained.
* Every Plan must enable a complete novice to implement the feature end-to-end without prior knowledge of this repo.
* Every Plan must produce a demonstrably working behavior, not merely code changes to "meet a definition".
* Every Plan and Task must define every term of art in plain language or do not use it.
* Every Plan holds what every child task needs. The defining property: working on a task loads the lean parent plan plus that one task file.
* Every Task is defined in the same order they need to be done to achieve the plan's goal incrementally.
* Every Task is a vertical slice of one capability, never a horizontal layer. It delivers observable behavior end-to-end — cutting through every layer that capability touches, whatever layers the system has — rather than completing one layer for capabilities that land later. The single exception is a deliberately content-free task that introduces a shared mechanism with no capability content (a connection, a runtime, a framework, a test harness). See `## Tasks`.

Purpose and intent come first. Begin by explaining, in a few sentences, why the work matters from a user's perspective: what someone can do after this change that they could not do before, and how to see it working. Then guide the reader through the exact steps to achieve that outcome, including what to edit, what to run, and what they should observe.

The agent executing your plan can list files, read files, search, run the project, and run tests. It does not know any prior context and cannot infer what you meant from earlier milestones. Repeat any assumption you rely on. Do not point to external blogs or docs; if knowledge is required, embed it in the plan itself in your own words. If a Plan builds upon a prior Plan and that file is checked in, incorporate it by reference. If it is not, you must include all relevant context from that plan.

## Formatting

Format and envelope are simple and strict. Each Plan must be one single fenced code block labeled as `md` that begins and ends with triple backticks. Do not nest additional triple-backtick code fences inside; when you need to show commands, transcripts, diffs, or code, present them as indented blocks within that single fence. Use indentation for clarity rather than code fences inside a Plan to avoid prematurely closing the Plan's code fence. Use two newlines after every heading, use # and ## and so on, and correct syntax for ordered and unordered lists.

Omit optional sections when they do not add value. Do not include sections whose only content would be `N/A`.

When writing a Plan to a Markdown (.md) file where the content of the file *is only* the single Plan, you should omit the triple backticks.

Write in plain prose. Prefer sentences over lists. Avoid checklists, tables, and long enumerations unless brevity would obscure meaning. Checklists are permitted only in the `Progress` section, where they are mandatory. Narrative sections must remain prose-first.

Use only the sections defined in the relevant skeleton (`PLAN-SKELETON.md` or `TASK-SKELETON.md`). You may omit or combine those sections when the guidance allows, but must not add any section the skeleton does not define. If information does not fit an existing section, place it in the closest applicable one rather than introducing a new heading.

## Guidelines

Self-containment and plain language are paramount. If you introduce a phrase that is not ordinary English ("daemon", "middleware", "RPC gateway", "filter graph"), define it immediately and remind the reader how it manifests in this repository (for example, by naming the files or commands where it appears). Do not say "as defined previously" or "according to the architecture doc." Include the needed explanation here, even if you repeat yourself.

Avoid common failure modes. Do not rely on undefined jargon. Do not describe "the letter of a feature" so narrowly that the resulting code compiles but does nothing meaningful. Do not outsource key decisions to the reader. When ambiguity exists, resolve it in the plan itself and explain why you chose that path. Err on the side of over-explaining user-visible effects and under-specifying incidental implementation details.

Anchor the plan with observable outcomes. State what the user can do after implementation, the commands to run, and the outputs they should see. Acceptance should be phrased as behavior a human can verify ("after starting the server, navigating to [http://localhost:8080/health](http://localhost:8080/health) returns HTTP 200 with body OK") rather than internal attributes ("added a HealthCheck struct"). If a change is internal, explain how its impact can still be demonstrated (for example, by running tests that fail before and pass after, and by showing a scenario that uses the new behavior).

Specify repository context explicitly. Name files with full repository-relative paths, name functions and modules precisely, and describe where new files should be created. If touching multiple areas, include a short orientation paragraph that explains how those parts fit together so a novice can navigate confidently. When running commands, show the working directory and exact command line. When outcomes depend on environment, state the assumptions and provide alternatives when reasonable. Use repository-relative paths in the plan, never full system paths, unless an external absolute path is itself part of the required environment.

Be idempotent and safe. Write the steps so they can be run multiple times without causing damage or drift. If a step can fail halfway, include how to retry or adapt. If a migration or destructive operation is necessary, spell out backups or safe fallbacks. Prefer additive, testable changes that can be validated as you go.

Validation is not optional. Include instructions to run tests, to start the system if applicable, and to observe it doing something useful. Describe comprehensive testing for any new features or capabilities. Include expected outputs and error messages so a novice can tell success from failure. Where possible, show how to prove that the change is effective beyond compilation (for example, through a small end-to-end scenario, a CLI invocation, or an HTTP request/response transcript). State the exact test commands appropriate to the project’s toolchain and how to interpret their results.

Capture evidence. When your steps produce terminal output, short diffs, or logs, include them inside the single fenced block as indented examples. Keep them concise and focused on what proves success. If you need to include a patch, prefer file-scoped diffs or small excerpts that a reader can recreate by following your instructions rather than pasting large blobs.

## Tasks

Tasks are narrative, not bureaucracy. Introduce each with a brief paragraph that describes the scope, what will exist at the end of the task that did not exist before, the commands to run, and the acceptance you expect to observe. Keep it readable as a story: goal, work, result, proof. Progress and tasks are distinct: tasks tell the story, progress tracks granular work. Both must exist. Never abbreviate a task merely for the sake of brevity, do not leave out details that could be crucial to a future implementation.

Each task is a **vertical capability**: the smallest end-to-end slice that produces observable behavior for one capability, cutting through every layer that capability touches — whatever layers the system has, be it storage and interface, parser and evaluator, or input and output. It is independently *demonstrable* — you can run it and watch it work — which matters far more than a small diff. When vertical slicing and a smaller, easier-to-review commit conflict, slice vertically; a larger end-to-end task beats a tidy layer. Decompose by capability, never by layer: deliver one whole capability, then the next capability built on it — not one layer for every capability, then the next layer.

Each capability owns its own slice of every layer — the data, settings, interfaces, and tests it needs land in the task that introduces the capability, never in an earlier task. A task may introduce a shared **mechanism** — a runtime or storage connection, a configuration loader, a test harness, any capability-agnostic plumbing — but only the mechanism, never a specific future capability's **content**. Pre-building content for capabilities that land later (every data structure up front, every setting, every interface) is the horizontal layer to reject.

The litmus for a capability task: *can a human observe this task working without the next task existing?* If no, it is a layer — fold it into the slice that makes it observable. A mechanism task is the rare, deliberately content-free exception, justified only when wedging its plumbing into the first capability's slice would be unclean; it is demonstrable merely as the system starting up, connecting, or loading its configuration, with no domain behavior, and it must hold no capability's content.

A capability bundles all the layers it needs and is the unit; it is never split by layer. The next task is a new capability built on the shipped one, not the next layer of the same one. Only when a single capability is still too large to land in one task, thin it into a **walking skeleton** — the thinnest end-to-end path that still produces observable behavior — and let later tasks enrich along the same vertical. Splitting a capability into horizontal layers is never the fallback.

Tasks are still defined in the order they must be done to build the plan's goal incrementally, each one independently demonstrable.

## Living plans, tasks, and design decisions

### Plans

* Plans and tasks are living documents. As you make key design decisions, update the plan to record both the decision and the thinking behind it. Record all decisions in the plan's `Decision Log` section when they apply to all or multiple child tasks only. When updating a plan, never update a decision log entry, always add a new one.
* Plans must contain and maintain a `Progress` section, a `Surprises & Discoveries` section, a `Decision Log`, and an `Outcomes and Retrospective` section. These are not optional.
* When you discover optimizer behavior, performance tradeoffs, unexpected bugs, or inverse/unapply semantics that shaped your approach, capture those observations in the `Surprises & Discoveries` section with short evidence snippets (test output is ideal).
* If you change course mid-implementation, document why in the `Decision Log` and reflect the implications in `Progress`. Plans are guides for the next contributor as much as checklists for you.
* At completion of a major task or the full plan, write an `Outcomes and Retrospective` entry summarizing what was achieved, what remains, and lessons learned.

### Tasks

* Tasks are living documents. As you make key design decisions exclusive to the task, update the task to record both the decision and the thinking behind it. Record all decisions in the plan's `Decision Log` section when they apply to all or multiple child tasks only.
* Tasks must contain and maintain a `Progress` section, a `Surprises & Discoveries` section, and a `Decision Log` section. These are not optional.
* When you discover optimizer behavior, performance tradeoffs, unexpected bugs, or inverse/unapply semantics that shaped your approach, capture those observations in the `Surprises & Discoveries` section with short evidence snippets (test output is ideal).
* When a task-local observation proves cross-cutting — a convention or constraint later tasks must also honor — promote it to the parent plan's `Surprises & Discoveries` exactly as a cross-cutting decision is promoted to the `Decision Log`: the parent holds the full observation and the task keeps only a one-line pointer to it. Never leave the full observation in both places.
* If you change course mid-implementation, document why in the `Decision Log` and reflect the implications in `Progress`. Tasks are guides for the next contributor as much as checklists for you.

# Prototyping tasks and parallel implementations

It is acceptable—-and often encouraged—-to include explicit prototyping tasks when they de-risk a larger change. Examples: adding a low-level operator to a dependency to validate feasibility, or exploring two composition orders while measuring optimizer effects. Keep prototypes additive and testable. Clearly label the scope as “prototyping”; describe how to run and observe results; and state the criteria for promoting or discarding the prototype.

Prefer additive code changes followed by subtractions that keep tests passing. Parallel implementations (e.g., keeping an adapter alongside an older path during migration) are fine when they reduce risk or enable tests to continue passing during a large migration. Describe how to validate both paths and how to retire one safely with tests. When working with multiple new libraries or feature areas, consider creating spikes that evaluate the feasibility of these features _independently_ of one another, proving that the external library performs as expected and implements the features we need in isolation.

# Skeletons

The structural templates live in their own files so each operation loads only the one it needs: author or revise the parent plan from the plan skeleton, detail or execute a task from the task skeleton.

- Plan: [`PLAN-SKELETON.md`](PLAN-SKELETON.md) — the ordered sections of a `PLAN.md`.
- Task: [`TASK-SKELETON.md`](TASK-SKELETON.md) — the ordered sections of a `tasks/NN-slug.md`.

Start from the relevant skeleton and flesh it out. Use only the sections it defines; omit or combine them only where the guidance above allows, and never add a section the skeleton does not define. Several sections appear in both skeletons but carry deliberately different scope: a plan's `Progress` is the coarse task index and its `Decision Log` records only decisions affecting more than one task, while a task's `Progress` is the granular checklist for that task and its `Decision Log` records task-local decisions. Keep each in its own skeleton; do not collapse them.

# Important Notes

If you follow the guidance above, a single, stateless agent -- or a human novice -- can read your plan from top to bottom and produce a working, observable result. That is the bar: SELF-CONTAINED, SELF-SUFFICIENT, NOVICE-GUIDING, OUTCOME-FOCUSED.

When you revise a plan, you must ensure your changes are comprehensively reflected across all sections, including the living document sections, and child tasks, and you must write a note at the bottom of the plan describing the change and the reason why. Plan must describe not just the what but the why for almost everything that is applicable to all plan's tasks.
