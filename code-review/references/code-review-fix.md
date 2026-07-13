# Fix Review

Use when a change aligns implementation with an existing design, issue,
expected behavior, or documented contract.

## Establish

- Intended behavior and the current mismatch.
- Evidence: failing test, reproduction, issue, log, report, or code path.
- Expected behavior after the fix.
- For a backport or cherry-pick, the source change and allowed target-branch
  differences.

## Check

- Fix the proven mismatch completely and no more.
- Add a test that fails for the original defect; use the narrowest useful
  integration test when a unit test cannot prove it.
- Preserve valid behavior, compatibility, and dependent workflows.
- Avoid unrelated cleanup, fixes, or features.
- Match a backport or cherry-pick to its source exactly unless a documented
  compatibility adjustment is required.
- Check performance, security, scale, concurrency, operations, and resource use
  where relevant.
