# Implementation milestones and acceptance targets

**Status:** the following milestones describe observable results, not chosen architecture, a schedule, or a promise that these features exist today. Priorities are preliminary. Resolve relevant [decisions](05-decisions-register.md) before fixing an implementation contract.

## M1 — Single developer, independent tasks

Relevant epics: E01, E02, E03, E06, E08, E09, E10, E11, E17, relevant parts of E20–E21.

**Acceptance:** One developer can request at least three independent changes, track them as separate tasks/issues, work in isolated environments, perform required local verification and submit three valid PRs without waiting for unrelated PRs' CI or merge completion. Retrying submission creates no duplicate PR. Dirty unrelated work is preserved.

## M2 — Multi-thread and dependency-aware execution

Relevant epics: E04, E05, E07, E14.

**Acceptance:** Two concurrent threads hold an explicit chain such as `1 → 2 → 3 → 4` and unrelated tasks `5–9`. The factory recognizes readiness, prevents invalid dependent execution, progresses independent work, and settles eligible tasks without violating dependency policy. Thread state remains recoverable.

## M3 — Strict asynchronous integration and recovery

Relevant epics: E12, E13, E15, E18.

**Acceptance:** PR checks are tracked accurately, policy-compliant passing PRs may integrate only under authorized strategy, failure/review blocks are reported, stale or combined-state verification is addressed per policy, and failed/partially completed attempts remain recoverable without stopping independent tasks.

## M4 — Multi-user correctness

Relevant epic: E16, with advanced E17/E20/E21 testing.

**Acceptance:** Two developers on different machines can operate concurrently against one repository. No duplicate side effects, unauthorized branch writes, hidden ownership takeover, lost modifications, or bypassed branch protections. Conflicts preserve work and escalate when unresolved.

## M5 — Reusable distribution and controlled release

Relevant epics: E19 and E22.

**Acceptance:** A different repository can adopt Gitxa through an approved installation/configuration method; all selected policies apply, task-to-PR flow works, and optional release operations provide explicit authorization, full verification, artifact identity and publication confirmation.

## Cross-cutting feature: Epic 23 — Git Dynamic Conflict

Placement into a milestone is **not yet decided**. It is not mandatory for the M1–M5 acceptance definitions above.

**Feature acceptance:** An authorized human can manually request an AI-assisted, read-only audit of 2+ PRs; it examines probable combined behavior, detects at least known fixture contradictions across separate files, returns evidence and uncertainty, ties findings to revisions, and marks results stale when inputs change. The feature makes no automatic issue, code, approval or merge changes. It never claims completeness.

## End-to-end vision acceptance

**Thread A:** tasks 1–6, where 1→2→3→4 are dependent and 5/6 independent. **Thread B:** tasks 7–9, independent of A.

Expected outcome: nine issues/tasks registered with correct dependencies; isolated implementation contexts; ready tasks progress concurrently; eligible commits/PRs are submitted without waiting for unrelated CI; required checks and protections govern merging; simple recoveries occur only within approved bounds; failures preserve all useful work; final status distinguishes merged, blocked, queued, pending CI, and ready-for-release states. The human reviewer may separately request a cross-PR semantic audit before merging.

## Release is not merge

Merging a PR must not automatically imply publishing a version or releasing a package. Publication requires its own explicit requirements and authority policy.
