---
name: to-spec
description: "Create a spec from the current conversation. Do not interview the user. Also update existing specs with new context."
---

# To-Spec

## Overview

This skill takes the current conversation context and codebase understanding and produces a spec. Do NOT interview the user; just synthesize what you already know.

For updates, read the existing spec and new context.

Preserve all explicit user requirements, decisions, terminology, constraints, code-style instructions, and boundaries. Do not replace them with preferred alternatives.

## The Gated Workflow

The human must review the created or updated spec before it can be finalized.

Never write implementation code. This skill only creates or updates specs.

## Workflow

### 1. Shared understanding

Surface assumptions before drafting the spec.

Don't silently fill in ambiguous requirements. The spec's entire purpose is to surface misunderstandings before code gets written — assumptions are the most dangerous form of misunderstanding.

Record unresolved items as Open Questions.

Only include assumptions that materially affect the spec.

Use this format:

```text
ASSUMPTIONS I'M MAKING:
1. This is a web application (not native mobile)
2. Authentication uses session-based cookies (not JWT)
3. The database is PostgreSQL (based on existing Prisma schema)
4. We're targeting modern browsers only (no IE11)

❗️Correct me now or I'll proceed with these.
```

Wait for the human to correct the assumptions or approve them.

### 2. Specify

Write a spec document using [template](./templates/SPEC.md).

Place it under `../../../docs/features` if no other destination is provided.

Update an existing spec in its current location.

**Guidelines:**

Do not duplicate repository-wide rules, conventions, or defaults that are already defined in `AGENTS.md` or other repository guidance.

Do not infer repository-wide rules into feature-specific spec sections.

Include them in the spec only when:

- the human explicitly discusses or changes them for this spec;
- the spec introduces an exception or additional constraint;
- they are necessary to understand a feature-specific decision.

Otherwise, omit them from the spec.

**After the spec is saved:**

- Summarize it and list any Open Questions.
- Ask the human to approve it or request changes.
- If changes are requested, update the same spec while preserving decisions the human did not change.
- Consider the spec final only after explicit human approval.
- Record explicit human approval and its scope in the spec.
- Changes to an approved spec remove its approval. Obtain new human approval.
- Do not change the spec to excuse code that fails an unchanged requirement.
