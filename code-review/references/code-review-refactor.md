# Code Review Refactor Workflow

Use when `review.type` is `refactor`: the PR changes code structure while
intending to preserve behavior.

## Properties

- `refactor.target`: structure, abstraction, ownership, or readability problem
  the PR addresses.
- `refactor.invariant`: behavior, API, schema, performance, or error semantics
  that must remain unchanged.
- `refactor.surface`: modules, callers, tests, and public contracts affected by
  the move or rewrite.

## Workflow

1. Review, identify, and clarify the feature and scope the MR is intended to
   refactor.
   - Identify the modules, callers, tests, and public contracts affected by the
     refactor.
   - Identify the behavior, API, schema, performance, error semantics, and
     compatibility expectations that must remain unchanged.
2. Check MR completeness. The MR should include implementation and unit tests
   when the refactor touches behavior-sensitive paths or public contracts.
   - Check that tests preserve the expected behavior instead of only matching
     new internals.
3. Review the refactor:
   - Check that the MR refactors code without changing behavior.
   - Check that the refactor does not break existing features, valid inputs,
     callers, or dependent workflows.
   - Check that the refactor simplifies the code or makes it more flexible. Use
     `references/code-style.md` for this check.
   - Check that the refactor has no system impact, including performance,
     security, scalability, concurrency, operational behavior, or resource usage.
   - Check that the refactor introduces no backward compatibility issue.
