---
name: code-review
description: Review designs and code, then remediate authorized findings. Use for architecture proposals, technical specifications, implementations, pull requests, commits, diffs, patches, implementation-risk assessments, review comments, and iterative review-and-fix requests. Finds behavioral, security, compatibility, concurrency, lifecycle, testing, documentation, and maintainability problems using feature, fix, or refactor workflows.
---

# Code Review

Find concrete defects and risks. Understand the change before judging it.

## Workflow

1. Identify the review target and read its supporting context: request, design,
   issue, PR description, commits, tests, and nearby documentation.
2. State the target, motivation, intended behavior, non-goals, and important
   compatibility constraints. Ask only when missing intent materially blocks the
   review.
3. Classify the primary change and read its reference:
   - `feature`: new capability or behavior. Read
     `references/code-review-feature.md`.
   - `fix`: alignment with an existing design, issue, or contract. Read
     `references/code-review-fix.md`.
   - `refactor`: structure changes that should preserve behavior. Read
     `references/code-review-refactor.md`.
4. Read `references/code-style.md` for every design and implementation review.
5. Inspect the complete change and verify uncertain behavior with focused tests,
   type checks, or reproductions when practical.
6. If edits are authorized, run the remediation loop before reporting results.

Use a conventional PR title as a classification hint: normalize `feat` to
`feature`; otherwise classify from the change's motivation. Load another
workflow only when a secondary change creates material risk.

## Review Standards

- Tie every finding to evidence, a precise source location, a failure mode, and
  user or system impact.
- Stay within the stated goal unless an omission creates real risk.
- Prefer project conventions over generic preferences.
- Check public APIs, schemas, CLIs, configuration, data formats, and visible
  behavior for compatibility.
- Check behavior changes and risk-sensitive paths for adequate tests.
- Check user, operator, integrator, and maintainer documentation when behavior
  or workflows change.
- Review the source of truth for generated, vendored, lockfile, or bulk-format
  changes when possible.
- Separate confirmed findings from questions and optional improvements.
- Do not report style preferences or speculative rewrites without concrete risk.

## Severity

- `Blocker`: severe security exposure, data corruption, broken builds, or a core
  workflow that cannot operate.
- `High`: likely production failure, user-visible regression, wrong result,
  migration failure, or important missing validation.
- `Medium`: plausible edge-case failure, reliability degradation, compatibility
  hazard, meaningful test gap, or maintainability risk.
- `Low`: worthwhile minor issue unlikely to break users.

Do not inflate severity. State what evidence is missing when impact is uncertain.

## Remediation Loop

Run this loop only when the user authorizes edits. A review-only request remains
read-only and reports findings at every severity.

1. Review and assign each confirmed finding a stable, unique ID and severity.
2. Fix in-scope medium and low findings that do not require a material product,
   API, compatibility, or design decision. Update focused tests or docs as
   needed.
3. Verify the fixes and review the updated change again.
4. Repeat until no actionable medium or low findings remain. Preserve IDs across
   passes and never reuse a resolved ID.
5. Do not fix blocker or high findings without explicit user direction. Treat
   unresolved items that need intent, authority, coordination, or a material
   decision as open questions.

After the loop, show only unresolved blocker/high findings and open questions.
Summarize resolved medium/low work and verification without restating those
findings.

## Output

Order the response as follows:

1. Findings, highest severity first.
2. Open questions or assumptions.
3. Brief summary.
4. Tests, docs, and verification checked or not run.

Use this format for each finding:

```text
ID: <stable-kebab-case-id>
Severity: <Blocker|High|Medium|Low>
Location: <file:line|document section|precise artifact location>
Comment: <failure mode, impact, and evidence>
Suggestion: <minimal fix or evidence needed>
```

If there are no findings, say so and mention residual risk or verification gaps.
