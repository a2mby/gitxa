# Open decisions register — D01–D29

**All entries are OPEN. No choices have been approved.** In particular, discussion examples of TypeScript, a CLI, worktrees, GitHub Apps, hosted orchestration, squash merges, auto-merge, merge queues, YAML configuration, or a database are not an architecture contract.

For each decision, eventually record: alternatives, trade-offs, user/owner choice, implications, verification requirements, and references. Resolve **one decision at a time** before implementation uses it.

| ID | Decision | Questions to resolve | Status |
|---|---|---|---|
| D01 | Configuration ownership | Global defaults, per-repo overrides, non-overridable constraints; who can edit policy? | OPEN |
| D02 | Task identity | GitHub issue as canonical ID, internal ID, or compound identity; cross-repo uniqueness? | OPEN |
| D03 | Thread identity | Local conversation/thread, remotely shared entity, or hybrid; how to resume? | OPEN |
| D04 | Task dependency strategy | Wait until prerequisite merges, stacked unmerged branches, or hybrid? | OPEN |
| D05 | Branch base strategy | Latest `main`, predecessor branch, integration branch, or configurable? | OPEN |
| D06 | Workspace isolation | Worktrees, clones, other isolated environment, or hybrid? | OPEN |
| D07 | Concurrency capacity | Fixed task limits, user-configured quotas, resource-sensitive scheduling? | OPEN |
| D08 | Task ownership | Claims, exclusive owner, shared owner, role-based handoff? | OPEN |
| D09 | File scope enforcement | Strict allowlist, advisory list with controlled expansion, sensitive-file rules? | OPEN |
| D10 | Local verification | Full checks, relevant checks, task-type profiles; who determines required gates? | OPEN |
| D11 | Commit strategy | One commit, multiple commits, user choice, required format? | OPEN |
| D12 | PR strategy | PR per task, grouped PR, stacked PR; when is grouping safe? | OPEN |
| D13 | PR approval authority | Required human reviews, self-review rules, automated recommendation versus formal approval? | OPEN |
| D14 | Merge authority | Can local skill request merge, only GitHub UI, or configurable by actor/task/repo? | OPEN |
| D15 | Merge method | Squash, regular merge commit, rebase, or policy-dependent? | OPEN |
| D16 | Stale branch handling | Always update, update when required, integrate via queue, or another mechanism? | OPEN |
| D17 | CI strictness | Required checks, commit binding, combined-state verification, branch rules and bypass prohibition? | OPEN |
| D18 | Automatic CI failure repair | Allowed classes, retry budget, required permissions, tests after repair? | OPEN |
| D19 | Conflict handling | Which conflicts can be repaired automatically, what must go to a human? | OPEN |
| D20 | Batch settlement semantics | Per-task PRs, grouped/atomic integration, readiness and partial completion? | OPEN |
| D21 | Failure isolation | Propagate blockers at task, dependency chain, thread or repo level? | OPEN |
| D22 | State persistence | Local files, database, GitHub, hybrid; source of truth and recovery protocol? | OPEN |
| D23 | Multi-user coordination | Claims, locking/leases, identities, permissions, consistency and race handling? | OPEN |
| D24 | Release authorization | Human approval, automated release, publish prerequisites, separation of duties? | OPEN |
| D25 | Audit history | GitHub as log, separate event history, retention and evidence requirements? | OPEN |
| D26 | Cleanup policy | Immediate or deferred cleanup; safeguards for dirty/unmerged work? | OPEN |
| D27 | Skill portability | One provider-specific skill, provider-independent interface, or optional adapters? | OPEN |
| D28 | Packaging and distribution | Local scripts, installable CLI, package manager, shared binary, hosted agent, or hybrid? | OPEN |
| D29 | Git Dynamic Conflict policy | On-demand invocation scope, context gathering, combined-state analysis, report format, coverage/uncertainty, advisory versus required report for selected repos? | OPEN |

## Additional unresolved questions implied by the backlog

These are **not decisions already settled** and should be considered when addressing relevant D-entries:

- What constitutes a safe enough edit to make automatically? Who authorizes a repair agent?
- How are equivalent/repeated user requests detected without confusing distinct intent?
- How are merged PRs, issue closures, branch deletions and local state reconciled without duplicate side effects?
- How are composed changes verified if individually passing PRs interact semantically?
- What does a `settle` invocation mean: submit now, request integration, wait, or verify completed integration?
- Can contributors alter an agent's operating scope or permissions from a PR description or issue comment? (No trust should be granted from untrusted text.)
- How are failed merges or reviewer-denied PRs preserved and communicated?
- How can a human override advisory AI audit findings without suppressing required repository checks?
- How are semantic-audit results invalidated when the target base changes, even if PR heads do not?
- What proof is required before marking a release published?
- How does an owner stop, pause or cancel a task without discarding user work?

## Decision process

1. Select one open D-entry.
2. Present options and trade-offs without assuming a default.
3. Record the chosen policy and reason only after explicit owner discussion.
4. Map the effect to backlog items, use cases and acceptance tests.
5. Proceed to the next decision; architecture stays uncommitted until enough decisions are resolved.
