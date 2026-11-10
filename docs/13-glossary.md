# Glossary

**Factory:** Gitxa's proposed policy-based coordination of task planning, work execution and GitHub integration.

**Thread:** A user-level orchestration context containing multiple related tasks; **not** necessarily a Git branch, chat ID or local process.

**Task:** A separately trackable unit of requested work, with expected outcome and verification.

**Dependency:** A rule saying a task needs another task's specification, implementation or merged state before some action is allowed.

**Ready:** Eligible for a specified action under current dependencies, policy and state; readiness is action-specific.

**Workspace:** The environment used to implement one task; its exact technology is undecided.

**Issue:** A GitHub work-tracking artifact; whether it is the sole task identifier is unresolved.

**Pull request (PR):** A proposed GitHub integration of branch changes. Open PR is not equivalent to merged code.

**Submission:** An action that commits/pushes/opens or updates PRs. It is not a guarantee of CI success or merge.

**Settlement:** A batch request to process eligible tasks through submission/integration policy; not necessarily a single atomic merge or completed release.

**Integration:** Changes being accepted into the target branch under GitHub's actual repository rules.

**CI:** Automated verification attached to changes or integration candidates. Passing checks can be revision-specific.

**Textual conflict:** A version-control conflict when changes cannot automatically be combined at the text/tree level.

**Semantic/logical conflict:** Incompatible behavior, contract or assumption between changes even if Git can textually combine them.

**Git Dynamic Conflict:** Proposed, deliberately **manual** AI semantic audit of two or more PRs; read-only and nonauthoritative.

**Stale evidence:** A verification/audit record no longer applicable to the current revisions or integration assumptions.

**Idempotency:** Repeating an operation safely has no unintended duplicate side effects.

**Recovery:** Reconciling local/remote truth after a crash, failure, or partially completed operation.

**Approval:** Authorized human or platform review required by policy; is different from AI recommendation.

**Merge request:** Request to merge or enroll a PR in a permitted merge workflow; is different from confirmation of completed merge.

**Release:** Explicit publication/rollout of integrated changes, governed separately from merges.
