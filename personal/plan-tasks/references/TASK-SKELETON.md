# Task Skeleton

Use this template for `tasks/NN-slug.md`. Use [PLANS.md](PLANS.md) for decomposition, size review, preservation, and explicit state. Make continuation possible without conversation history. Refer directly to applicable agreements and repository sources. Use these six short sections.

    # Task NN — <responsibility>

    Current task: <NN-slug>
    State: <task state from PLANS.md>
    Remaining: <specified next action or approval>
    Parent: <repository-relative PLAN path>

    ## Outcome and scope

    Write the task result and its boundary.
    Write exclusions necessary to control scope.
    Cite applicable agreement and acceptance IDs.
    Identify its portion of scenarios that span tasks.

    ## Owned paths and implementation area

    Identify the single owner and explicit write paths.
    Write the backend, frontend, shared-contract, or integration boundary.
    Identify the owner of each shared file.
    Read dependencies do not give write ownership.
    Write each exception for an invalid intermediate state and its reason.

    ## Required contracts and dependencies

    Refer to each applicable agreement by repository path and stable ID, symbol, or anchor.
    Include applicable invariants, terms, parent decisions, necessary approved shared contracts, accepted handoffs, and related source.
    Write predecessor outcomes and approval status.
    Keep local contracts here only if they have no other canonical location.

    ## Implementation steps

    Give the minimum ordered work by file or module.
    Put edit commands with their steps.
    Include the repository-relative working directory and expected result.
    Write validation procedures, or reference them directly, with PLANS.md Acceptance and evidence.
    Put recovery instructions with work with risk.
    Shorten completed edit instructions when appropriate.
    Keep validation procedures or direct references to them.

    ## Acceptance and validation

    For each acceptance ID or portion, write the behavior and agreed test seam.
    Give the stable procedure reference, latest result, date, and tested revision or description of uncommitted changes.
    For the task boundary, follow PLANS.md Acceptance and evidence.
    Identify invalid evidence and necessary reruns in remaining work.

    ## Current status and remaining work

    Write planning approval, result-review state, acceptance or reopening, open obligations, and detailed remaining work.
    Keep scope-review and preservation-check conclusions.
    Give history references with PLANS.md Current instructions and history.

    - [x] <completed work and evidence reference>.
    - [ ] <remaining action, validation, or approval>.

    After acceptance, refer to the parent handoff.
