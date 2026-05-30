# Code Review Fix Workflow

Use when `review.type` is `fix`: the PR aligns implementation with the intended
design, specification, issue, expected behavior, or documented contract.

## Properties

Set or refine these properties before evaluating defects:

- `fix.design`: intended design, specification, issue, expected behavior, or
  documented contract.
- `fix.mismatch`: where the current implementation diverges from that design.
- `fix.evidence`: failing test, reproduction steps, issue detail, log, user
  report, or code path proving the mismatch.
- `fix.expected_behavior`: behavior after implementation and design are aligned.
- `fix.source_pr`: original PR, commit, release branch change, or upstream patch
  when the fix is a cherry-pick or backport.
- `fix.source_equivalence`: whether the cherry-pick or backport matches the
  original fix exactly.

## Workflow

1. Review, identify, and clarify the issue the MR is intended to fix.
   - Identify the intended design, specification, issue, expected behavior, or
     documented contract.
   - Identify where the current implementation diverges from that target.
   - Identify the evidence for the issue, such as failing tests, reproduction
     steps, issue details, logs, user reports, or code paths.
2. Check MR completeness. The MR should include implementation, unit tests, and
   documentation when the fix changes behavior, contracts, operations, or user
   workflows.
   - Check that tests prove the original issue or implementation/design mismatch.
   - If a unit test cannot capture the issue, require the narrowest useful
     integration or end-to-end test and explain why.
3. Review the fix:
   - Check that the MR fixes the original issue and aligns implementation with
     the intended design.
   - If the fix is labeled, titled, described, or structured as a cherry-pick or
     backport, identify the original PR or commit and compare the implementation
     against it. The fix should be exactly the same as the original PR. Treat any
     code, test, documentation, behavior, or dependency difference as a finding
     unless the MR explicitly justifies a target-branch compatibility adjustment.
   - Check that the implementation does not break existing features, valid
     inputs, compatibility, or dependent workflows.
   - Check that the implementation only focuses on fixing the issue, without
     extra fixes, unrelated cleanup, or new features.
   - Check that the fix is as simple as possible while still being correct.
   - Check that the fix has no system impact, including performance, security,
     scalability, concurrency, operational behavior, or resource usage.
   - Check that the fix introduces no backward compatibility issue.
