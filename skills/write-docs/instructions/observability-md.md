# `docs/observability.md` instruction

## Purpose

Document how the project is monitored, logged, traced, alerted, and debugged.

This doc should help agents avoid blind debugging and understand where runtime signals are produced.

## Output file

```text
docs/observability.md
```

## When to create or update

Create this file only when approved and observability tooling or conventions are detected.

Recommend it when the repo has:

- structured logging
- metrics
- tracing
- dashboards
- error tracking
- alerting
- health checks
- job monitoring
- incident/runbook docs

## Sources to inspect

- logging configuration
- metrics configuration
- tracing/OpenTelemetry configuration
- Sentry, Datadog, New Relic, CloudWatch, Azure Application Insights, Grafana, Prometheus, or similar setup
- health check routes
- deployment config
- infrastructure config
- existing docs
- CI/CD deployment jobs
- user-provided context

## Required content

Cover what can be verified:

1. Logging approach.
2. Error tracking.
3. Metrics.
4. Tracing.
5. Health checks.
6. Dashboards or alerting.
7. Background job visibility.
8. Common debugging entry points.

## Recommended structure

```markdown
# Observability

## Summary

<Short overview or `Not documented yet`.>

## Logging

- <Logging tool/pattern>

## Error tracking

- <Tool or Not documented yet>

## Metrics

- <Tool or Not documented yet>

## Tracing

- <Tool or Not documented yet>

## Health checks

- `<endpoint or command>` — <purpose>

## Dashboards and alerts

- <Dashboard/alerting system or Not documented yet>

## Debugging notes

- <Verified note>
```

## What to avoid

Do not include:

- private dashboard URLs
- credentials
- generic debugging advice
- invented dashboards
- invented alerting policies
- infrastructure details unrelated to observability

## Accuracy rules

- Do not claim a monitoring provider is used unless config, dependencies, docs, or user context confirm it.
- Do not expose private URLs or secrets.
- Do not claim alerting exists unless visible.
- If only basic logging exists, keep the doc short.

## Self-check

Before finishing, confirm:

- Tools listed are verified.
- No private secrets or URLs are exposed.
- Unknown observability areas are marked clearly.
- The doc does not duplicate infrastructure details.
