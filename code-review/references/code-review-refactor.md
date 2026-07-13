# Refactor Review

Use when structure changes while behavior should remain stable.

## Establish

- Structural problem and intended improvement.
- Affected modules, callers, tests, and public contracts.
- Invariants: behavior, API, schema, errors, performance, and compatibility.

## Check

- Preserve every invariant and valid input path.
- Simplify ownership, structure, or extension; apply `code-style.md`.
- Keep tests focused on behavior rather than new internals.
- Avoid performance, security, scalability, concurrency, operational, or
  resource-use regressions.
