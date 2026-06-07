# `docs/security.md` instruction

## Purpose

Document project-specific security, authentication, authorization, tenancy, and sensitive-data rules.

This doc should capture security facts that an AI coding agent must not get wrong.

It is not a generic secure-coding checklist.

## Output file

```text
docs/security.md
```

## When to create or update

Create this file only when approved and security-sensitive behavior is present.

Recommend it when the repo has:

- authentication
- authorization
- roles or permissions
- multi-tenancy
- admin functionality
- public/private routes
- payments
- personal data
- audit logging
- security middleware
- API keys or external secret usage

## Sources to inspect

- auth middleware
- route guards
- permission checks
- role definitions
- tenancy logic
- API handlers
- config files
- security-related tests
- docs
- infrastructure secret references
- CI/CD secret names
- user-provided context

## Required content

Cover what can be verified:

1. Authentication mechanism.
2. Authorization model.
3. Roles and permissions.
4. Tenancy boundaries.
5. Public vs protected surfaces.
6. Sensitive data handling.
7. Secret management references, without values.
8. Audit logging, if present.
9. Security-sensitive gotchas for agents.

## Recommended structure

```markdown
# Security

## Summary

<Short security overview or `Not documented yet`.>

## Authentication

- <Mechanism/provider or Not documented yet>

## Authorization

- <Roles/permissions/model or Not documented yet>

## Tenancy

- <Tenant boundary or Not documented yet>

## Protected surfaces

- <Route/API/resource> — <protection mechanism if verified>

## Sensitive data

- <Data type> — <handling rule if verified>

## Secrets

- Secrets are referenced by name only.
- `<NAME>` — <purpose if visible>

## Audit logging

- <Behavior or Not documented yet>

## Agent cautions

- <Specific project constraint an agent must preserve>
```

## What to avoid

Do not include:

- generic security advice
- secret values
- private keys
- tokens
- passwords
- invented roles
- invented permission behavior
- detailed exploit information
- broad policy claims not represented in the repo

## Accuracy rules

- Do not claim RBAC exists unless roles or permissions are visible.
- Do not claim multi-tenancy exists unless tenant boundaries are visible.
- Do not claim a route is protected unless guards/middleware/config confirm it.
- Do not claim audit logging exists unless code or docs show it.
- If security behavior is unclear, mark it as `Not documented yet`.

## Self-check

Before finishing, confirm:

- No secrets are exposed.
- Auth and permission claims are verified.
- Tenant boundaries are not guessed.
- Security cautions are project-specific.
