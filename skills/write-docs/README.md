# write-docs

A skill package for creating accurate, project-specific documentation for AI coding agents and human maintainers.

## Structure

```text
write-docs/
  SKILL.md
  instructions/
    # Root-level and per-folder docs
    agents-md.md
    feature-readme-md.md

    # Required project docs
    ci-cd-md.md
    domain-md.md
    infrastructure-md.md
    local-development-md.md
    product-md.md

    # Optional project docs
    architecture-md.md
    observability-md.md
    release-md.md
    security-md.md
    testing-md.md

    # Per-area conventions
    conventions-md.md

    # Review mode
    review.md
```

## Usage

Install or copy this folder into the skill location supported by your coding agent.

The skill orchestrates documentation work and uses the files in `instructions/` as focused writing specifications for individual target documents. `review.md` drives Review mode, which audits existing project docs before any changes are written. Orchestration templates (fact base, structure proposal, worker prompt, final response) live inline in `SKILL.md`.
