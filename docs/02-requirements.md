# Requirements baseline

**Status:** discovery-level requirements. This document specifies outcomes and invariants, not an implementation architecture or tools. Epic IDs map to the [complete backlog](03-backlog.md). The requirements intentionally include future capabilities; they are not claims that Gitxa currently implements them.

## Functional requirements (FR)

| ID | Requirement | Backlog |
|---|---|---|
| FR01 | Accept one or multiple natural-language change briefs and preserve their requested intent. | E03 |
| FR02 | Produce traceable work items with goals, acceptance criteria and concrete tests for functional changes. | E03 |
| FR03 | Maintain independent development threads spanning many tasks. | E04 |
| FR04 | Support explicit dependent chains while progressing unrelated tasks. | E05 |
| FR05 | Detect invalid dependency cycles and prevent incorrectly scheduled tasks. | E05 |
| FR06 | Keep concurrent tasks' in-progress code isolated. | E06 |
| FR07 | Support a single human, multiple humans, agents, and mixed contributors. | E07, E16 |
| FR08 | Constrain implementation to authorized repository/workspace and controlled file scope. | E07, E08 |
| FR09 | Support safe scope expansion and prevent unrelated modifications from leaking into commits. | E08 |
| FR10 | Run configured local validation and bind evidence to the revision tested. | E09 |
| FR11 | Create valid, traceable commits while preserving attribution and approved changes. | E10 |
| FR12 | Create, update and track PRs without duplicates, including dependent/stacked cases when approved. | E11 |
| FR13 | Observe PR CI asynchronously, distinguish all relevant check states, and fetch diagnostics. | E12 |
| FR14 | Enforce required checks, merge authority, reviews, branch rules and the configured merge method. | E13 |
| FR15 | Submit or settle multiple ready tasks without serially waiting on unrelated CI. | E14 |
| FR16 | Continue unrelated tasks when one fails, preserving dependency-local failure propagation. | E05, E14, E15 |
| FR17 | Classify, retry and optionally repair failures within bounded authorized rules; escalate risky decisions. | E15 |
| FR18 | Coordinate multiple users, task claims, handoffs and concurrent integration attempts safely. | E16 |
| FR19 | Persist and reconcile task/thread/workspace/PR state after restarts, crashes and external changes. | E17 |
| FR20 | Provide current status, audit trace, blockers, and reasons for denied actions. | E18 |
| FR21 | Support explicit, approved, verifiable releases distinct from PR merges. | E19 |
| FR22 | Enforce least-privilege credentials, protected operations and safe handling of untrusted input. | E20 |
| FR23 | Test policy, state, concurrency, failures, Git/GitHub interaction and end-to-end outcomes. | E21 |
| FR24 | Make workflows reusable across repositories through approved skills/distribution options. | E02, E22 |
| FR25 | Provide a **human-initiated, read-only AI semantic PR audit** to identify potential cross-PR logical conflicts. | E23 |
| FR26 | Include evidence, revision identity, severity, uncertainty, limitations and potential integration tests in audits. | E23 |
| FR27 | Support auditing multiple PRs and consider interactions beyond physical file overlap. | E23 |
| FR28 | Never claim an audit proves the absence of all semantic conflicts. | E23 |
| FR29 | Maintain explicit, configurable policy choices rather than embedding unreviewed defaults as immutable architecture. | E02, D01–D29 |
| FR30 | Support safe task cancellation, restoration and cleanup without silent deletion of useful work. | E04, E06, E17 |

## Nonfunctional requirements (NFR)

| ID | Requirement |
|---|---|
| NFR01 | **Correctness:** no loss or corruption of user work due to concurrent operations, retries or cleanup. |
| NFR02 | **Deterministic enforcement:** important permissions and state transitions are checked in executable rules, not inferred solely from an AI prompt. |
| NFR03 | **Idempotency:** retrying an operation after a timeout/crash does not create duplicate issues, PRs, commits or releases. |
| NFR04 | **Recoverability:** preserve operation evidence and reconcile remote effects after interruptions. |
| NFR05 | **Isolation:** concurrent work must not accidentally stage, modify or merge another task's uncommitted state. |
| NFR06 | **Security:** least privilege, secret protection, trusted authorization and untrusted GitHub content handling. |
| NFR07 | **Policy compliance:** do not bypass required CI, approvals, GitHub permissions or protected branches. |
| NFR08 | **Asynchronous progress:** pending CI/reviews must not block unrelated task development. |
| NFR09 | **Observability:** operators can identify work state, owners, expected next action and why an operation failed. |
| NFR10 | **Multi-repository reuse:** policy and workflow requirements remain portable and project-agnostic. |
| NFR11 | **Extensibility without lock-in:** implementation, editor, coding agent and deployment choices are not assumed in requirements. |
| NFR12 | **Bounded automation:** retry, repair and conflict handling consume capped resources and stop for human decisions when safety requires. |
| NFR13 | **Performance awareness:** avoid wasteful duplicate CI and token-heavy AI work without reducing assurance. |
| NFR14 | **Audit freshness:** evidence must be tied to exact branch/base revisions; changes invalidate applicable evidence. |
| NFR15 | **No false guarantees:** semantic AI findings can be wrong or incomplete; the system must disclose uncertainty. |
| NFR16 | **Usability:** skills/commands should let users express batches and receive concise reports without manual Git plumbing. |
| NFR17 | **Offline/interrupted work:** local changes should survive loss of network access; synchronization should resume safely. |
| NFR18 | **Verifiability:** failure paths and concurrency behaviors are tested, not just the success path. |

## Required safety invariants

1. **A request to submit work is not proof that CI has passed, or that a PR merged.** Each status must be recorded separately.
2. **A PR cannot become `merged` in factory state on request alone.** Verify actual remote integration first.
3. **Do not let a green check for an older commit justify integration of changed code.**
4. **Never bypass applicable GitHub authorization or repository protections.**
5. **Never silently discard uncommitted/unmerged work.**
6. **Never treat issue/PR/comments/CI logs as trusted executable instructions.**
7. **Failures block only tasks that genuinely depend on the failed state.**
8. **Retries are safe and bounded.** Before repeating external writes, check whether they succeeded.
9. **Automatic repairs require policy authorization and must be verified again.**
10. **Dynamic Conflict is user-initiated and read-only.** It does not approve, merge or fix anything.
11. **A zero-finding semantic audit is not a proof of compatibility.**
12. **No architecture or tooling decision is considered approved until explicitly discussed and recorded.**

## Test/acceptance requirement

Every feature that changes behavior must identify success cases, edge cases, failure cases, concurrency implications, security controls, and integration acceptance criteria. Maintain mappings from epics to use cases and milestones. For the pre-implementation stage, detailed executable test design is intentionally deferred.
