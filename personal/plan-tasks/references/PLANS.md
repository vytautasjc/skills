# Plan Tasks

An execution plan maps one responsibility delivered end-to-end to bounded implementation tasks. The lean parent PLAN, current task brief, and explicit repository references must make the work resumable without conversation history. Refer to source paths, tests, and canonical contracts instead of reproducing them.

## How to use this file

Read this reference when creating, revising, validating, executing, or resuming a plan. The [plan-tasks flow](../SKILL.md#flow) owns task sequencing and approval gates. Use `PLAN-SKELETON.md` for the parent and `TASK-SKELETON.md` for the current execution brief when authoring or restructuring them. Inspect the source needed for the current phase; future tasks remain a map until their turn.

## Current context and ownership

Every agreed requirement, constraint, contract, acceptance condition, and consequential decision has one durable, identifiable canonical home. The current task includes or explicitly references every agreement governing it. Compaction changes retrieval and presentation; it never silently deletes, weakens, or overrides agreed meaning.

- The PLAN owns the focused end-to-end outcome, ordered task map, acceptance coverage, shared implementation contracts, current decisions, and accepted handoffs needed later. Keep it lean; local detail belongs in the task or canonical repository references.
- The task owns its outcome and scope, write-path ownership, local contracts, implementation steps, validation, and remaining work. Load only the PLAN, that task, and required repository references.
- Promote any decision, discovery, or contract needed by another task to the parent or a canonical repository reference linked there. Leave a one-line pointer at the origin. Keep each meaning in one authoritative place.

Sibling task files open only to investigate a changed or failing **contract**: promised interfaces, types, or outcomes another task relies on. A plan revision, new requirement, scope change, or described outcome failing may trigger this exception. Cross-task influence otherwise uses current contracts and accepted handoffs in the PLAN or canonical contracts linked there.

Define unfamiliar terms at their canonical scope or point to the necessary glossary entries. Name files with repository-relative paths and functions or modules precisely. Explain how the relevant parts connect only when that helps implementation. Required knowledge must be available from the current repository and explicit references; conversations and sibling task rationale are not dependencies.

## Task map

Map all tasks before detailing any. Each map entry gives an observable outcome, scope boundary, dependencies, governing agreements, and acceptance IDs. PLANs define stable acceptance IDs such as `A001`. Assign shared constraints to every applicable task. Define shared contracts before the Map gate only when they constrain decomposition. All agreed future outcomes, boundaries, dependencies, acceptance references, and constraints remain in the PLAN or its canonical references and task map; only future implementation detail is deferred.

## Decomposition

Task: One bounded implementation responsibility within a plan. It owns a clear implementation area and has focused validation. It does not need to deliver the complete user journey independently.

Before approving a task map:

- Split backend and frontend implementation into separate tasks. Split tasks containing independently verifiable implementation concerns, including distinct backend concerns where appropriate.
- Define required shared contracts before dependent implementation begins. Map who establishes them and when they are approved.
- Assign one owner to each shared file and integration change. Create shared-contract and integration tasks only when they require actual work; name their acceptance responsibilities.
- Review oversized artifacts for duplicated content or scope that needs further splitting.

Allow a narrow exception only when splitting would leave an invalid intermediate state; record the reason and affected boundary. Sharing a feature, domain, application, or deadline is insufficient. A backend task may be accepted through HTTP behavior before the frontend exists; a frontend task may be accepted against controlled API responses.

For example, Google authentication can have shared authentication contracts (if actual work), backend authentication and Sessions, frontend sign-in/Session state/logout, and integration (if actual work). Apply the independent-concern check within those example areas rather than treating the example as a fixed task count.

A prototype task states the unknown, runnable experiment, and adoption criteria. Migration tasks define validation of coexisting paths and safe retirement.

## Parallel execution

Tasks may run concurrently only when their owned write paths do not overlap, their required contracts are approved, and neither depends on the other's unfinished implementation. Each agent receives only its task, governing agreements, required contracts, and relevant source context. Detail and approve that small set before starting; other tasks remain map entries. Record the set, each task's state, and the sole owner of shared files and integration in the PLAN. Serialize work if ownership cannot be made disjoint. Creating the set does not itself authorize delegation.

## Compact execution briefs

Use six sections: Outcome and scope; Owned paths and implementation area; Required contracts and dependencies; Implementation steps; Acceptance and validation; Current status and remaining work. Include exclusions where needed to prevent scope expansion. Include rationale only when it changes implementation or prevents a likely mistake. Local decisions and discoveries belong beside the contract or step they affect, rather than in separate mandatory logs.

Put setup, generation, and migration commands beside the steps they support. Validation procedures follow [Acceptance and evidence](#acceptance-and-evidence); Acceptance and validation references them and records expected and observed results without repeating commands. State each working directory relative to the repository root. Recovery instructions belong beside the risky step; spell out safe retry, backup, or rollback where necessary.

### Task-size check

Use roughly 600–1,200 words for a parent PLAN as a soft routing target; excess prompts a review of duplication, independent concerns, and current versus historical content.

Use 500–1,000 words as a soft target for an active task, excluding necessary protocol examples. These are starting limits, not measured optimums; a complete smaller brief is sufficient. Above the target, remove duplicated requirements and historical material, then reference canonical source contracts. If independently verifiable implementation concerns remain, split them into focused tasks.

Above roughly 1,500 words, perform a scope review before the Plan gate or the next implementation step. Record a short conclusion in Current status and remaining work: reduced size, proposed implementation split, or why one coherent outcome needs the remaining detail. A split revises the task map and requires Map approval; coherent complexity may justify exceeding the target. Size targets trigger scope review; they must never justify dropping requirements or hiding necessary detail in another mandatory document. Run the preservation check below through every reduction.

## Acceptance and evidence

Every plan delivers demonstrable behavior. Define acceptance with inputs, actions, and observable results, including relevant error and recovery paths. Internal changes need a runnable scenario or behavioral tests that prove their effect; compilation alone is insufficient.

Task validation proves its boundary: HTTP behavior for backend work, UI behavior against controlled API responses for frontend work, and the owned assembly boundary for integration work. Assign the plan's assembled-behavior validation and cross-task checks to an explicit task; its Result gate reviews that evidence.

Agree test seams at the Plan gate. During implementation use TDD: one behavior, a failing test, then the minimum implementation to pass it; a bug starts with a regression test. Use exact project commands and explain expected results. Inspect repository scripts instead of caching unrelated toolchain instructions.

Give validation procedures stable IDs or named anchors. Retain their exact commands, repository-relative working directories, required setup, and expected results in Implementation steps after completion, or in a directly referenced canonical validation record. When compacting completed edit steps, update evidence pointers to the retained procedures. Each retained result must resolve directly to the procedure used to obtain it.

Record the latest relevant validation against each acceptance ID: procedure reference, observed result, date, and tested commit or description of the uncommitted working tree. For incremental checks on unchanged behavior, retain the evidence still applicable to the current result. Mark invalidated evidence and the required rerun as remaining work; earlier success never proves revised behavior by itself. Keep short output or link durable evidence instead of pasting full logs.

Result acceptance, rather than finishing implementation or passing tests, completes the task. The plan is complete when every task result is accepted and no planned work remains. Preserve shipped acceptance IDs and evidence references even when implementation instructions are retired.

## Current instructions and history

Active artifacts describe current approved work. Keep agreed behavior and constraints in the PLAN or canonical agreements referenced there. Keep implementation decisions at the narrowest consuming scope with stable IDs or named anchors; dependent tasks link to them. Retain unresolved questions, unfinished obligations, and decisions still governing future work as active, even when the current task does not load them.

An old decision leaves default execution context only after its approved replacement is explicit. Retain the earlier decision and rationale in a directly linked history record, marked `Superseded`, with its replacement pointer, reason for change, approval record, and affected task contracts and acceptance evidence. A single archive file may hold named records; load only the relevant record when needed to understand a governing decision or investigate a problem. Git history preserves ordinary edits, but is not the canonical home for agreed decisions. Superseded verification rounds and completed review follow-ups may share that history record; preserve shipped evidence references and mark which evidence remains applicable.

Before compacting a legacy task, reconcile approved changes, unresolved review work, and evidence applicability. For a Session changed from PostgreSQL to Redis, the active contract retains expiry, rotation, failure behavior, and accepted re-login after data loss. It links directly to the superseded PostgreSQL decision, change rationale, approval, affected task contracts, and evidence. A dependent Project ownership task retrieves the current Session contract; earlier rationale is directly retrievable when needed.

An accepted result produces a short parent handoff containing contracts and outcomes later work needs, with canonical paths or symbols and evidence pointers. Recommend a fresh conversation for the next task; file isolation cannot remove previous work already loaded into a conversation. Keep general retrospectives outside execution context unless a lesson still constrains work; consequential decisions always retain identifiable records.

### Preservation check

Before compaction, inventory every agreed item in the affected artifacts, including future-work agreements. After restructuring, verify that:

- Every requirement, constraint, contract, acceptance condition, and consequential decision still has one identifiable canonical location; its meaning is preserved.
- Every moved item has a direct reference that resolves to the file and ID or anchor. The current task includes or references every governing agreement without requiring a history scan.
- Every superseded decision has an explicit approved replacement and a linked record retaining rationale, approval, and affected contracts and evidence.
- The task map and dependent tasks point to current contracts. Inspect sibling contract pointers only under the contract-change exception; use the parent map to audit coverage.
- All unresolved questions, unfinished obligations, future constraints, acceptance IDs, and shipped evidence references remain accounted for; mark invalidated evidence and required reruns explicitly.
- Every retained validation result resolves to its reproducible procedure as defined in Acceptance and evidence, including after completed edit steps are removed.

Record a short check result with any gaps in the artifact's current status or audit section. Compaction is complete only when every item is accounted for and references resolve. Gaps stay active until reconciled; document editing never substitutes for semantic approval.

## Resume state

Near the top of the PLAN record `Current task` (or approved concurrent set), `State`, and `Remaining`. Record each mapped task's explicit state as well as its checkbox. The task repeats its identity and state as a synchronized view, with granular remaining work in its final section. Update both at every phase transition and before handing off. Checkboxes track accepted completion; the explicit state selects the next action.

| State | Next action |
| --- | --- |
| `awaiting-map-review` | Wait for task-map approval. |
| `ready-to-detail` | Detail the named task when authorized to continue. |
| `detailing` | Finish its execution brief and scope check. |
| `awaiting-plan-review` | Wait for this task's plan approval. |
| `implementing` | Continue approved implementation and validation. |
| `awaiting-result-review` | Wait for acceptance or requested revision. |
| `reopened` | Address recorded review work; material design changes return to the Plan gate. |
| `accepted` | Task boundary accepted; publish its handoff and select remaining work. |
| `complete` | No task work remains; all results are accepted. |

Record approval scope and any follow-up conditions compactly in current status so resume does not reconstruct them from chat. Follow the flow's transitions; `complete` requires every task result accepted, no planned work remaining, and `Current task: none`.

## Formatting

Use plain Markdown with one blank line after headings. When presenting a whole plan in chat, use one `md` fence and indented examples inside it; files omit that envelope. Use the skeleton's sections, omit optional sections without useful content, and add no placeholder prose. Checklists track progress in the PLAN and remaining work in the task. Tables are useful for coverage or state mappings when clearer than prose.

All paths in planning artifacts, including commands, working directories, examples, logs, and evidence, are relative to the repository root. Treat artifacts as public: include no secrets. Use the current Git username where an author is needed.
