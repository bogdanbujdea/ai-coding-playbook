# `docs/infrastructure.md` instruction

## Purpose

Document where and how the project runs outside local development.

This doc should help an AI coding agent understand deployed environments, runtime services, hosting, and infrastructure dependencies without inventing them.

## Output file

```text
docs/infrastructure.md
```

## When to create or update

Create this file by default for project documentation tasks, but keep it short if infrastructure is not visible in the repo.

## Sources to inspect

- infrastructure-as-code files
- deployment manifests
- Docker files
- compose files
- Kubernetes manifests
- Terraform, Pulumi, Bicep, ARM, CloudFormation, CDK files
- hosting config files
- CI/CD deployment jobs
- environment-specific config
- `README.md`
- existing docs
- user-provided context

## Required content

Cover what can be verified:

1. Hosting platform or runtime environment.
2. Deployed services.
3. Environments, such as local, staging, production.
4. Databases, queues, storage, caches, and background workers.
5. External infrastructure services.
6. How infrastructure relates to CI/CD, if visible.
7. Unknown infrastructure facts that need human confirmation.

## Recommended structure

```markdown
# Infrastructure

## Summary

<Short overview of deployed runtime, or `Not documented yet`.>

## Environments

| Environment | Purpose | Notes |
| --- | --- | --- |
| Local | Development | <notes> |
| Staging | Not documented yet | |
| Production | Not documented yet | |

## Services

- <Service> — <purpose and environment if verified>

## Runtime dependencies

- <Database/cache/queue/storage> — <purpose>

## Hosting and deployment

- Hosting platform: <verified platform or Not documented yet>
- Deployment mechanism: <verified mechanism or Not documented yet>

## External services

- <Service> — <why the project uses it>

## Open questions

- <Infrastructure fact that could not be verified>
```

## What to avoid

Do not include:

- local setup commands
- full CI/CD pipeline details
- release process details
- invented cloud provider
- invented environment names
- secrets, credentials, private URLs, or tokens
- detailed diagrams unless the user asks
- standalone integration deep dives

## Accuracy rules

- Do not claim production hosting unless verified.
- Do not infer cloud provider from a dependency package alone.
- Do not infer staging or production environment names unless visible.
- Do not list secrets values.
- Mention integration services only at a high level.
- If infrastructure is not represented in the repo, say so.

## Self-check

Before finishing, confirm:

- Hosting claims are evidence-backed.
- Environment names are verified or marked unknown.
- Runtime dependencies match visible config.
- CI/CD details are linked to `docs/ci-cd.md` instead of duplicated.
