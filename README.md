# AI Coding Playbook

My rules, skills, prompts, and workflows for practical AI-assisted software development.

This repository is the practical companion to [The Copilot's Log](https://www.linkedin.com/newsletters/7355571647858229250/?displayConfirmation=true), my newsletter about using AI coding tools in real projects without the hype.

The goal is not to vibe-code everything and hope for the best.

The goal is to use AI like a fast assistant: give it good context, keep the work reviewable, and stay in control of the final result.

## What is in this repo?

This repo contains reusable material for working with AI coding agents. Some skills are original, and some are adapted from other public skill collections with attribution.

```text
skills/
  grill-me/
  summarize/
  summarize-debugging/
  summarize-for-review/
  to-issues/
  to-prd/
  write-docs/
```

More folders may be added over time for rules, prompts, examples, and tool-specific workflows.

## Skills

### `grill-me`

Stress-tests a plan or design by asking one question at a time.

Useful when you want an AI agent to challenge your assumptions, walk through trade-offs, and turn a vague idea into a clearer implementation plan.

### `summarize`

Summarizes long conversations, documents, or context into something easier to reuse.

Useful before starting a new chat or handing context to another agent.

### `summarize-debugging`

Summarizes a debugging session.

Useful when a bug investigation gets long and you want to preserve what was tried, what failed, what was learned, and what should happen next.

### `summarize-for-review`

Summarizes changes for review.

Useful before opening a pull request or asking another developer, or another agent, to review the work.

### `to-issues`

Turns a plan, idea, or conversation into implementation issues.

Useful when you want to break work into smaller, trackable tasks.

### `to-prd`

Turns a rough product idea into a product requirements document.

Useful before implementation, especially when the feature is still vague.

### `write-docs`

Creates or updates project documentation.

Useful when you want an agent to inspect a codebase and produce practical docs such as product overview, domain glossary, local development instructions, infrastructure notes, and CI/CD documentation.

## Principles

These materials follow a few rules:

- Keep context focused.
- Prefer small, reviewable changes.
- Make the agent ask when requirements are unclear.
- Do not invent project facts.
- Use documentation and rules to reduce repeated prompting.
- Treat AI output like a pull request from a very fast junior developer.
- Review, build, test, and verify before trusting the result.

## How to use this repo

Copy the skill, rule, or prompt you need into the tool you use.

Different tools support different formats, so some adaptation may be needed.

Examples:

- Claude Code skills can use folders with a `SKILL.md`.
- Cursor can use project rules or custom instructions.
- GitHub Copilot can use repository instructions.
- Other agents can usually reuse the markdown as prompt context.

## Recommended starting point

Start with:

```text
skills/grill-me/
skills/write-docs/
```

`grill-me` helps before implementation, when the idea still needs pressure-testing.

`write-docs` helps after or during implementation, when the project needs durable context for humans and AI agents.

## The Copilot's Log

[The Copilot's Log](https://www.linkedin.com/newsletters/7355571647858229250/?displayConfirmation=true) is my newsletter about practical AI-assisted software development.

In the newsletter, I write about the ideas behind these skills and workflows: how to use AI coding tools without hype, how to review AI-generated code, how to manage context, and how to keep developers in control.

The repo is where I keep the reusable pieces.

The newsletter is where I explain the thinking behind them.

## Why this exists

I use AI coding tools daily, but I do not treat them as magic.

They are useful because they are fast, not because they are always right. Good workflows matter: planning, scoped prompts, clear documentation, tests, code review, and boring engineering discipline.

This repo is where I collect the reusable parts of that workflow.

## Acknowledgements

Some of the skills in this repository are adapted from [Matt Pocock's skills repository](https://github.com/mattpocock/skills).

Matt's work was the starting point for several of these workflows. I copied the ideas that were useful to me, changed the instructions to match my own preferences, and added extra guardrails where I wanted the agents to behave differently.

I'll write more in [The Copilot's Log](https://www.linkedin.com/newsletters/7355571647858229250/?displayConfirmation=true) about what I changed, why I changed it, and how these skills fit into my AI-assisted coding workflow.

## About me

I'm [Bogdan Bujdea](https://bogdanbujdea.dev), a software engineer and former Microsoft MVP focused on practical AI-assisted software development, .NET, Azure, and developer workflows.

## License

This repository is licensed under the MIT License. See [LICENSE.txt](LICENSE.txt).
