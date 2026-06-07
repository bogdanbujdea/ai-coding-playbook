# `docs/testing.md` instruction

## Purpose

Document the project's actual test tools and commands.

This doc should stay short. It is not a generic testing philosophy document.

## Output file

```text
docs/testing.md
```

## When to create or update

Create this file only when approved and when tests or test tooling are detected.

Do not create this file for projects with no tests unless the user explicitly asks.

## Sources to inspect

- test files
- test project files
- package manifests
- test config files
- CI/CD pipeline jobs
- `README.md`
- existing docs
- build scripts
- Makefile or task runner files

## Required content

Cover:

1. Test frameworks and assertion libraries.
2. Test project or test file locations, only if obvious and useful.
3. Commands to run tests.
4. Commands for specific test categories, if present.
5. Required local services for integration/e2e tests.
6. CI/CD test behavior, briefly.

## Recommended structure

```markdown
# Testing

## Tools

- <Framework> — <purpose>
- <Assertion library> — <purpose>

## Run tests

```bash
<command>
```

## Test categories

- Unit tests: `<command or Not documented yet>`
- Integration tests: `<command or Not documented yet>`
- End-to-end tests: `<command or Not documented yet>`

## Local requirements

- <Service or dependency required for tests>

## CI/CD

- Tests run in `<pipeline/job>` if verified.
```

## What to avoid

Do not include:

- generic testing advice
- “write meaningful tests”
- “use best practices”
- mocking philosophy unless project-specific and verified
- lengthy test naming conventions
- invented test categories
- unverified commands

## Accuracy rules

- Do not say tests exist unless test files, test projects, or test commands exist.
- Do not say a framework is used unless dependencies or config confirm it.
- Do not say integration tests need a service unless config or docs confirm it.
- Keep this doc short.

## Self-check

Before finishing, confirm:

- The doc names only detected test tools.
- Commands are verified.
- It does not contain generic testing rules.
- It links to CI/CD only if relevant and existing.
