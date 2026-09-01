# Task Skeleton

Structural template for a child task file (`tasks/NN-slug.md`). The method and rules governing these sections live in [`PLANS.md`](PLANS.md); start a new task from this template and flesh it out, keeping every section.

    # Task NN — <slug>

    This task is a living document. The sections `Progress`, `Surprises & Discoveries`, `Decision Log`, and `Outcomes and Retrospective` must be kept up to date as work proceeds.

    ## Purpose

    Explain in a few sentences what someone gains after this task is completed and how they can see it working. State the user-visible behavior you will enable.

    ## Context

    What this task needs that the parent plan does not already give: the specific files, types, and terms in play for this task. Name files by their complete repository-relative paths. Keep it to this task.

    ## Plan of Work

    Describe, in prose, the sequence of edits and rationale. For each edit, name the file and location (function, module) and what to insert or change. Keep it concrete and minimal.

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

    Be prescriptive. Name the libraries, modules, and services to use and why. Specify the types, traits/interfaces, and function signatures that must exist at the end of the task. Prefer stable names and paths such as `crate::module::function` or `package.submodule.Interface`. E.g.:

    In crates/foo/planner.rs, define:

        pub trait Planner {
            fn plan(&self, observed: &Observed) -> Vec<Action>;
        }

    ## Outcomes and Retrospective

    Summarize outcomes, gaps, and lessons learned at completion. Compare the result against the original purpose.
