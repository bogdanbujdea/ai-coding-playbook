# `docs/local-development.md` instruction

## Purpose

Document how to install, run, build, and validate the project locally.

This doc should help an AI coding agent or developer execute the project without guessing commands.

## Output file

```text
docs/local-development.md
```

## When to create or update

Create this file by default for project documentation tasks.

## Sources to inspect

- `README.md`
- package manifests
- workspace files
- build files
- scripts
- Docker files
- compose files
- `.env.example`
- development config files
- test config files
- existing docs
- Makefile or task runner files

## Required content

Cover:

1. Tech stack summary.
2. Prerequisites.
3. Install command.
4. Local run command.
5. Build command.
6. Test command or link to `docs/testing.md`, if tests exist.
7. Typecheck and lint commands, if available.
8. Required local services.
9. Required local environment variables, without secrets.
10. Common local setup notes, if verified.

## Recommended structure

```markdown
# Local development

## Tech stack

- Language/runtime:
- Frameworks:
- Package manager:
- Database:
- Local services:

## Prerequisites

- <Tool/version if verified>

## Install

```bash
<command>
```

## Run locally

```bash
<command>
```

## Build

```bash
<command>
```

## Validate changes

```bash
<test/typecheck/lint commands>
```

## Local services

- <Service> — <how it is started locally>

## Environment variables

Required local variables:

- `<NAME>` — <purpose, not value>

## Notes

- <Verified setup note>
```

## What to avoid

Do not include:

- production secrets
- real credentials
- unverified commands
- full CI/CD description
- deployment instructions
- generic setup advice
- long troubleshooting sections unless backed by existing docs or known errors

## Accuracy rules

- Commands must be verified from scripts, config, docs, or successful execution.
- Do not infer the package manager if lockfiles conflict; ask or mark unknown.
- If a command is missing, write `Not documented yet`.
- If tests are complex, keep local-development short and link to `docs/testing.md`.
- Do not duplicate infrastructure details beyond local services needed to run the project.

## Self-check

Before finishing, confirm:

- Install/run/build commands are correct or marked unknown.
- Required local services are listed.
- Env vars do not expose secrets.
- The doc does not duplicate CI/CD or production infrastructure.
