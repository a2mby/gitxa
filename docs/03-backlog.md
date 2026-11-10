# Complete product backlog

**Scope:** canonical discovery backlog. **23 epics.** Each bullet is a candidate implementation item, not a commitment to specific tools or architecture. Priorities express the preliminary sequencing discussed; revisit during planning. Do not remove or silently reorder items.

Priority legend: **P0** foundation/safety; **P1** core multi-thread vision; **P2** advanced collaboration/hardening; **P3** optional where justified. Epics span several priorities where noted.

## Epic 01 — Factory foundation (P0)

- [ ] Create an independent GitHub repository.
- [ ] Establish an executable entry point and internal core (language and packaging undecided).
- [ ] Define Git operation boundaries/adapters.
- [ ] Define GitHub operation boundaries/adapters for issues, PRs, checks and merges.
- [ ] Define versioned configuration and state schemas.
- [ ] Define structured errors and exit codes.
- [ ] Execute commands safely, without unsafe shell interpolation.
- [ ] Build a test harness for Git/GitHub operations.
- [ ] Establish boundaries between skills, policy enforcement and execution.

Outcome: reusable, testable foundation not dependent on an AI prompt for correctness.

## Epic 02 — Configuration and rules engine (P0)

- [ ] Support global default policies.
- [ ] Support repository-specific policies.
- [ ] Validate every configuration property.
- [ ] Support policy inheritance and overrides.
- [ ] Define precedence among CLI/request arguments, repository policies and global policies.
- [ ] Define safety rules that cannot be overridden without appropriate authority.
- [ ] Support configurable strictness where safe.
- [ ] Validate repository compatibility before operations.
- [ ] Explain effective configuration and rejected actions.
- [ ] Support configuration migration between factory versions.

Policy candidates: merge strategy, approval authority, branch constraints, required CI, concurrency limits, retry budgets, scope rules, release authority. **No default values or formats selected.**

## Epic 03 — Task planning and GitHub issues (P0)

- [ ] Accept one task or multiple tasks in a request.
- [ ] Convert a brief into a structured task specification.
- [ ] Create one GitHub issue per task by default; policy TBD.
- [ ] Associate issues with a development thread.
- [ ] Define expected files, outcomes and acceptance criteria.
- [ ] Require tests to be planned for functional changes.
- [ ] Detect existing issues and avoid unintended duplicates.
- [ ] Support updating task scope and acceptance criteria.
- [ ] Support priority, labels and assignment.
- [ ] Support cancellation and reopening.
- [ ] Track newly discovered work separately from the original request.

## Epic 04 — Thread orchestration (P1)

- [ ] Represent a thread as a group of related tasks.
- [ ] Allow multiple simultaneous threads per repository.
- [ ] Associate threads with users and coding sessions where available.
- [ ] Track per-thread progress independently.
- [ ] Pause, resume and cancel threads.
- [ ] Add tasks to an active thread.
- [ ] Support thread-level settlement.
- [ ] Report thread completion and blockers.
- [ ] Preserve thread state across restarts.

## Epic 05 — Dependency management (P1)

- [ ] Define explicit task dependencies and prerequisites.
- [ ] Represent dependencies as an acyclic graph.
- [ ] Detect and reject dependency cycles.
- [ ] Determine which tasks are ready for implementation.
- [ ] Distinguish implementation dependencies from integration dependencies.
- [ ] Support tasks requiring code already merged into the base branch.
- [ ] Explore stacked branches/PRs for unmerged prerequisites (policy TBD).
- [ ] Handle updates to upstream tasks.
- [ ] Propagate blockers only to affected tasks.
- [ ] Recompute task readiness after state changes.
- [ ] Warn about plausible hidden dependencies in files or public interfaces.

## Epic 06 — Branch and workspace management (P0)

- [ ] Create branches from configured base references.
- [ ] Provide an isolated working environment for each active task.
- [ ] Evaluate multiple local workspaces/worktrees as a candidate; selection remains open.
- [ ] Allow separate-machine work through independent clones or equivalent models.
- [ ] Prevent agents from modifying other tasks' workspaces accidentally.
- [ ] Detect dirty working directories before switching or cleanup.
- [ ] Never overwrite unrelated uncommitted changes.
- [ ] Map branches and workspaces to issues/tasks.
- [ ] Detect stale, renamed, missing or deleted branches.
- [ ] Recover workspaces from available remote state when possible.
- [ ] Synchronize/rebase branches safely when policy requires.
- [ ] Clean up completed workspaces only after verified eligibility.

## Epic 07 — Execution and agent contracts (P1)

- [ ] Define execution inputs and outputs independent of any AI model.
- [ ] Supply task brief, constraints, workspace identity and acceptance criteria.
- [ ] Record task execution ownership and attempts.
- [ ] Enforce repository and workspace boundaries.
- [ ] Support multiple simultaneous human or AI executors.
- [ ] Pause, resume and hand off execution.
- [ ] Replace an executor without losing task history.
- [ ] Limit concurrency by configurable policy.
- [ ] Set bounds on automatic retries.
- [ ] Separate implementation authority from merge authority.
- [ ] Allow workflows to operate without AI coding agents.

## Epic 08 — Change scope and file control (P0)

- [ ] Track planned files per task.
- [ ] Compare actual modifications to planned scope.
- [ ] Differentiate expected from unexpected changes.
- [ ] Support justified scope expansion.
- [ ] Require approval for sensitive expansion.
- [ ] Detect unrelated dirty files.
- [ ] Avoid cross-task staging/commits.
- [ ] Identify modifications to protected files.
- [ ] Handle intentionally shared documentation and configuration updates.
- [ ] Prevent accidental credential, secret and environment-file commits.

## Epic 09 — Local verification (P0)

- [ ] Define configurable verification commands without selecting a runner now.
- [ ] Run change-targeted tests when appropriate.
- [ ] Run full-project verification when required.
- [ ] Enforce configured formatting and lint checks.
- [ ] Enforce configured build and type checks.
- [ ] Verify required test-plan coverage for functional changes.
- [ ] Check generated artifacts where relevant.
- [ ] Associate test results with the exact tested revision.
- [ ] Block submission when mandatory local gates fail.
- [ ] Support verification profiles by task type.
- [ ] Avoid redundant checks when inputs are provably unchanged.

## Epic 10 — Commit management (P0)

- [ ] Stage only authorized task changes.
- [ ] Support configurable commit message conventions.
- [ ] Generate meaningful commit descriptions.
- [ ] Validate staged contents before commit.
- [ ] Allow multiple commits per task.
- [ ] Support optional pre-submission squashing under policy.
- [ ] Prevent empty and duplicate commits.
- [ ] Detect commits created outside the factory.
- [ ] Associate commit hashes with task records.
- [ ] Preserve author intent and attribution.
- [ ] Prevent unrelated history changes.

## Epic 11 — Pull request management (P0)

- [ ] Open PRs for task branches.
- [ ] Detect and reuse existing PRs.
- [ ] Support draft PRs.
- [ ] Link PRs to corresponding issues.
- [ ] Prepare summaries and testing evidence.
- [ ] Support reviewer requests and labels where authorized.
- [ ] Detect base branch changes.
- [ ] Track review status and approvals.
- [ ] Track mergeability and textual conflicts.
- [ ] Support per-task PRs.
- [ ] Evaluate grouped PRs where explicitly configured.
- [ ] Evaluate stacked PRs for dependencies where needed.

## Epic 12 — CI integration (P1)

- [ ] Identify required repository checks and workflows.
- [ ] Track runs associated with each PR.
- [ ] Distinguish pending, successful, failed, skipped and canceled statuses.
- [ ] Bind results to the correct revision/integration candidate.
- [ ] Detect stale results.
- [ ] Support multiple workflows and test matrices.
- [ ] Retrieve failure logs and diagnostics.
- [ ] Observe CI without blocking independent work.
- [ ] Cancel obsolete runs only where allowed and safe.
- [ ] Never allow merge when mandatory checks fail.
- [ ] Support optional verification of combined integration state.
- [ ] Avoid wasteful duplicate verification where safe.

## Epic 13 — Merge and integration management (P1)

- [ ] Support squash merges under configuration.
- [ ] Support regular merge commits under configuration.
- [ ] Support rebase merges under configuration.
- [ ] Enforce whichever strategy the repository and owners select.
- [ ] Support human-controlled merge authorization.
- [ ] Support requests for authorized automatic merging.
- [ ] Respect GitHub branch protections and rulesets.
- [ ] Respect required approvals and reviewers.
- [ ] Handle repositories that require up-to-date branches.
- [ ] Consider merge queues only where supported/appropriate.
- [ ] Enforce dependency constraints during integration.
- [ ] Detect outdated assumptions after concurrent merges.
- [ ] Revalidate combined changes when policy requires.
- [ ] Confirm the remote PR truly merged before changing local state to `merged`.
- [ ] Record resulting integration revision(s).

## Epic 14 — Batch settlement (P1)

- [ ] Settle one selected task.
- [ ] Settle all eligible tasks in a thread.
- [ ] Settle eligible tasks across selected threads.
- [ ] Identify tasks actually ready for submission.
- [ ] Skip incomplete or blocked tasks safely.
- [ ] Respect dependency order.
- [ ] Submit independent PRs concurrently where permitted.
- [ ] Support intentional grouped integration if configured.
- [ ] Request automatic merging only where allowed.
- [ ] Continue unaffected tasks after a particular task fails.
- [ ] Produce exact outcome reports.
- [ ] Make repeat settlement idempotent.
- [ ] Distinguish submitted, queued, CI-pending, merged, and failed states.

## Epic 15 — Failure detection and automatic recovery (P1)

- [ ] Classify failures by cause and severity.
- [ ] Retry transient transport failures safely.
- [ ] Handle GitHub rate limits without unsafe retries.
- [ ] Allow safe formatting corrections under policy.
- [ ] Permit bounded repair attempts for test/type failures, if explicitly authorized.
- [ ] Detect actual textual merge conflicts.
- [ ] Automate only unambiguous conflict resolutions under policy.
- [ ] Escalate ambiguous or behavior-altering conflicts to an authorized person.
- [ ] Treat architectural rule violations as policy failures, not something to bypass.
- [ ] Preserve work after failure.
- [ ] Record attempts and outcomes.
- [ ] Prevent unbounded repair loops.
- [ ] Create new issues only for genuinely separate discovered work.
- [ ] Keep unrelated tasks unblocked.

## Epic 16 — Multi-user coordination (P2)

- [ ] Support developers operating from different machines.
- [ ] Support task claims and ownership.
- [ ] Detect competing claims.
- [ ] Define enforceable coordination for exclusive actions.
- [ ] Record handoffs and ownership changes.
- [ ] Respect repository permissions and roles.
- [ ] Support humans and AI agents together.
- [ ] Prevent unauthorized changes to other owners' branches.
- [ ] Prevent duplicate settlement/merge attempts.
- [ ] Handle temporary disconnections.
- [ ] Resume stale or abandoned claims safely.
- [ ] Maintain contributor-aware history.

## Epic 17 — Factory state and persistence (P0)

- [ ] Define task, thread, workspace and settlement states.
- [ ] Persist state across sessions.
- [ ] Distinguish local facts from remote authoritative GitHub facts.
- [ ] Reconcile state after interruptions and external changes.
- [ ] Make repeat operations idempotent.
- [ ] Recover after crashes.
- [ ] Detect partially completed commands and side effects.
- [ ] Record attempts and outcomes.
- [ ] Migrate durable state safely.
- [ ] Protect newer remote state against stale local writes.
- [ ] Reconstruct state from Git/GitHub where feasible.

## Epic 18 — Status, logs and observability (P1)

- [ ] Show active threads and tasks.
- [ ] Show dependencies, readiness, and blockers.
- [ ] Show executing humans/agents where known.
- [ ] Show branch and workspace mappings.
- [ ] Show PR and CI states.
- [ ] Highlight decisions requiring human attention.
- [ ] Report settlement outcomes accurately.
- [ ] Record important operations and rationale.
- [ ] Support machine-readable views.
- [ ] Support concise human-readable reports.
- [ ] Explain policy denials.
- [ ] Measure waiting time, throughput and bottlenecks.

## Epic 19 — Release and publishing (P2)

- [ ] Distinguish integration complete from released.
- [ ] Verify required changes truly merged.
- [ ] Track included/unreleased changes.
- [ ] Support version selection/validation according to project rules.
- [ ] Prepare release notes and changelogs.
- [ ] Run required complete release verification.
- [ ] Verify build/package artifacts.
- [ ] Support project-specific publishing methods.
- [ ] Enforce release approval policy.
- [ ] Prevent duplicate or wrong-version publication.
- [ ] Verify published destination and artifact identity.
- [ ] Recover or escalate partial releases safely.
- [ ] Record who authorized and performed each release.

## Epic 20 — Security and authorization (P0/P2)

- [ ] Apply least-privilege repository credentials.
- [ ] Validate targets of Git/GitHub actions.
- [ ] Protect sensitive branches.
- [ ] Prevent unauthorized force pushes.
- [ ] Prevent direct pushes to protected branches when disallowed.
- [ ] Protect secrets from logs and agent context.
- [ ] Require explicit authorization for destructive actions.
- [ ] Check actors' merge and publish authority.
- [ ] Treat issues, diffs, PRs, comments and CI logs as untrusted input.
- [ ] Audit sensitive actions.
- [ ] Define credential policy for multi-user operation.

## Epic 21 — Testing the factory (P0/P1)

- [ ] Unit-test policy evaluation.
- [ ] Unit-test dependency ordering and cycle detection.
- [ ] Test valid/invalid lifecycle state transitions.
- [ ] Test idempotency and retries.
- [ ] Test Git operations in disposable repositories.
- [ ] Test GitHub interactions with controlled fakes/fixtures.
- [ ] Test concurrent workspaces and branches.
- [ ] Test simultaneous task submissions.
- [ ] Test conflicts and failed rebases.
- [ ] Test interruption and crash recovery.
- [ ] Test full PR lifecycle.
- [ ] Simulate CI success/failure, staleness and cancellation.
- [ ] Test multi-user races.
- [ ] Test permissions, malicious inputs and security boundaries.
- [ ] Validate end-to-end acceptance scenarios.

## Epic 22 — Distribution and integrations (P1/P3)

- [ ] Make Gitxa installable/reusable without copying large instruction files.
- [ ] Provide skill adapters for selected developer environments.
- [ ] Provide repository initialization flow.
- [ ] Support per-user and per-project setup where justified.
- [ ] Publish example configuration once its format is chosen.
- [ ] Version documented policies and schemas.
- [ ] Support safe upgrades.
- [ ] Test compatibility across supported environments.
- [ ] Consider webhooks/central coordinator only when needed.
- [ ] Consider UI only if command/status access proves insufficient.

## Epic 23 — Git Dynamic Conflict: on-demand semantic PR audit (P2, prioritization open)

- [ ] Support a **manually triggered** semantic conflict audit initiated by a person intending to merge.
- [ ] Compare **two or more** PRs without modifying them.
- [ ] Retrieve changed code, surrounding relevant context and documented contracts.
- [ ] Detect potentially incompatible API assumptions and interfaces.
- [ ] Detect contradictory business rules.
- [ ] Detect schema/migration versus consumer incompatibilities.
- [ ] Detect authentication/authorization assumption mismatches.
- [ ] Detect configuration/environment incompatibilities.
- [ ] Detect indirect dependencies, shared side effects and concurrency interactions.
- [ ] Detect cross-PR effects even when changed files do **not** overlap.
- [ ] Analyze likely combined state/integration order, not only isolated diffs.
- [ ] Support 3+ PR interactions beyond pairwise comparisons.
- [ ] Explain findings with evidence, severity and confidence/uncertainty.
- [ ] Suggest mitigation and targeted integration tests.
- [ ] Record exact audited head/base SHA(s) and assumptions.
- [ ] Treat results as stale after relevant PR revisions/base changes.
- [ ] Produce readable reports for human merging decisions.
- [ ] Remain **read-only**; never auto-change code, approve, merge or open issues during the audit.
- [ ] Remain **on-demand**, not another automatically triggered CI job.
- [ ] Test known positive conflicts, safe combinations, incomplete context and false positives.

See [Git Dynamic Conflict](09-git-dynamic-conflict.md). **Decision D29** is open regarding audit inputs, coverage, evidence and advisory-versus-required-report policy. Even a clean report is not proof of compatibility.

---

**Backlog integrity:** 23 epics are recorded. M1–M5 and UC01–UC61 are recorded separately. Detailed implementation architecture remains unselected.
