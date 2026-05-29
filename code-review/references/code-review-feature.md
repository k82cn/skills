# Code Review Feature Workflow

Use when `review.type` is `feature`: the PR adds a new function, capability,
public behavior, API, command, configuration, integration, or user workflow.

## Properties

Set or refine these properties before evaluating defects:

- `feature.target`: intended new function, user problem, and success criteria.
- `feature.motivation`: why the new function is being added now.
- `feature.scope`: use cases, non-goals, and design requirements that define
  what must be implemented.
- `feature.public_surface`: UI, API, CLI, config, schema, event, permission,
  integration, or operational contract exposed by the feature.
- `feature.interactions`: existing features, controllers, workflows, APIs, or
  data paths that can interact with the new function.
- `feature.rollout`: migration, feature flag, default, deployment, downgrade,
  and observability expectations.

## Workflow

1. Review, identify, and clarify the intent, motivation, scope, and use cases of
   the feature before judging the implementation.
   - Confirm the target is clear.
   - Confirm the implementation stays inside the intended scope while covering
     required use cases.
2. Check MR completeness. The MR should include implementation, unit tests, and
   documentation when the feature changes behavior, contracts, operations, or
   user workflows.
   - Confirm implementation, unit tests, and docs are included or explicitly
     unnecessary.
3. Review feature function:
   - Check that all feature behavior required by the design is implemented.
   - Check edge cases and negative cases, including invalid inputs, empty or
     missing data, duplicates, boundary values, partial failures, and unsupported
     states.
   - Check interactions with existing features, including shared state,
     configuration, compatibility, ordering, defaults, and behavior when features
     are enabled together or independently.
   - Check whether the new function composes safely with existing features,
     flags, defaults, APIs, storage paths, and workflows.
   - Check whether code and components are well organized through existing local
     design patterns, GoF design patterns, architecture, or a focused
     abstraction that reduces real complexity, duplication, or state handling
     risk. Use `references/code-style.md` for this check.
   - Avoid suggesting patterns or abstractions that overgeneralize or hide
     important control flow.
4. Review system behavior:
   - Performance and throughput: check whether latency, memory, CPU, I/O,
     watch/list pressure, queue length, cache churn, hot-path allocations, or
     throughput can get worse.
   - Security: check authn/authz, input validation, secret handling,
     auditability, and trust boundaries.
   - Scalability and multi-tenancy: check behavior as tenants, objects, nodes,
     regions, or request volume grow.
   - Race conditions: check concurrent requests, retries, event reordering,
     leadership changes, stale caches, and partial failures.
   - High availability and failover: check availability during node, process,
     leader, network, dependency, or zone failure, and safe recovery after
     failover.
5. Review UI/UX surfaces:
   - CLI behavior, flags, defaults, errors, and help text.
   - GUI flows, states, errors, and discoverability.
   - API references, examples, schemas, and compatibility.
   - Confirm user-facing surfaces are understandable and compatible.
6. Review operations:
   - Backward compatibility.
   - Rollout plan and rollout steps.
   - Rollback steps, including feature flags when applicable.
   - Confirm backward compatibility, rollout steps, and rollback steps are clear
     and safe.
