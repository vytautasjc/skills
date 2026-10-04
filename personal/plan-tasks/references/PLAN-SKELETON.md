# Plan Skeleton

Use this template for `PLAN.md`. Use [`PLANS.md`](PLANS.md). Keep Purpose, Progress, and Validation and Acceptance. Include other sections only when they contain current information.

    # <Plan responsibility>

    Current task: <NN-slug | approved concurrent set | none>
    State: <state from PLANS.md>
    Remaining: <specified next action or approval>
    Method: <repository-relative PLANS.md path, only if stored in the repository>

    ## Purpose / Big Picture

    Write the plan outcome from start to end.
    Write its scope boundary and exclusions.

    ## Progress

    Map each task.
    Create detailed files only for the next task, approved concurrent set, and earlier tasks.
    Set a box to checked only after result acceptance.
    Use the fields above to select the resume action.

    - [ ] 01 <slug> — Outcome: <observable behavior>.
      Scope: <implementation concern with a clear boundary and applicable exclusions>.
      Owner and write paths: <single owner, with separate paths for concurrent work>.
      State: <task state from PLANS.md>.
      Dependencies: <accepted predecessor outcome or none, and necessary approved contracts>.
      Agreements: <applicable parent IDs or anchors and canonical references>.
      Acceptance: <IDs>.

    ## Context and Contracts

    Give repository-relative paths, canonical symbols, and glossary references shared by tasks.
    Write contracts before decomposition if they control task boundaries.
    Get approval for all necessary shared contracts before dependent implementation.
    Add accepted implementation contracts when they become available.
    Give shared constraints to each applicable task in Progress.

    ## Plan State and Current Decisions

    Write the plan state and the approved concurrent set, if applicable.
    Identify owners of shared files and integration.
    Write decomposition checks, exceptions, and task dependencies.
    Include decisions or findings that still control multiple tasks.
    Include future obligations and open questions.
    Give important decisions stable IDs or named anchors.
    Keep each decision at its canonical scope.
    Add references to canonical agreements and repository contracts.

    - D001: <current choice>.
      Rationale: <reason that affects implementation or prevents a mistake>.
      Approval: <scope and approval record, if necessary>.

    ## Accepted Handoffs

    Write each accepted result's handoff with PLANS.md Current instructions and history.

    ## Validation and Acceptance

    Write stable acceptance IDs and observable scenarios.
    Give each applicable agreement and acceptance ID to tasks.
    Include shared constraints.
    Give assembled-behavior validation and checks across tasks to an explicit task.
    Keep validation commands in task briefs.

    ## Audit References

    Give direct references to decision history and delivered evidence.
    Include the repository-relative file and ID or anchor.
    Use PLANS.md Current instructions and history.
    When you make the PLAN shorter, write the preservation-check result here.
