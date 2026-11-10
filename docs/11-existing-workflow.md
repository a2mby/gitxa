# Pre-Gitxa Apixa workflow (context only)

Gitxa is intended to preserve valuable aspects of the original two-skill workflow while removing unnecessary sequential work. This is **historical context**, not an architecture or requirement to copy every command verbatim.

## `/plan-change` — what it did

- Developer supplies a short brief; empty brief leads to a clarification request.
- Reads `docs/context.md`, the active version folder and its version README; avoids recapping entire project.
- Detects an already-active task branch for the same work and refuses to stack unrelated work on it.
- Opens a GitHub issue with the unchanged brief, active version, problem, outcome, expected paths and **required tests** for behavior changes.
- Includes documentation and active milestone files when justified by the change, with explicit out-of-scope warnings.
- For behavior/type/API/error-path changes, plans happy path, overrides, edge cases, failure and regression coverage using fake/injectable transport instead of flaky network dependencies.
- Originally switched to latest `main` and created a `task/N-slug` branch; this tied the developer to one active checkout.
- Replies with issue, branch, version, expected files, tests, and then stops unless implementation was explicitly requested.

## `/git-push` — what it did

- Required current branch `task/N-slug`; read the issue and enforced its intended file scope.
- Updated from latest `main` before pushing and before merging; stopped at rebase conflicts.
- Updated context and top-of-file story log, including version acceptance when relevant.
- Ran format before staging; staged listed files and permitted format-only collateral changes.
- Created a conventional-style commit with explanation, pushed to a task branch.
- Opened or reused a PR with `Closes #N`, summary and test plan.
- Attempted a squash merge and branch deletion; required `main` synchronized and task branch removed before completion.
- Returned PR URL, squash commit and story entry.

## Existing strengths to retain

- Issue-per-change traceability, reproducible test plans, explicit active version scope.
- Clean and intentional staging, no credentials/unrelated changes.
- Clear commit/PR history, link from PR to issue, documentation of what landed.
- Strict repository verification rather than removing CI.

## Problems motivating Gitxa

- PR completion was conflated with local submission completion.
- Branch/checkout management hindered multiple simultaneous task implementations.
- Rebase-before-every-step caused unnecessary stalls for unrelated work.
- Every task touching shared story/context files increased conflict likelihood.
- No durable first-class model for threads/dependencies/parallel settlement.
- No explicit multi-user idempotency or recovery semantics.

## Requirements derived from this history

- Keep the issue/branch/PR/test lineage, but disentangle task submission from actual merge.
- Preserve safety/quality checks, but avoid CI as a global development lock.
- Support concurrent independent tasks and controlled dependent chains.
- Make submit/settle resumable and repeatable without duplicates.
- Let architecture and merge authority be deliberately decided rather than assumed from a previous script.
