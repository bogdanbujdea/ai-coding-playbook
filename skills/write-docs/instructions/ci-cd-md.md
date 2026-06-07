# `docs/ci-cd.md` instruction

## Purpose

Document the repository's continuous integration and continuous delivery/deployment behavior.

This doc should describe actual pipelines and jobs, not a desired pipeline.

## Output file

```text
docs/ci-cd.md
```

## When to create or update

Create this file by default for project documentation tasks, but keep it short if no CI/CD configuration is found.

## Sources to inspect

Look for:

- `.github/workflows/*`
- `.gitlab-ci.yml`
- `azure-pipelines.yml`
- `.circleci/config.yml`
- Buildkite config
- Jenkinsfile
- Drone config
- Bitbucket pipelines
- deployment scripts
- package scripts used by pipelines
- infrastructure deployment workflows
- existing docs

## Required content

Cover what can be verified:

1. CI/CD system used.
2. Pipeline files.
3. Pipeline triggers.
4. Validation jobs: build, test, lint, typecheck, security scans.
5. Deployment jobs.
6. Required services or job dependencies.
7. Secrets and variables by name only, if visible.
8. Manual gates or approvals, if visible.
9. Relationship to release process, if relevant.

## Recommended structure

```markdown
# CI/CD

## System

- CI/CD provider: <provider or Not documented yet>
- Pipeline config files:
  - `<path>`

## Pipelines

### <Pipeline name>

Triggers:
- <trigger>

Jobs:
- `<job>` — <what it does>

Deployment:
- <environment or Not documented yet>

Required variables/secrets:
- `<NAME>` — <purpose if visible>

## Validation commands

- `<command>` — <where it runs>

## Notes

- <Verified pipeline note>

## Open questions

- <CI/CD behavior that could not be verified>
```

## What to avoid

Do not include:

- deployment claims not visible in pipeline config or docs
- secret values
- assumed branch strategy
- assumed release process
- generic CI/CD advice
- full infrastructure documentation
- commands that do not appear in scripts, jobs, or docs

## Accuracy rules

- Document only actual pipeline files and jobs.
- Do not infer deployment from a job name unless the steps confirm it.
- Do not say a job is required unless the config shows it as part of the pipeline.
- Do not say a pipeline blocks merge unless branch protection or docs confirm it.
- Use `Not documented yet` for unknown approvals, gates, or secrets.
- Mention secrets by name only when names are present in config.

## Self-check

Before finishing, confirm:

- Pipeline file paths are correct.
- Triggers are accurately described.
- Job names match config.
- Deployment details are not guessed.
- Release details are linked to `docs/release.md` if that file exists.
