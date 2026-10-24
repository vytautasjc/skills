---
name: write-tests
description: "Write and change tests with TDD, arrange-act-assert, real collaborators, branch coverage, and mutation testing. Use when you add or change tests, or add or change behavior of production code, in any language. Do not use for refactors, renames, formatting, or dependency updates that do not change behavior."
---

# Write Tests

Write tests that prove behavior. Use TDD. Use real collaborators where possible. Cover each branch. Prove the tests with mutation testing.

## Scope

- Apply these rules when you add or change tests, or add or change behavior of production code.
- Apply the test rules only to tests that you add or change. Do not change other tests unless the user asks.
- Do not add a tool or a dependency without approval from the user. This rule includes test, coverage, and mutation tools.

## Rule precedence

1. If a rule conflicts with a rule in [Security](#security), the Security rule wins.
2. User instructions win over all other rules.
3. Follow the repository for the test framework, file locations, test naming style, and grouping style. These repository conventions win over this skill and the language references.
4. For all other rules, follow this skill and the language reference. If they conflict, the language reference wins.

## Language references

Read only the reference file for the language of the tests that you write. Do not read other reference files. If you write tests in more than one language, read one reference file for each language.

- JavaScript and TypeScript: [javascript.md](./references/javascript.md)
- Java: [java.md](./references/java.md)
- Kotlin: [kotlin.md](./references/kotlin.md)
- Python: [python.md](./references/python.md)
- Go: [go.md](./references/go.md)
- C#: [csharp.md](./references/csharp.md)
- Rust: [rust.md](./references/rust.md)
- Ruby: [ruby.md](./references/ruby.md)

For a language with no reference file, use the grouping mechanism of the language:

- Use one root group for each file. Name the root group after the unit under test.
- Use nested groups for each method, function, or scenario.

## Workflow

1. Run all test suites that the repository defines. Record the failures as the baseline. If a suite cannot run because of missing infrastructure, record the suite as skipped.
2. Do the [TDD cycle](#tdd-cycle) for each behavior.
3. Do the [branch coverage](#branch-coverage) check.
4. Do [mutation testing](#mutation-testing).
5. Do the [completion](#completion) steps.

If a change adds or changes no behavior, do only these steps:

- Refactor or rename: steps 1, 3, and 5. Write tests for uncovered branches with [Tests for existing code](#tests-for-existing-code).
- Dependency update: steps 1 and 5.

## TDD cycle

1. Write one failing test for one behavior.
2. Run the test. Make sure that it fails for the expected reason. A compile error or a setup error is not the expected reason.
3. Write the minimum production code that makes the test pass.
4. Refactor the code that you wrote or changed in this task. Keep all tests green.
5. Write the next test. Do not write all tests first.

During the cycle, run only the tests for the unit under test and the test files that you changed.

### Bug fixes

1. Write a test that reproduces the bug.
2. Run the test. Make sure that it fails before the fix.
3. Fix the bug.
4. Run the test. Make sure that it passes after the fix.

For a bug that end users can see, also write a failing e2e test first. If the repository has no e2e suite, do not write the e2e test. Report the missing e2e test in the [completion](#completion) steps.

### Tests for existing code

A test for existing code that works cannot fail first. Do these steps to prove each test:

1. Write the test and make sure that it passes.
2. Break the production code on purpose.
3. Make sure that the test fails.
4. Restore the production code.
5. Run the tests for the unit. Make sure that all tests pass.

## Test levels

| Level | Use for | Allowed |
| --- | --- | --- |
| Unit (default) | All logic, and adapters that do not touch a unit boundary | The options in the order of [Test doubles](#test-doubles) |
| Integration | Adapters that touch a unit boundary, e.g. an HTTP controller on a real HTTP server, a repository on a real database, or an HTTP client on a local server | Real file system, network, and database |
| E2E | Bug fixes that end users can see, and flows that the user asks for, through the public interface (HTTP, CLI, UI) | The real system. No test doubles, except for third-party services. |

Do not write e2e tests for other behavior. Use unit and integration tests.

### Unit tests

Write unit tests as small integration tests of a module, component, or package. Inject real instances of collaborators.

Unit tests never touch these unit boundaries:

- file system
- network
- database
- real clock
- randomness
- child processes
- environment variables

Use a fake for these boundaries. If a fake is not practical, use a mock. In-memory substitutes are fakes, e.g. `memfs` or `jimfs`. For environment variables, follow [Environment variables](#environment-variables).

### Environment variables

- No test sets or changes environment variables.
- Unit tests do not read environment variables.
- Integration and e2e tests can read environment variables.
- Production code receives its configuration as a value, e.g. a config object or a constructor parameter. Unit tests pass the configuration values directly.
- Only the entry point reads environment variables, e.g. `main`, the composition root, or the framework config loader. The entry point passes the values as configuration.
- Only integration or e2e tests cover the entry point.
- If a function or method that you change reads environment variables directly, change that function or method to receive its configuration as a value. Move the read to the entry point.

### Test doubles

Use the first option that works:

1. Real instance.
2. Fake: a simple working in-memory implementation, e.g. `InMemoryUserRepository`. The test asserts on the state of the fake, e.g. `fakeMailer.sent`.
3. Stub: returns fixed values. The test does not verify calls on a stub.
4. Mock: records calls. The test verifies the calls. Use a mock only at a unit boundary, and only when a fake is not practical, e.g. for a large third-party SDK.

### E2E tests

- Do not use test doubles.
- The only exception is a third-party service that you do not control. Use its sandbox. If it has no sandbox, use a local fake server.

## Test structure

- Use arrange-act-assert. Put one blank line between the sections. Do not add section comments.
- If the framework puts the Act inside the assertion, e.g. `expect(() => f()).toThrow()`, write Act and Assert as one section.
- If a test has no Arrange, omit the Arrange section.
- Use one Act and one behavior in each test. A test can have more than one assertion if all assertions check that behavior.
- Name each test after its behavior, e.g. `returns 0 for an empty cart`. Do not use the `should` prefix.
- Do not use logic in tests, e.g. `if` or loops.
- Inline the values that the test is about. For complex values that are not related to the behavior, you can use a builder or a factory.
- Use specific matchers, e.g. `toEqual(...)`, not `toBeTruthy()`.
- Use parameterized tests only when all cases have the same Act and the same assertion shape. Give each case a descriptive name.

## Isolation and cleanup

Tests never leave a dirty test environment, e.g. databases, files, or queues.

- Put cleanup in hooks, e.g. `afterEach` or `afterAll`. Cleanup at the end of a test body does not run when the test fails.
- Give each test its own resources, e.g. a unique temp directory, a unique database schema, or a transaction rollback.
- Do not share mutable fixtures between tests.
- Create new fakes in each test, or reset the fakes in a setup hook.
- Make sure that tests pass in any order and in parallel.

## Security

- Do not use real secrets or real personal data in tests or fixtures.
- Never weaken or remove a security assertion to make a test pass.

### API tests

Apply these rules to all tests that send HTTP requests to an endpoint of the system under test, at all test levels.

- Assert the full response body, not a part of it. Unexpected fields must fail the test.
- For dynamic values, e.g. IDs or timestamps, use type or format matchers in place of the value. Keep the exact set of fields.
- Assert the response headers that the API sets, e.g. `Content-Type`, `Cache-Control`, and security headers.
- Make sure that responses do not leak sensitive data. Examples are passwords, password hashes, tokens, secrets, internal IDs, stack traces, and data of other end users.
- An internal ID is an ID that the API specification does not include and that no existing endpoint returns, e.g. a database row ID behind a public UUID.
- Make sure that error responses do not show internal details.
- Test access control for each new or changed endpoint:
  - If the endpoint requires authentication, send a request with no authentication.
  - If the endpoint gives access to resources of an end user, send a request for a resource of another end user.
- Assert the status code that the API specification sets for each case, e.g. 401, 403, or 404. An example of an API specification is an OpenAPI file.
- If the repository has no API specification, use the status code that the existing endpoints use for the same case.
- If you cannot find the status code, ask the user.

## Branch coverage

Do the branch coverage check one time, after the TDD cycles for all behaviors are complete. Cover each branch in the production code that you add or change.

A branch is one outcome of a decision:

- the true outcome and the false outcome of an `if`, ternary, or loop condition
- each `case` and the default of a switch or match
- each early return
- each `catch` block or error path

Each operand of `&&` or `||` is not a separate branch. If a coverage tool reports each operand as a branch, use the definition in this skill.

- If the repository has a coverage tool with branch coverage, run it on the changed code.
- If the repository has no coverage tool with branch coverage, write a manual branch list in the report. Name the test that covers each branch.
- Write a test for each branch that no test covers.
- If a branch cannot be reached, explain why in the report.

## Mutation testing

Do mutation testing one time, after the branch coverage check. Mutate the production code that you changed and that unit or integration tests cover. If you only add tests for existing code, mutate the units that the new tests target. Do not mutate code that only e2e tests cover. This code is the mutation scope.

- If the repository has a mutation tool, e.g. Stryker, PIT, or mutmut, run it on the mutation scope only.
- If the repository has no mutation tool, do manual mutations. Make one mutant for each condition, comparison, and return value in the mutation scope.
- Make a maximum of 20 manual mutants for each task. Start with the logic that is most likely to be wrong. Report the parts that you skipped.
- Restore the code after each mutation. Run the tests for the unit. Make sure that all tests pass.
- Kill each surviving mutant with a new test. If a mutant is equivalent, explain why.

## Completion

Do these steps one time, after mutation testing. Do not do them after each test.

1. Examine `git diff`. Make sure that it shows only the intended changes, and no mutation or break from a test proof.
2. Run all test suites that the repository defines. If a suite cannot run because of missing infrastructure, report the suite as skipped. Give the reason.
3. Compare the failures with the baseline. Fix each new failure that your change did not intend. If a test fails because of an intended behavior change, ask the user before you change the test.
4. Report the baseline failures. Do not fix them unless the user asks.
5. Report each e2e test that you did not write because the repository has no e2e suite.
6. Report the branch coverage result and each branch that cannot be reached.
7. Report the mutation results: mutants that you ran, killed, and survived. Give a reason for each surviving mutant.
8. If the repository has no coverage tool or no mutation tool, suggest a tool from the language reference. Do not install the tool.
