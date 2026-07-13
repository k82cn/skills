# Feature Review

Use when a change adds a capability, public behavior, API, command,
configuration, integration, or user workflow.

## Establish

- Target, motivation, use cases, non-goals, and success criteria.
- Public surfaces and compatibility promises.
- Interactions with existing features, state, configuration, and workflows.
- Rollout, rollback, observability, and migration expectations.

## Check

- Implement all required behavior without expanding scope.
- Cover invalid, empty, duplicate, boundary, partial-failure, and unsupported
  states.
- Compose safely with existing defaults, flags, APIs, storage, and workflows.
- Organize design and code around clear boundaries; apply `code-style.md`.
- Check performance, security, scale, multi-tenancy, concurrency, failover, and
  recovery where relevant.
- Check user-facing APIs, CLIs, GUIs, errors, help, examples, and schemas.
- Include proportionate tests, documentation, rollout, and rollback guidance.
