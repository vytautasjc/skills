# Plan Tasks

An execution plan divides one responsibility from start to end into tasks with clear implementation boundaries. The parent PLAN, current task brief, and repository references must support continuation without conversation history. Refer to source paths, tests, and canonical contracts.

## How to use this file

To create, revise, validate, execute, or continue a plan, read this reference. Use the [plan-tasks flow](../SKILL.md#flow) for task sequence and approval gates. Load `PLAN-SKELETON.md` only to write or restructure the parent PLAN. Load `TASK-SKELETON.md` only to write or restructure a task brief.

Examine the source necessary for the current phase. Keep future tasks as map entries until their turn.

## Current context and ownership

A **canonical location** is the single source of truth for an agreement.

Give each agreed requirement, constraint, contract, acceptance condition, and important decision one permanent, identifiable canonical location. The current task includes or directly references each applicable agreement. A shorter document can change presentation and retrieval. It must keep agreed meaning unchanged.

- **PLAN:** keep the outcome, ordered task map, acceptance coverage, shared implementation contracts, current decisions, and accepted handoffs for future work. Keep local detail in the task or canonical repository references.
- **Task:** keep its outcome, scope, write-path ownership, local contracts, implementation steps, validation, and remaining work. Load only the PLAN, current task, and necessary repository references.
- **Shared knowledge:** keep information necessary for other tasks in the parent or a canonical repository reference. Add that reference to the parent. Leave a one-line reference at the original location. Keep each meaning in one canonical place.

Open sibling task files only to investigate a changed or failing **contract**. A contract is a promised interface, type, or outcome that is necessary for a different task. A plan revision, new requirement, scope change, or failed outcome can cause this exception. For other effects across tasks, use current contracts and accepted handoffs in the PLAN or its linked references.

Define each unfamiliar term at its canonical scope, or link its glossary entry. Use repository-relative file paths. Identify functions and modules accurately. Show connections only when they help implementation. Keep necessary knowledge in the current repository and explicit references. Keep conversations and sibling task reasons outside execution dependencies.

## Task map

Map all tasks before you detail a task. Give each entry an observable outcome, scope boundary, dependencies, applicable agreements, and acceptance IDs. Write stable PLAN acceptance IDs, such as `A001`. Give shared constraints to each applicable task.

Before the Map gate, write shared contracts only when they affect decomposition. Keep all agreed future outcomes, boundaries, dependencies, acceptance references, and constraints in the PLAN, task map, or canonical references. Prepare future implementation detail when its turn starts.

## Decomposition

A **task** has one implementation responsibility with a clear boundary. It owns a specified implementation area and focused validation. A task can cover only part of the full user journey.

Before task map approval:

- Divide backend and frontend implementation into separate tasks.
- Separate implementation concerns that you can validate independently. Use this rule in backend work where applicable.
- Write necessary shared contracts before dependent implementation starts. Map who establishes them and when they get approval.
- Give one owner to each shared file and integration change.
- Create shared-contract and integration tasks only when actual work is necessary. Identify their acceptance responsibilities.
- Examine large documents for repeated content or scope that makes more tasks necessary.

Let a narrow exception apply only when separation causes an invalid intermediate state. Write the reason and affected boundary. A shared feature, domain, application, or deadline does not justify the exception. The user can accept backend HTTP behavior before the frontend exists. The user can accept frontend behavior against controlled API responses.

For example, Google authentication can have these tasks:

- Shared authentication contracts, if actual work is necessary.
- Backend authentication and Sessions.
- Frontend sign-in, Session state, and logout.
- Integration, if actual work is necessary.

Use the independent-concern rule in each example area. Select the task count from the work.

For a prototype task, write the unknown, executable experiment, and adoption criteria. For migration tasks, write validation of paths that coexist and conditions for safe retirement.

## Parallel execution

Run tasks concurrently only when all three conditions hold:

- Their write paths are separate.
- Their necessary contracts have approval.
- Neither task depends on the other's unfinished implementation.

Give each agent only its task, applicable agreements, necessary contracts, and related source context. Detail the small concurrent set before execution. Get approval for that set. Keep other tasks as map entries.

In the PLAN, write the set, each task's state, and the single owner of shared files and integration. Use sequential work if you cannot separate write ownership. Get explicit authorization before you give work to subagents. Concurrent-set approval does not authorize delegation.

## Compact execution briefs

Use these six sections:

1. Outcome and scope.
2. Owned paths and implementation area.
3. Required contracts and dependencies.
4. Implementation steps.
5. Acceptance and validation.
6. Current status and remaining work.

Write exclusions when necessary to control scope. Include reasons only when they change implementation or prevent a possible mistake. Keep local decisions and findings with the affected contract or step.

Put setup, generation, and migration commands with their steps. Use [Acceptance and evidence](#acceptance-and-evidence) for validation procedures. In Acceptance and validation, refer to those procedures. Write expected and observed results there. Keep commands at their canonical location.

Write each working directory relative to the repository root. Put recovery instructions with the step with risk. Where necessary, write safe retry, backup, or rollback procedures.

### Task-size check

Use approximately 600–1,200 words as a flexible target for a parent PLAN. Above that target, examine repeated content, independent concerns, and current versus historical content.

Use 500–1,000 words as a flexible target for an active task. Exclude necessary protocol examples from this count. These targets are starting points. They are not measured optimum sizes. A full shorter brief is sufficient.

Above the target, remove repeated requirements and historical material from active context. Then refer to canonical source contracts. Separate any remaining implementation concerns that you can validate independently.

Above approximately 1,500 words, examine scope before the Plan gate or next implementation step. Write a short conclusion in Current status and remaining work. Write the reduced size, proposed task split, or reason the remaining detail is necessary for one outcome. A task split changes the map and makes Map approval necessary. Necessary detail for one coherent outcome can justify a larger task.

Use size targets to trigger scope review. Keep all requirements and necessary detail available. A target does not justify a new mandatory document that hides necessary detail. Use the preservation check through each reduction.

## Acceptance and evidence

Each plan delivers behavior that you can demonstrate. Write acceptance through inputs, actions, and observable results. Include applicable error and recovery paths. For internal changes, provide an executable scenario or behavioral tests that prove their effect. Compilation alone is insufficient.

Validate each task's boundary:

- Backend: HTTP behavior.
- Frontend: UI behavior against controlled API responses.
- Integration: the assembly boundary owned by the task.

Give assembled plan behavior and checks across tasks to an explicit task. Examine that evidence at its Result gate.

Agree test seams at the Plan gate. During implementation, use TDD for one behavior at a time. First, write a failing test. Then write the minimum implementation that makes it pass. For a bug, start with a regression test. Use full project commands. Explain expected results. Examine repository scripts for tool instructions.

Give validation procedures stable IDs or named anchors. After completion, keep their full commands, repository-relative working directories, necessary setup, and expected results. Keep them in Implementation steps or a directly referenced canonical validation record.

When you make completed edit steps shorter, update evidence references to the kept procedures. Give each kept result a direct reference to the procedure that produced it.

For each acceptance ID, write the latest applicable validation:

- Procedure reference.
- Observed result.
- Date.
- Tested commit or description of uncommitted changes.

For incremental checks on unchanged behavior, keep evidence that still applies to the current result. Identify invalid evidence. Write necessary reruns as remaining work. Earlier success alone does not prove revised behavior. Keep short output or link permanent evidence.

Complete a task only after result acceptance. Complete the plan only after acceptance of each task result and completion of all planned work. Keep delivered acceptance IDs and evidence references after you retire implementation instructions.

## Current instructions and history

Active documents describe current approved work. Keep agreed behavior and constraints in the PLAN or its canonical agreement references. Keep implementation decisions at the narrowest scope that uses them. Give those decisions stable IDs or named anchors. Add references to those decisions in dependent tasks.

Keep unresolved questions, unfinished obligations, and decisions that control future work active. This rule also applies when the current task does not load them.

Remove an old decision from default execution context only after its approved replacement is explicit. Keep the earlier decision and reason in a directly linked history record. Identify it as `Superseded`. Include its replacement reference, change reason, approval record, affected task contracts, and acceptance evidence.

One archive file can hold named records. Load only the necessary record to understand a current decision or investigate a problem. Git history keeps ordinary edits. Keep agreed decisions in identifiable, canonical records.

You can keep replaced verification rounds and completed review changes in the same history record. Keep delivered evidence references. Identify which evidence still applies.

Before you make an earlier task shorter, reconcile approved changes, open review work, and evidence applicability. For example, a Session can change from PostgreSQL to Redis. Its active contract keeps expiry, rotation, failure behavior, and accepted re-login after data loss. Refer directly to the replaced PostgreSQL decision, change reason, approval, affected task contracts, and evidence. A dependent Project ownership task reads the current Session contract. Keep earlier reasons directly available when needed.

For an accepted result, write a short parent handoff. Include contracts and outcomes necessary for future work, with canonical paths or symbols and evidence references. Recommend a new conversation for the next task. File isolation cannot remove work already loaded in a conversation.

Keep general retrospectives out of execution context unless a lesson still controls work. Keep identifiable records for important decisions.

### Preservation check

Before you make documents shorter, list each agreed item in the affected documents. Include agreements for future work. After restructuring, make sure all these conditions hold:

- Each requirement, constraint, contract, acceptance condition, and important decision has one identifiable, canonical location. Its meaning stays unchanged.
- Each moved item has a direct reference to its file and ID or anchor. The current task includes or references each applicable agreement. It has no dependency on a history search.
- Each replaced decision has an explicit approved replacement. Its linked history record keeps reasons, approval, affected contracts, and evidence.
- The task map and dependent tasks refer to current contracts. Examine sibling contract references only for the contract-change exception. Use the parent map to audit coverage.
- All open questions, unfinished obligations, future constraints, acceptance IDs, and delivered evidence references remain available. Explicitly identify invalid evidence and necessary reruns.
- Each kept validation result links to its reproducible procedure with Acceptance and evidence. This rule is applicable after removal of completed edit steps.

Write a short check result and all gaps in the document's current status or audit section. Complete the reduction only when each item remains available and each reference reaches its target. Keep gaps active until resolved. Get semantic approval for changes to meaning.

## Resume state

Near the PLAN top, write `Current task`, `State`, and `Remaining`. `Current task` can identify an approved concurrent set. Write each mapped task's state as well as its checkbox.

Write task identity and state in the task file again. Keep these fields the same as in the PLAN. Write detailed remaining work in the task's final section. Update the two documents at each phase change and before handoff.

Checkboxes show accepted completion. The explicit state selects the next action.

| State | Next action |
| --- | --- |
| `awaiting-map-review` | Wait for task map approval. |
| `ready-to-detail` | Detail the named task when the user authorizes continuation. |
| `detailing` | Complete the execution brief and scope check. |
| `awaiting-plan-review` | Wait for task plan approval. |
| `implementing` | Continue approved implementation and validation. |
| `awaiting-result-review` | Wait for acceptance or requested revision. |
| `reopened` | Complete recorded review work. For important design changes, go to the Plan gate again. |
| `accepted` | The task boundary has acceptance. Write its handoff. Select remaining work. |
| `complete` | All results have acceptance. No task work is unfinished. |

Write approval scope and follow-up conditions briefly in current status. Make continuation possible without chat history. Use the flow's state changes. For state `complete`, get acceptance of each task result. Complete all planned work. Set `Current task: none`.

## Formatting

Use [ste-writing-skill](../../ste-writing-skill/SKILL.md) for language guidance and the review before delivery.
Apply it to PLANs, task briefs, handoffs, history records, and supporting planning documents.

Use plain Markdown. Add one blank line after each heading. For a complete plan in chat, use one `md` code fence. Indent examples inside that fence. Do not use the outer fence in files.

Use the required skeleton sections. Omit optional sections that have no useful content. Replace placeholder text with actual content.

Use checklists for PLAN progress and remaining work. Use tables for coverage or state mappings when a table is clearer than prose.

Use repository-root-relative paths for commands, working directories, examples, logs, evidence, and other planning content.

Treat all documents as public. Do not include secrets. If an author is required, use the current Git username.
