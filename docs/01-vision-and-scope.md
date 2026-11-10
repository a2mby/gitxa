# Vision, goals, non-goals, and users

## Mission

Build a reusable **GitHub Development Factory** that lets a developer describe multiple changes, plan their dependencies, progress eligible work concurrently, and integrate only policy-compliant changes, with complete traceability and recoverable failure handling.

> **Parallel development. Controlled integration. Deliberate releases.**

## Goals

1. Separate task implementation from PR submission, CI completion, merge and release completion.
2. Coordinate one task, batches of independent tasks, and dependent chains within and across multiple threads.
3. Keep traceability from user request to task, issue, branch, workspace, commits, tests, PR, CI outcome, merge, and release.
4. Make independent work progress while unrelated CI or reviews are pending.
5. Enforce configurable, strict policies with deterministic checks; do not rely exclusively on agent prompts.
6. Support one human, many humans, many AI agents, or a hybrid; multiple repositories and machines must be considered.
7. Recover safely from conflicts, interruptions, retries, external changes, and partial failures.
8. Enable manually requested **Git Dynamic Conflict** audits for semantic cross-PR inconsistencies.
9. Preserve existing GitHub governance, permissions, CI, review and branch protections.
10. Stay useful as a personal tool; avoid unrelated platform/product complexity.

## Users and roles (not permission commitments)

- **Solo developer:** operates multiple concurrent changes, possibly with independent AI coding sessions.
- **Team developer:** contributes in a shared repository from a separate machine.
- **Task executor:** human or agent implementing an assigned change.
- **Reviewer/merger:** examines PRs, verifies policy satisfaction, may manually invoke semantic audit, and requests or authorizes integration as permitted.
- **Maintainer/releaser:** decides when and what to publish after verification.

## In scope

Task intake, issue traceability, grouping into threads, dependency tracking, isolated development, scoped change verification, commits, PRs, CI visibility, integration policy enforcement, batch settlement, failure/recovery, multi-user coordination, persistent state, status/audit trail, optional release workflow, skill interfaces, and on-demand semantic PR audits.

## Out of scope (for the factory's responsibility)

Implementing a new Git engine; replacing GitHub Issues/PRs or GitHub Actions; building a coding language model; implementing a general IDE or CI server; guaranteeing bug-free semantic conflict detection; requiring a dashboard/hosted service; granting the factory authority to bypass a repository's real protections; or automatically accepting risky architectural decisions.

## Design status

This document defines **what Gitxa should achieve**. It does **not** decide how the code is organized, which tools are used, where persistent state lives, which execution/agent platform runs tasks, how user identity is managed, or which integration and merge policies are adopted. All such questions belong in [the open decision register](05-decisions-register.md).
