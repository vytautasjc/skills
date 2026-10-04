# Task Skeleton

Template for `tasks/NN-slug.md`. Follow [PLANS.md](PLANS.md), including decomposition, size review, preservation, and explicit state. Resumable without conversation history, using explicit references to governing agreements and repository sources. Use these six compact sections.

    # Task NN — <responsibility>

    Current task: <NN-slug>
    State: <task state from PLANS.md>
    Remaining: <exact next action or approval>
    Parent: <repository-relative PLAN path>

    ## Outcome and scope

    State the task's bounded result and exclusions needed to prevent scope expansion. Cite its governing agreement and acceptance IDs; name its portion of scenarios spanning tasks.

    ## Owned paths and implementation area

    Name the sole owner and explicit write paths. State the backend, frontend, shared-contract, or integration boundary and who owns each shared file. Read dependencies do not grant write ownership. Record any invalid-intermediate-state exception and its reason.

    ## Required contracts and dependencies

    Reference every governing agreement by repository path and stable ID, symbol, or anchor: applicable invariants and terms, parent decisions, required approved shared contracts, accepted handoffs, and relevant source. State predecessor outcomes and approval status. Keep local contracts here only when they have no other canonical home.

    ## Implementation steps

    Give minimal ordered work by file/module. Keep edit commands beside their steps, with repository-relative working directory and expected result. Define or directly reference validation procedures using PLANS.md Acceptance and evidence. Keep recovery instructions beside risky work. Compact completed edit instructions while retaining validation procedure definitions or their direct pointers.

    ## Acceptance and validation

    For each acceptance ID/portion, give the behavior, agreed test seam, stable procedure reference, latest result, date, and tested revision or uncommitted-tree description. Apply PLANS.md Acceptance and evidence to the task boundary. Mark invalid evidence and required reruns in remaining work.

    ## Current status and remaining work

    Record planning approval, result-review state, acceptance or reopening, unresolved obligations, and granular remaining work. Preserve scope-review and preservation-check conclusions; link history records as defined in PLANS.md Current instructions and history.

    - [x] <completed work and evidence reference>.
    - [ ] <remaining action, validation, or approval>.

    On acceptance, reference the parent handoff.
