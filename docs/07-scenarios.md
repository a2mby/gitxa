# Scenario library and operational examples

These examples define intended behavior, not an approved branch topology, agent runtime, directory layout, database, or merge policy.

## S01 — Two conversations, nine tasks

**Thread A:** `plan-change 1 2 3 4 5 6`.

- Task 1: write a version contract.
- Task 2: implement it after Task 1's accepted contract.
- Task 3: improve the implementation after Task 2.
- Task 4: extend functionality after Task 3.
- Task 5: fix an unrelated bug independently.
- Task 6: write unrelated docs independently.

**Thread B:** `plan-change 7 8 9`: three independent bugfix/refactor tasks, capable of starting while Thread A is still active.

Expected: organize nine issues/tasks, preserve intent and dependencies, prepare isolated work contexts, progress eligible work, and never block 5–9 solely because 2–4 are awaiting earlier dependencies. Actual scheduling/execution technology remains undecided.

## S02 — CI is strict but not a developer-wide lock

- PR A is submitted and CI is still pending.
- Developer/agent starts and submits unrelated PR B.
- PR A passes and merges only if required policy is satisfied.
- PR B might be pending, pass, fail or require base/integration revalidation; it is evaluated against its own current rules.
- New work may continue independently. No CI check is removed simply to make the workflow faster.

## S03 — Multiple branches in one IDE

- Three task implementations are active in one project.
- The factory must ensure changing files in Task A cannot silently stage or overwrite Task B's changes.
- The user can navigate and resume any task without needing a completed merge for the others.
- **Mechanism undecided:** worktrees, clones, remote workspaces or another arrangement may satisfy the requirements.

## S04 — Settle many tasks

- Developer requests settlement of Thread A while unrelated Thread B is active.
- Factory identifies ready tasks and verifies missing requirements without touching incomplete tasks.
- Valid changes are committed/submitted according to policy; existing PRs are reused.
- Pending CI is recorded as pending, not merged. Later remote results are reconciled.
- Failure of one PR does not halt settlement of truly independent PRs.
- Completion means **settlement request handled**, not necessarily that every PR has already merged.

## S05 — Dependent chain and concurrent merge

- Task B depends on A's new API. C depends on B; D is unrelated.
- A receives a late update; B and C may need their assumptions and verification rechecked.
- D should not be blocked by changes to A.
- B's PR must not merge earlier than its necessary prerequisites when that would break the intended contract.
- Policy for waiting, stacking, integration refs, and revalidation is **D04–D16**, not chosen here.

## S06 — Ordinary code/test failure

- A task's local typecheck or CI fails.
- A bounded safe fix may be attempted if an authorized policy permits it.
- Reverification is required after modifications; retry limits apply.
- Serious ambiguity or altered architecture requires human input.
- Routine failure is tracked on the current task/PR; it is **not** an excuse to create a new issue per failed test.

## S07 — Crash or timeout during PR creation

- Remote GitHub API accepts a PR but client times out before saving its ID.
- On retry, the factory must reconcile issue/branch/PR identity.
- It must not blindly create a second PR.
- Incomplete local operations do not cause uncommitted work to be deleted.

## S08 — Two developers, one repository

- Developer A and B operate from separate machines while each has active tasks.
- They may compete to claim the same task or submit concurrently.
- The factory must not overwrite one person's commits, reuse another's authorization, or assume machine-local state is shared.
- Remote and local state reconciliation, ownership and locks are unresolved design decisions, but correctness is mandatory.

## S09 — Two PRs with no Git conflict, incompatible semantics

- PR 101 changes API authentication to JWT headers.
- PR 102 implements a consumer expecting session cookies.
- Both have green independent tests and clean textual mergeability.
- A reviewer **manually** asks for `audit-conflicts 101 102` (syntax not final).
- AI produces an evidence-backed **possible semantic conflict**, not an automatic change or a veto independent of policy.
- The reviewer chooses tests/changes/merge order; repo protections remain in effect.

## S10 — Audit several PRs and stale reports

- Three PRs jointly modify a data contract; no individual pair clearly contradicts the others.
- The reviewer explicitly requests a three-PR audit.
- Report must consider higher-order interaction or clearly state that it could not.
- PR 2 receives an update after the audit; the previous result is stale and cannot be misrepresented as a current review.

## S11 — Release after integration

- A milestone contains merged and pending PRs.
- The factory reports the distinction; it does not publish simply because a batch was submitted.
- An authorized releaser requests a release, and project-specific release verification is applied.
- Success is only reported after confirmation of the published artifact/destination.

## S12 — Clean branch, dirty workspace

- A PR merges but an associated working environment contains unrelated uncommitted changes.
- Branch/workspace cleanup must preserve those changes; an automatic deletion without checking is prohibited.

## S13 — Explicit policy mismatch

- An agent requests squash merging while the repository requires human review and disallows its requested method.
- Gitxa rejects or routes the action under the actual repository policy, explains the reason, and does not attempt a hidden bypass.

## S14 — Prompt-injection attempt

- A PR description or CI log contains text claiming authority to skip tests, delete branches or approve changes.
- Gitxa must treat that text as untrusted evidence, never as operator instructions.
- Only a verified authorized actor and effective configured policy may trigger sensitive actions.
