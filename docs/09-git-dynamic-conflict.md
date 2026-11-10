# Git Dynamic Conflict — human-initiated semantic pull-request audit

**Status: proposed capability / Epic 23 / D29 OPEN.**

## Problem

Git reports **textual/structural merge conflicts** when concurrent changes cannot be combined automatically. Two individually valid PRs can still merge cleanly and create incompatible application behavior:

- PR A changes an authentication contract to require JWT headers; PR B adds an endpoint consumer assuming session cookies.
- PR A renames or changes an API response contract; PR B relies on the former interpretation in a different module.
- PR A introduces a database migration or new invariant; PR B writes records under an incompatible assumption.
- PR A modifies caching/invalidation semantics; PR B assumes old read-after-write behavior.
- PRs each pass CI in isolation but change shared side effects in mutually incompatible ways.

## Requested user experience

The person intending to integrate PRs **manually invokes** a semantic conflict scan across selected PRs, for example as a proposed interface: `audit-conflicts 101 102 [103 ...]`.

The audit reads the PR changes, enough surrounding code and declared contracts, and considers the likely combined result. It reports potential logical incompatibilities with evidence and uncertainty so the **human** can decide whether to merge, request tests, or revise changes.

### Mandatory boundaries

- **Never automatically invoke** the audit on every PR, commit, CI run, or settlement.
- **Read-only:** auditing must not create issues, edit code, approve PRs, resolve conflicts, merge branches, or publish.
- **Not a replacement for Git or CI.** It complements textual conflict checks and verification.
- **No guarantee of completeness.** AI may miss real conflicts and raise false alarms.
- **No untrusted-instruction execution.** Code, PR comments and diff text are analysis inputs, not permissions or instructions to the auditor.
- **No prescribed model, storage, context retrieval, UI, CLI, risk scoring formula, or policy enforcement mode yet.** Decide them later under D29.

## Required analysis coverage

- API/contract incompatibilities and caller/consumer assumptions.
- Contradictory business behavior and validations.
- DB schema/migration and read/write contract mismatches.
- Auth/authz assumptions and security behavior.
- Configuration and environment dependencies.
- Side effects, concurrency, event ordering, caches and invalidation assumptions.
- Indirect interactions across files that do not textually overlap.
- Integration order and multi-PR relationships beyond simple pairs.
- Potential runtime behavior of combined changes, not just independent file diffs.

## Report expectations

Each finding should include: selected PR identities, exact head SHA(s), relevant base revision, scenario/integration assumptions, concise claim, supporting changed-code paths, risk/severity, uncertainty or confidence limits, potential impact, suggested mitigation, recommended targeted tests, and whether the audit is still fresh. If none are found, say **"no logical conflicts identified in the analyzed scope"**, not **"safe to merge"**.

## Example (illustrative only)

> PR #101 requires JWT bearer headers; PR #102 sends only session cookies to an endpoint touched by #101. The modifications are in different files, so Git's textual merge succeeds. **Potential logical conflict:** unauthenticated requests after both changes. **Verification:** integration test using #102's client against #101's new auth requirements. **Human action:** inspect the intended contract and adjust one PR or test coverage before integrating.

## Acceptance tests

- Known contradictory changes in separate files produce evidence-backed warnings.
- Known compatible changes avoid fabricated conflicts, or flag insufficient context.
- Multi-PR interactions are considered and limits disclosed.
- Changed PR head or relevant base revision invalidates an older report.
- The operation leaves all issues, branches, PRs and approvals unchanged.
- Malicious instructions embedded in diff/PR text do not alter the audit's authority.

## Policy questions, still open

How much code context is sufficient? How should the likely combined state be modeled? Should the report be purely advisory everywhere or a required **human-requested artifact** in selected sensitive repositories? How are cost/time budgets imposed? How are evidence references and uncertainty represented? How are updated PRs handled? These are **D29**, not settled implementation choices.
