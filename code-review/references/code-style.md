# Design and Code Style

Apply these rules to design artifacts and implementations.

## Principles

- Make intent, ownership, boundaries, and state transitions explicit.
- Prefer small, composable components and narrow interfaces.
- Extract real concepts; do not hide unrelated behavior behind generic helpers.
- Keep lifecycle, retries, idempotency, cancellation, timeouts, and cleanup
  visible.
- Use patterns to reduce risk and complexity, not as decoration.

## Avoid Conditional Dispatch

Treat centralized branching over behavior, type, mode, backend, construction,
or lifecycle state as a maintainability and extension risk. Each new variant
modifies shared dispatch, couples implementations, and may duplicate rules.

Prefer:

- Interface or Strategy for behavior variants.
- Factory or Builder for construction variants.
- State pattern or explicit state machine for lifecycle transitions.
- Adapter or Facade for unstable external boundaries.
- Observer or Mediator for scattered coordination, while keeping ordering and
  failure handling visible.

Report conditional dispatch as a finding when it selects extensible behavior,
construction, or state transitions. Apply the rule to both architecture and
code.

Keep local validation, preconditions, error handling, boundary checks, and short
guard clauses. Do not add a pattern that only moves one binary decision or adds
indirection without a useful extension or test boundary.

## Other Smells

- Logic duplicated across places that must change together.
- Functions or components mixing policy, orchestration, I/O, and mutation.
- Construction scattered across callers.
- Hidden transitions, ordering, ownership, or mutable state.
- Small changes requiring edits across unrelated modules.
- Abstractions with one unclear use or names that do not match the domain.
