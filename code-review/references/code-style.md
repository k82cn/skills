# Code Style Review

Use when reviewing code organization, design patterns, refactors, or whether a
feature implementation can be simplified. This reference condenses high-level
lessons from refactoring practice and GoF design patterns into review guidance.

## Principles

- Preserve behavior first. Refactoring and pattern changes must not change
  observable behavior unless the PR is explicitly a feature or fix.
- Make intent obvious through names, boundaries, and control flow.
- Keep changes small enough to review. Prefer a sequence of clear local
  transformations over a broad rewrite.
- Reduce duplication by extracting a real concept, not by hiding unrelated code
  behind a generic helper.
- Prefer composition and narrow interfaces over shared mutable state,
  inheritance-heavy structure, or broad abstractions.
- Encapsulate variation only at real variation points: behavior, construction,
  state transitions, adaptation, observation, or orchestration.
- Use GoF patterns as vocabulary and tools, not goals. A pattern is useful only
  when it reduces complexity, duplication, or risk.
- Keep distributed-system state transitions explicit: ownership, lifecycle,
  retries, idempotency, cancellation, timeouts, and cleanup should be visible.

## Review Smells

- Duplicated logic that must change together.
- Long functions or large components mixing policy, orchestration, I/O, and
  state mutation.
- Repeated conditionals over type, mode, state, or backend.
- Construction logic scattered across callers.
- Code that knows too much about another component's internals.
- Small changes requiring edits across many unrelated files.
- Hidden state transitions, implicit ordering, or unclear ownership.
- Abstractions with only one unclear use or names that do not match the domain.

## Pattern Guidance

- Factory or Builder: use when construction has meaningful variants, defaults,
  validation, or setup sequencing.
- Strategy: use when behavior varies by policy, backend, mode, or tenant and
  repeated branching is growing.
- State: use when valid behavior depends on lifecycle state and transitions must
  be explicit.
- Adapter or Facade: use when external APIs, clients, or subsystems need a stable
  local boundary.
- Observer or Mediator: use when event propagation or component coordination is
  scattered, but avoid hiding critical ordering or failure handling.
- Template Method or Command: use only when it clarifies repeated workflow
  structure without making control flow harder to trace.

## Review Rule

Suggest a refactor or design pattern only when the current code creates concrete
risk: repeated bugs, difficult extension, unclear ownership, duplicated logic,
unsafe state handling, or hard-to-test behavior. Prefer the smallest design move
that solves that risk.
