# Plan Skeleton

Template for `PLAN.md`. Follow [`PLANS.md`](PLANS.md). Keep Purpose, Progress, and Validation and Acceptance; include other sections only when they contain current information.

    # <Plan responsibility>

    Current task: <NN-slug | approved concurrent set | none>
    State: <state from PLANS.md>
    Remaining: <exact next action or approval>
    Method: <repository-relative path to PLANS.md, only when checked in>

    ## Purpose / Big Picture

    State the focused end-to-end plan outcome, scope boundary, and exclusions.

    ## Progress

    Map every task; create detailed files only for the next task, approved concurrent set, and earlier tasks. Check a box only after result acceptance. The fields above select the resume action.

    - [ ] 01 <slug> — Outcome: <observable behavior>.
      Scope: <bounded implementation concern and relevant exclusions>.
      Owner and write paths: <sole owner; disjoint paths for concurrency>.
      State: <task state from PLANS.md>.
      Dependencies: <accepted predecessor outcome or none; required approved contracts>.
      Agreements: <governing parent IDs or anchors; canonical references>.
      Acceptance: <IDs>.

    ## Context and Contracts

    Repository-relative paths, canonical symbols, and glossary pointers shared by tasks. Define contracts up front where they constrain decomposition, and approve all required shared contracts before dependent implementation; add accepted implementation contracts as they become available. Assign shared constraints to all applicable tasks in Progress.

    ## Plan State and Current Decisions

    Record plan state, approved concurrent set (if any), ownership of shared files and integration, decomposition checks/exceptions, and task dependencies. Decisions or discoveries that still govern multiple tasks, including future obligations and unresolved questions. Give consequential decisions stable IDs or named anchors. Keep each at its canonical scope; link canonical agreements and repository contracts instead of copying them.

    - D001: <current choice>.
      Rationale: <only what affects implementation or prevents a mistake>.
      Approval: <scope and recorded approval, when needed>.

    ## Accepted Handoffs

    Record each accepted result's handoff as defined in PLANS.md Current instructions and history.

    ## Validation and Acceptance

    Define stable acceptance IDs and observable scenarios. Map every governing agreement and acceptance ID to tasks, including shared constraints. Assign assembled-behavior validation and cross-task checks to an explicit task; validation commands live in task briefs.

    ## Audit References

    Direct repository-relative file and ID/anchor pointers to decision history and shipped evidence, following PLANS.md Current instructions and history. Record the preservation-check result here when compacting the PLAN.
