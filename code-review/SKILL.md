---
name: code-review
description: Structured code review workflow based on k82cn's distributed systems experience, first understanding the target and motivation of a change, then routing to feature, fix, or refactor review workflows to find bugs, regressions, security issues, API or data contract problems, concurrency and lifecycle hazards, missing tests, and missing documentation updates. Use when the user asks to review code, review a pull request, inspect a diff or patch, assess recent changes, evaluate implementation risk, or provide review comments rather than directly implementing a change.
---

# Code Review

## Overview

Review code as a defect-finding pass, not as a general commentary exercise.
Start by understanding what the change is trying to accomplish and why.
Prioritize concrete behavioral risks with file and line references, then mention
unit test, documentation, or residual uncertainty gaps.

## Workflow Properties

Before deep review, classify the PR into exactly one review workflow whenever
possible:

- `feature`: new function, capability, public behavior, API, command,
  configuration, integration, or user workflow.
- `fix`: align the implementation to the intended design, specification, issue,
  expected behavior, or documented contract.
- `refactor`: code refactor that should preserve behavior while improving
  structure, ownership, readability, or maintainability.

When a PR title follows `<type>([optional scope]): <description>`, use it as a
classification hint. Normalize `feat` to `feature`. Ignore other title types as
workflow names and classify from the target and motivation instead.

Set these properties from the PR title, user request, PR body, issue, commit
message, labels, branch name, or changed files:

- `pr.title.type`: parsed PR title type, when present.
- `pr.title.scope`: optional parsed scope, when present.
- `pr.title.description`: parsed title description, when present.
- `review.target`: what the PR is intended to change.
- `review.motivation`: why the change exists.
- `review.type`: `feature`, `fix`, or `refactor`.
- `review.workflow`: selected type-specific reference path, plus any additional
  reference paths loaded for material secondary risk.

Load the workflow reference according to `review.workflow`:

- `feature`: set `review.workflow` to `references/code-review-feature.md`.
- `fix`: set `review.workflow` to `references/code-review-fix.md`.
- `refactor`: set `review.workflow` to `references/code-review-refactor.md`.

If the PR contains multiple kinds of work, identify the primary motivation and
set `review.type` from that. Note secondary concerns in the review, but do not
load unrelated workflows unless the secondary change materially affects risk.

If `review.type` is unclear, infer conservatively from PR metadata and changed
behavior. Ask a clarifying question only when the target or motivation cannot be
discovered and that uncertainty would materially affect the review.

## Entrypoint Workflow

1. Identify the review target: branch diff, PR, commit, staged changes, file list,
   or pasted code.
2. Understand the target and motivation before judging the implementation. Read
   the user request, PR title/body, issue, design note, commit message, or nearby
   discussion to identify the intended behavior, non-goals, and success criteria.
3. Set `review.type` to `feature`, `fix`, or `refactor`, then load the matching
   workflow reference before continuing.
4. Read the primary type-specific workflow reference:
   - `feature`: `references/code-review-feature.md`
   - `fix`: `references/code-review-fix.md`
   - `refactor`: `references/code-review-refactor.md`
5. Load an additional type-specific workflow reference when a secondary change
   materially affects risk.
6. Delegate type-specific review execution and checks to the loaded references.
7. When reviewing code organization, design patterns, or refactoring quality,
   also read `references/code-style.md`.
8. Apply the common standards, severity, and output format below.

## Common Standards

- Treat review as evidence-based. Every finding should cite the changed file and
  line, explain the failure mode, and state why it matters.
- Anchor the review in the change's target and motivation. Avoid rejecting an
  implementation for not doing work outside the stated goal unless that omission
  creates a real risk.
- Avoid low-signal style comments unless style creates ambiguity, bugs, or
  maintenance risk in the touched code.
- Do not request changes for hypothetical rewrites when the current approach is
  sound.
- Distinguish confirmed issues from questions, assumptions, and optional
  improvements.
- Prefer local project conventions over generic preferences.
- Consider backwards compatibility for public APIs, schemas, CLIs, config files,
  data formats, and user-visible behavior.
- Treat missing or stale unit tests as a review finding when the change affects
  behavior, contracts, or risk-sensitive paths.
- Treat missing or stale docs as a review finding when users, operators,
  integrators, or future maintainers need updated guidance to use the change
  correctly.
- For generated code, lockfiles, vendored code, or bulk formatting changes,
  review the generator/source of truth when possible.
- When a finding depends on runtime behavior, try to verify it with tests,
  typechecks, focused commands, or minimal reproduction steps.

## Severity

- Blocker: change can corrupt data, expose secrets, break builds, prevent core
  workflows, or create a severe security issue.
- High: likely user-visible regression, production failure, incorrect result,
  migration problem, or important missing validation.
- Medium: plausible edge-case failure, degraded reliability, compatibility
  hazard, or meaningful missing test coverage.
- Low: minor issue worth fixing but unlikely to break users.

Do not inflate severity. If impact is uncertain, say what evidence would confirm
it.

## Output Format

Use this order:

1. Findings, highest severity first.
2. Open questions or assumptions, including unclear target or motivation.
3. Brief summary, only after findings.
4. Tests, docs, or verification checked, including anything not run or not
   present.

Use this template for each finding:

```text
ID: <short-stable-name>
Severity: <Blocker|High|Medium|Low>
Location: <file:line>
Comment: <concrete failure mode, why it matters, and the evidence from the diff>
Suggestion: <minimal fix direction, test/doc update, or verification step>
```

- Use a short kebab-case `ID` that names the issue, such as
  `stale-leader-cache` or `missing-retry-test`.
- Keep IDs unique and stable for the entire review session so follow-up feedback
  can reference them without ambiguity. Do not reuse an ID for a different
  finding, even across later review updates in the same session.
- Keep `Comment` focused on the review finding, not general explanation.
- Keep `Suggestion` actionable. If no fix is obvious, state the evidence needed
  to decide safely.
- Do not include findings that cannot be tied to a concrete risk.

If there are no findings, say so directly and mention residual risk or test gaps.

## When Asked To Fix

If the user asks to both review and fix issues, review first, then implement only
the confirmed fixes that are in scope. Avoid sweeping refactors unless they are
needed to resolve a finding safely.
