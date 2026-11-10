# Candidate skill and command interfaces

**Status: exploratory, not a committed CLI/skill contract.** The user wants Gitxa to remain **skill-first**. Deterministic enforcement must be possible independently of an AI prompt; the specific command runner, language, packaging and skill platform are not chosen.

| Proposed invocation | Intent |
|---|---|
| `/factory-init` | Initialize or inspect repository integration/policies. |
| `/plan-change` | Plan a single change or multi-task thread, preserving user brief. |
| `/start-task` | Claim/start a planned task in an authorized isolated environment. |
| `/task-status` | Show a task's exact readiness, owner, PR, CI and blockers. |
| `/factory-status` | Show all threads/tasks, dependencies and pending decisions. |
| `/verify-task` | Run configured local checks against the correct revision. |
| `/git-push` | Scope/validate/commit/push and create/update the PR; does not implicitly wait for all CI. |
| `/settle-thread` | Process all eligible tasks in a selected thread. |
| `/settle-all` | Process eligible tasks across explicitly selected threads. |
| `/fix-failure` | Diagnose a failed operation; attempt only authorized bounded repairs. |
| `/sync-task` | Safely reconcile a task with its base/dependency changes. |
| `/resume-task` | Recover an interrupted task from known current state. |
| `/factory-cleanup` | Remove only confirmed safe-to-delete task workspaces/branches. |
| `/publish-library` | Execute verified, authorized project-specific release. |
| `/audit-conflicts` | **Human-requested**, read-only AI review of two or more PRs for logical conflicts. |

## Skill requirements

- One request may describe 1, 6, 9 or more tasks and their dependencies.
- Skills must be compact; don't make every invocation re-explain the whole repository.
- Real status must come from the state and GitHub, not narrative assumptions.
- Safe repetitive operations should be executable without high-cost AI reasoning.
- Sensitive decisions should be explicit, actionable and bounded.
- No skill may silently replace a repository's branch/CI/review permissions.
- AI coding agent choice, scheduling tool, IDE and execution runtime remain open.
- These commands may ultimately be aliases, consolidated commands, or different interfaces, depending on design decisions.

## Interaction example (illustrative)

```text
Thread 1: /plan-change 1, 2, 3, 4, 5, 6
Thread 2: /plan-change 7, 8, 9
/settle-thread 1
/factory-status
/audit-conflicts 101 102
```

The first three commands should not force Thread 2 to wait for Thread 1's unrelated CI. The last is **never triggered implicitly by settlement**.
