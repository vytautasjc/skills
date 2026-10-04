# Effort Specifications

This reference gives rules for the permanent `SPEC.md` for one staged effort. To create, revise, review, or keep an effort SPEC, read this file. During execution, load only the current task's assigned entries and all references necessary to understand them. One entry has no dependency on the full SPEC or its history.

Use [`ROADMAPS.md`](ROADMAPS.md) for delivery coordination. Use `plan-tasks` and its `PLANS.md` reference for implementation planning as work becomes current.

## What a SPEC is

The SPEC is the permanent source of truth for the full agreed outcome. It keeps accepted behavior and product decisions from discovery. Delivery assignments and implementation details have separate documents. Create one SPEC with the ROADMAP during initial decomposition. Keep it for the life of the effort.

A full SPEC gives an agent without conversation history enough context to understand each stage's assigned outcome. It has no dependency on a transcript, chat, scratch document, or sibling stage tree.

Keep these items in the SPEC:

- Overall outcome and scope.
- Domain language.
- Requirements and contracts.
- Invariants.
- Acceptance scenarios.
- Open product questions.

Keep stage assignments in the ROADMAP. Keep task decomposition, file edits, commands, and implementation detail in PLANs and tasks.

Use [PLANS.md](../../plan-tasks/references/PLANS.md#current-context-and-ownership) for general context ownership, decision history, and preservation. This reference adds staged ownership, ID traceability, and semantic amendment rules.

## Canonical ownership

Keep each meaning in one canonical place:

- `SPEC.md`: full agreed behavior, constraints, contracts, invariants, acceptance, domain meaning, and open product questions across all stages.
- `ROADMAP.md`: stage boundaries, order, dependencies, production release prerequisites, SPEC-ID coverage, status, delivery decisions and terms, and delivered outcomes needed later.
- Stage PLANs and tasks: implementation decisions, terms, and mappings with [PLANS.md ownership](../../plan-tasks/references/PLANS.md#current-context-and-ownership).

Move delivery knowledge needed across stages to the ROADMAP. Make proposed changes to agreed meaning through the Spec amendment gate.

References can include the same stable IDs. Keep definitions and reasons in one canonical location. When a delivery stage changes, update references. Keep the item's definition at its existing location.

Keep effort-specific domain definitions in the SPEC after scaffolding. Refer directly to them from feature `CONTEXT.md` files. For existing repository-wide terms, refer to their canonical glossary.

## Stable IDs and traceability

Use IDs that remain stable when delivery plans change:

- `R001`, `R002`, …: necessary behavior or constraints.
- `C001`, `C002`, …: externally related interfaces, data, protocols, compatibility, or recovery contracts.
- `I001`, `I002`, …: invariants that must remain true.
- `A001`, `A002`, …: acceptance scenarios or validation rules.
- `Q001`, `Q002`, …: open product questions.

Each normative ID (`R`, `C`, or `I`) must have coverage through one or more `A` IDs. In each acceptance entry, cite each normative ID that it covers. If direct behavioral observation is impossible, identify the specified inspection, analysis, or test evidence that proves the obligation.

Keep IDs stable for clearer wording with the same meaning. After approval, use a new ID for changed meaning. Identify the earlier entry as `Retired`. Add a reference to its replacement, if one exists. Keep identifiers unique permanently.

For the earlier meaning and decision record, follow [Current instructions and history](../../plan-tasks/references/PLANS.md#current-instructions-and-history). Default SPEC context can keep only the retired ID, replacement, and history reference. A requirement can then move between stages with the same identity. Evidence from delivered stages keeps its original meaning.

Give normative, acceptance, and applicable open-question IDs to stages in the ROADMAP. Give stage normative and acceptance coverage to tasks in the PLAN. Give shared constraints to each applicable task. In task results, write evidence against acceptance IDs.

For acceptance scenarios across stages:

- Give the same acceptance ID in each contributing stage's `Coverage`.
- Identify each stage's observable portion.
- Identify one final acceptance owner.
- Give those portions to tasks.
- Demonstrate each contributing stage's assigned portion.
- Have the final owner demonstrate the full scenario against the assembled result.

Keep the full scenario definition in the SPEC. Use coverage entries to identify boundaries.

For stage decomposition and acceptance, load full stage coverage. For task planning and execution, load task coverage, referenced contracts and invariants, and necessary glossary entries. Keep the full traceability map when retrieval is limited to a task.

Use references through each necessary level. Include shared contracts, applicable invariants, necessary domain terms, acceptance portions, and important decisions. Identify the full applicable set in each task. A stage-wide list alone is insufficient.

Give open-question IDs to each stage their answers can affect. Get answers before the earliest affected Map gate. Repeated IDs along this sequence are references to one definition.

Keep an open-question ID stable after resolution. Identify its entry as `Resolved`. Write the answer and normative or acceptance IDs that it added or clarified. Keep the original question. Pass the resolution through the Spec amendment gate before affected planning or implementation continues. A product answer changes or completes the agreed outcome.

## Completeness bar

Before the Roadmap/Spec gate, compare each discovery source with the SPEC and ROADMAP. Make sure all these conditions hold:

- Each accepted behavior and product decision has one permanent, canonical location.
- Each applicable success path, error path, edge case, failure mode, and security or privacy constraint has coverage.
- Each applicable compatibility or migration concern, operational expectation, and recovery behavior has coverage.
- Each normative ID has acceptance evidence coverage.
- Each delivery dependency appears in the ROADMAP through references to SPEC definitions.
- Each open question states its resolution condition and latest safe gate.
- Each open-question ID appears in each stage that its answer can affect. Its latest safe gate is at or before the earliest affected stage's Map gate.
- A future planner has no dependency on a transcript, conversation memory, or sibling-stage file.

## Concision bar

Write each accepted meaning only in its canonical ID entry. Use accurate terms and observable conditions. Keep examples and reasons only when they explain necessary meaning. Omit empty optional sections and implementation commentary.

Use one sentence or short list item when sufficient. Add detail for domain complexity, unclear meaning, risk, edge cases, or contracts. Keep each accepted behavior, constraint, invariant, acceptance case, and the context necessary to understand it.

## Lifecycle

The initial Roadmap/Spec gate approves the agreement and its first delivery map. After that gate, select the applicable change procedure:

- **Delivery change:** reassign unchanged SPEC IDs among stages that have not started. Use a Stage gate during milestone review. If the change cannot safely wait, use a Roadmap amendment gate. Update the ROADMAP. Write the reason in its Decision Log.
- **Semantic change:** change agreed behavior, constraints, contracts, invariants, or acceptance. This includes resolution of an open product question. Retire and add normative or acceptance IDs as necessary. Keep a resolved question with its existing ID. Add a SPEC Revision Log entry. Update affected ROADMAP coverage. Stop at the Spec amendment gate before more planning or implementation.

Keep delivered stage coverage and evidence fixed. For later semantic changes, add new IDs for future delivery. Keep what the delivered stage proved. Clearer wording with the same meaning can keep its ID. Show the clarification and reason in the Revision Log.

## History and preservation

Before you make documents shorter, use [Current instructions and history](../../plan-tasks/references/PLANS.md#current-instructions-and-history). Complete its [Preservation check](../../plan-tasks/references/PLANS.md#preservation-check) across affected documents.

Also make sure these conditions hold:

- Each retired SPEC ID keeps its replacement reference, if one exists.
- Delivered coverage remains fixed.
- Semantic changes have passed the Spec amendment gate.

Keep short SPEC change records in the Revision Log. Identify each record by stable ID or named anchor. Follow PLANS.md Current instructions and history to reference earlier definitions in Git. Write the preservation-check result in the Revision Log. Write ROADMAP checks in Audit References. Write PLAN and task checks in their status or audit sections.

## Formatting

Use short paragraphs or lists, whichever is clearer. Put one blank line after each heading. Use correct list syntax. Write each path relative to the repository root. Give a definition for each domain term at first use.

Treat the file as public. Keep secrets out of it. Omit unnecessary optional sections and placeholder prose. Keep all content necessary to meet the completeness bar. For a standalone SPEC file, omit outer code fences.

## Template

    # <Effort name> Specification

    Roadmap: <repository-relative ROADMAP path>
    Method: <repository-relative SPECS.md path, only if stored in the repository>

    ## Purpose / Big Picture

    Write what becomes possible and how to identify it.
    Use one sentence when sufficient.
    Keep delivery and implementation in their own documents.

    ## Ubiquitous Language

    Give a definition for each domain term necessary to understand the specification.
    Keep implementation terms in the applicable PLAN, task, or code context document.

    ## Scope

    ### Included

    Write the behaviors, users, data, and operating conditions that the effort covers.

    ### Excluded

    Write nearby behavior deliberately deferred or rejected.

    ## Requirements

    Write each accepted behavior and constraint.
    Include reasons when they prevent a future change in interpretation.

    - R001: …
      Rationale: …

    ## Contracts

    Write externally related interfaces, data or protocol rules, compatibility boundaries, and failure or recovery guarantees.

    - C001: …

    ## Invariants

    Write conditions that implementation must keep across all applicable states and transitions.

    - I001: …

    ## Acceptance Scenarios

    Give observable scenarios or accurate validation rules that together prove each normative ID.
    Include applicable errors and edge cases.

    - A001 (covers R001, C001, I001): Given …, when …, then …

    ## Open Questions

    Include only open product questions.
    Write why each question is open.
    Write its resolution condition and latest safe gate.
    Keep implementation choices without effects on the agreed outcome in the future PLAN.

    - Q001 [Open]: …
      Why unresolved: …
      Resolution condition: …
      Latest safe gate: …

    After resolution, keep the entry as Q001 [Resolved].
    Add the answer and normative or acceptance IDs that it added or clarified.

    ## Revision Log

    Index each clarification or semantic amendment after approval by stable revision ID or named anchor.
    For replaced records, follow PLANS.md Current instructions and history.
    When you make documents shorter, write preservation-check results.

    - REV001: …
      Affected IDs: …
      Rationale: …
      Approval gate: Roadmap/Spec | Spec amendment
      Approval record: <decision reference and date, pending until approval>
      Affected contracts/evidence: <direct references and applicability>
      History: <full commit hash, repository-relative file path, and ID or anchor for replaced records>
      Date/Author: (2026-06-20 14:00Z) / <git username>
