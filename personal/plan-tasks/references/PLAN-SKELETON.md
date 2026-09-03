# Plan Skeleton

Structural template for a `PLAN.md`. Follow [`PLANS.md`](PLANS.md). Keep required sections, but add no filler or placeholder prose; one sentence is enough when it fully communicates the point.

    # <Short, action-oriented description>

    Living plan: keep `Progress`, `Surprises & Discoveries`, `Decision Log`, `Outcomes`, and `Retrospective` current.

    Method: <repository-relative path to PLANS.md, only when checked in>

    ## Purpose / Big Picture

    State what becomes possible and how to observe it. Use one sentence when sufficient.

    ## Progress

    The delivery sequence of tasks. One line per task: status box, completion timestamp, number, slug, and one-line scope. This is the resume index and the only place coarse status is tracked. This section must always reflect the actual current state of the work.

    - [x] (2026-06-20 13:00Z) 00 example — completed task looks like this
    - [ ] 01 config — load environment, config
    - [ ] 02 prisma — database and migrations

    ## Surprises & Discoveries

    Capture optimizer behavior, performance tradeoffs, unexpected bugs, or insights that shaped the approach across tasks, with short evidence (test output is ideal).

    - Observation: …
      Evidence: …

    ## Decision Log

    Record every decision made that affects this plan's tasks while working on the plan in the format:

    - Decision: …
      Rationale: …
      Date/Author: (2025-10-01 13:00Z) / <git username>

    ## Outcomes

    Summarize outcomes, gaps, and lessons learned of each child task for further tasks to be able to pick up and use without needing to read specific task file. This section should read as usage instruction for further task implementation work.

    ## Retrospective
    
    Summarize general outcome, gaps, and lessons learned at plan completion. Compare the result against the original purpose.

    ## Context and Orientation

    Give only the repository context needed to execute the plan: key repository-relative paths, how they connect, and definitions of non-obvious terms. Do not refer to prior plans.

    ## Validation and Acceptance

    Describe how to start or exercise the system and what to observe. Phrase acceptance as behavior, with specific inputs and outputs. If tests are involved, say "run <project’s test command> and expect <N> passed; the new test <name> fails before the change and passes after>".

    ## Idempotence and Recovery

    If steps can be repeated safely, say so. If a step is risky, provide a safe retry or rollback path. Keep the environment clean after completion.

    ## Artifacts and Notes

    Include this section only when concise transcripts, diffs, or snippets materially help the next agent. Keep entries focused on what proves success.
