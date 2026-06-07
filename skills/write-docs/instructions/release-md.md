# `docs/release.md` instruction

## Purpose

Document how changes are released to users.

This doc should explain the actual release and rollback process when it is visible or provided by the user.

## Output file

```text
docs/release.md
```

## When to create or update

Create this file only when approved and when release behavior is non-trivial or visible.

Recommend it when the repo has:

- deployment pipelines
- version tags
- release branches
- changelog tooling
- manual approval steps
- package publishing
- production migration concerns
- feature flags
- rollback instructions

## Sources to inspect

- CI/CD deployment workflows
- release scripts
- package publishing config
- changelog files
- versioning config
- deployment docs
- infrastructure docs
- existing release notes
- user-provided context

## Required content

Cover what can be verified:

1. Release trigger.
2. Release environments.
3. Versioning or tagging.
4. Deployment process.
5. Manual approval or gate steps.
6. Rollback process, if known.
7. Database or infrastructure migration cautions, if known.
8. Relationship to CI/CD.

## Recommended structure

```markdown
# Release process

## Summary

<How changes reach users, or `Not documented yet`.>

## Release trigger

- <branch/tag/manual action/package publish trigger>

## Environments

- <Environment> — <release behavior>

## Steps

1. <Verified step>
2. <Verified step>

## Versioning

- <Versioning/tagging approach or Not documented yet>

## Rollback

- <Rollback process or Not documented yet>

## Migration cautions

- <Caution or Not documented yet>

## Related docs

- CI/CD: `ci-cd.md`
- Infrastructure: `infrastructure.md`
```

## What to avoid

Do not include:

- generic release advice
- invented rollback steps
- invented versioning policy
- deployment details already covered in CI/CD
- infrastructure inventory
- secret values

## Accuracy rules

- Do not infer release process from CI existence alone.
- Do not claim automatic production deployment unless verified.
- Do not claim rollback exists unless scripts/docs/pipelines describe it.
- If no release process is visible, say `Not documented yet`.

## Self-check

Before finishing, confirm:

- Release triggers are evidence-backed.
- Rollback is marked unknown if not verified.
- The doc does not duplicate `docs/ci-cd.md`.
- Links resolve.
