# Task Skeleton

Structural template for `tasks/NN-slug.md`. Follow [`PLANS.md`](PLANS.md). Keep required sections, but add no filler or placeholder prose; one sentence is enough when it fully communicates the point.

    # Task NN — <slug>

    Living task: keep `Progress`, `Surprises & Discoveries`, `Decision Log`, and `Outcomes and Retrospective` current.

    ## Purpose

    State what becomes possible and how to observe it. Use one sentence when sufficient.

    ## Context

    What this task needs that the parent plan does not already give: the specific files, types, and terms in play for this task. Name files by their complete repository-relative paths. Keep it to this task.

    ## Plan of Work

    Give the minimal sequence of edits. Name each file and location (function or module), the change, and only rationale that affects implementation.

    ## Concrete Steps

    State the exact commands to run and where to run them, expressing every working directory relative to the repository root. When a command generates output, show a short expected transcript so the reader can compare. This section must be updated as work proceeds.

    ## Validation / Acceptance

    How to prove this solution works as behavior a human can verify — exact commands or tests with the working directory, and the output to expect. State the test that fails before and passes after. This is what you show at the result gate.

    ## Surprises & Discoveries

    Document unexpected behaviors, bugs, optimizations, or insights discovered during implementation. Provide concise evidence.

    - Observation: …
      Evidence: …

    ## Decision Log

    Record every decision made while working on this task in the format:

    - Decision: …
      Rationale: …
      Date/Author: (2025-10-01 13:00Z) / <git username>

    ## Progress

    Granular checklist for resuming this task mid-flight. Split a partially done item into done vs remaining. The root plan's `Progress` tracks coarse status; this tracks the work inside the task.

    - [x] (2026-06-20 13:00Z) Example completed step.
    - [ ] Example remaining step (completed: X; remaining: Y).

    ## Interfaces and Dependencies

    Include only dependencies and interfaces that constrain implementation. Name required libraries, modules, services, types, and signatures, with rationale only where the choice is non-obvious. Prefer stable names and paths such as `crate::module::function` or `package.submodule.Interface`. Example when useful:

    In crates/foo/planner.rs, define:

        pub trait Planner {
            fn plan(&self, observed: &Observed) -> Vec<Action>;
        }

    ## Outcomes and Retrospective

    Summarize outcomes, gaps, and lessons learned at completion. Compare the result against the original purpose.
