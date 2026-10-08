# Task [Number]: [Observable outcome]

Size: [XS | S | M | L]
Depends on: [Task links, or None]
Source: [Relevant spec section; omit for conversation input.]

## Description

[One or two sentences about the task outcome and purpose.]

## Requirements

- [Required behavior or constraint.]

## Design

[Concrete task contract. Refer to plan decisions by ADRn. Omit when no design trigger applies.]

```[language]
// path/to/file
export function name(input: Type): Result; // throws NameError | returns Result<T, NameError>
```

### Required implementation (optional)

[Only when mandated. Reference ADRn for rationale.]

## References and Patterns

- Follow: path/to/file — [what to mirror, e.g. error handling, test structure]
- [Optional file path relevant to the task. Omit this section when no useful paths are known.]

## Acceptance Criteria

- [ ] [Observable result.]
- [ ] [Input or action] → [Exact expected result]
- [ ] [Required failure behavior, when applicable.]

## Verification

- [Check or procedure] → [Expected result]

## Result and Review

[Append each review attempt. Omit until implementation starts.]

- Changes: [Implemented behavior and changed files]
- Design: [Matches sketches, or approved contract changes]
- Verification: [Actual check results and any missing checks or existing failures]
- Human review: [Feedback and explicit acceptance of the checked result]
- Remaining work: [Corrections, amendments, or None]
