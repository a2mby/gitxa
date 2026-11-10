# Complete use-case catalog (UC01–UC61)

**Status:** requirements, not implemented capabilities. The factory must accommodate human users, optional coding agents, multiple threads and repositories; individual behaviors depend on future policy decisions.

## A. Planning and task creation

| ID | Use case | Expected behavior |
|---|---|---|
| UC01 | One developer requests one change | Create an issue and associated task workspace according to policy. |
| UC02 | Request ten unrelated changes | Create ten independently trackable tasks. |
| UC03 | Request a sequence of dependent changes | Express and validate task dependencies. |
| UC04 | Request several changes in one thread | Track a coherent thread of distinct tasks. |
| UC05 | Open a second thread during active development | Begin ready work without waiting for unrelated tasks. |
| UC06 | Submit an identical planning request twice | Detect likely duplicates and avoid silent duplication. |
| UC07 | Change requirements during development | Record and validate updates to scope and acceptance criteria. |
| UC08 | Plan work whose prerequisites are not ready | Create tasks but defer dependent execution. |

## B. Parallel development

| ID | Use case | Expected behavior |
|---|---|---|
| UC09 | Five agents implement independent tasks | Keep their branch/workspace changes isolated. |
| UC10 | Task B depends on unmerged Task A | Apply chosen wait-versus-stack dependency policy. |
| UC11 | Two tasks modify the same source file | Avoid overwrites and warn about potential integration risk. |
| UC12 | An agent crashes during implementation | Preserve existing work and allow safe resume. |
| UC13 | Developer resumes a task in another session | Recover correct task identity, context, and workspace state. |
| UC14 | More ready tasks exist than capacity permits | Enforce configured concurrency and queue excess ready work. |
| UC15 | Developer manually changes a task branch | Reconcile observed branch/commit state before any write. |
| UC16 | An agent must change an unplanned file | Apply justified-scope-expansion policy. |
| UC17 | Developer changes to another repository | Keep repository state and policies independent. |
| UC18 | Two developers attempt to claim the same task | Enforce ownership/coordination policy. |

## C. Commits and pull requests

| ID | Use case | Expected behavior |
|---|---|---|
| UC19 | Agent finishes implementation | Validate, commit and submit according to policy. |
| UC20 | Mandatory local tests fail | Block submission and expose actionable diagnostics. |
| UC21 | A PR already exists for a task | Update/reuse it rather than opening a duplicate. |
| UC22 | Submit a new PR while another PR's CI is running | Both progress independently. |
| UC23 | Developer requests squash merging | Respect repository and actor policies for squash merge. |
| UC24 | Repository requires manual approval | Never merge without the required authorization. |
| UC25 | Developer requests a merge from their device | Apply merge-request authority and GitHub protections. |
| UC26 | Task PR is behind `main` | Follow configured base freshness/integration rules. |
| UC27 | PR requires reviewers | Hold merge until required reviews satisfy policy. |

## D. Batch settlement and CI

| ID | Use case | Expected behavior |
|---|---|---|
| UC28 | Settle Thread A | Submit all eligible tasks from A without misreporting pending merges. |
| UC29 | Settle Threads A and B | Coordinate eligible work across both threads. |
| UC30 | Task 2 depends on Task 1 | Preserve required implementation and integration ordering. |
| UC31 | Task 5 fails while 6–9 pass | Continue processing 6–9 if truly independent. |
| UC32 | CI fails because of formatting | Permit bounded, safe automated correction if authorized. |
| UC33 | CI fails because of an architecture rule | Escalate; do not bypass architecture enforcement. |
| UC34 | Two PRs pass independently but fail together | Detect integration failure; withhold unsafe merge. |
| UC35 | Settlement is repeated after partial success | Resume idempotently with no duplicate PRs or commits. |
| UC36 | CI completes after the IDE closes | Remote process continues according to configured rules; local state later reconciles. |
| UC37 | A successful CI check is tied to an old revision | Do not reuse it to authorize unverified changes. |

## E. Conflicts and recoverability

| ID | Use case | Expected behavior |
|---|---|---|
| UC38 | Merge conflict is trivial/unambiguous | Resolve only if policy permits; reverify afterward. |
| UC39 | Conflict alters semantics or is ambiguous | Ask for authorized human judgment. |
| UC40 | GitHub API times out | Verify whether the remote operation succeeded before retrying. |
| UC41 | Commit succeeds, PR creation fails | Resume from the existing commit/branch. |
| UC42 | Factory crashes midway through settlement | Reconcile durable records with GitHub to resume safely. |
| UC43 | A separate unrelated bug is discovered | Create a linked issue when justified; don't proliferate issues for routine failures. |
| UC44 | Upstream dependency changes | Reconsider downstream state and invalidate affected checks/audits. |
| UC45 | Automatic repair fails repeatedly | Stop at budget, preserve changes and surface blocker. |

## F. Releases and long-term use

| ID | Use case | Expected behavior |
|---|---|---|
| UC46 | All milestone tasks are merged | Mark milestone integration complete, not automatically released. |
| UC47 | Some tasks merge while others remain pending | Report exact readiness and blockers. |
| UC48 | Developer requests an npm release | Apply repository's approved release process. |
| UC49 | Release verification fails | Block publication. |
| UC50 | Publication succeeds | Verify the registry/artifact state and record publication evidence. |
| UC51 | Merged task still has dirty local files | Preserve those files; do not blindly delete workspace. |
| UC52 | Developer resumes after a week | Reconcile with remote changes and recover work accurately. |
| UC53 | Factory configuration changes | Validate and migrate any affected persisted state. |

## G. Git Dynamic Conflict (manually requested semantic audit)

| ID | Use case | Expected behavior |
|---|---|---|
| UC54 | Reviewer manually audits two PRs | Analyze possible logical incompatibilities beyond textual conflicts. |
| UC55 | Reviewer manually audits several PRs before settlement | Consider pairwise and higher-order interactions; do **not** auto-run audits merely because settlement starts. |
| UC56 | Separate files implement contradictory business rules | Report the behavioral contradiction with evidence. |
| UC57 | PRs contain incompatible schema/API/consumer assumptions | Explain the contract mismatch and affected integration path. |
| UC58 | PRs introduce conflicting side effects or integration assumptions | Flag the concrete risk, with confidence and uncertainty. |
| UC59 | Reviewer requests evidence and suggestions | Report specific files, changed code, reasonable tests and mitigations. |
| UC60 | A PR changes after an audit | Mark earlier findings stale and allow a new manual audit. |
| UC61 | No plausible conflict is found | Report `none identified` with coverage/uncertainty, **not** a guarantee of safety. |

---

**Use-case integrity:** exactly UC01–UC61, no gaps or duplicates. Feature behavior remains subject to the [unresolved design decisions](05-decisions-register.md).
