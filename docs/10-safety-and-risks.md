# Safety, correctness and operational risks

These are engineering requirements and failure modes, **not** a proposed architecture.

## Critical risks

| Risk | Required property |
|---|---|
| Unrelated tasks block each other | Dependency-aware readiness; independent progress. |
| Concurrent writes race or overwrite history | Validation/coordination before shared mutations. |
| Dirty workspace destroyed during cleanup | Verify and preserve useful uncommitted state. |
| Duplicate PR/issue/commit after retry | Idempotent identity and remote reconciliation. |
| Merging despite missing CI or reviews | Enforce remote GitHub policies and required checks. |
| Green CI from old revision reused | Tie evidence to exact tested SHA/integration candidate. |
| Individual PRs pass but combination breaks | Integration checks and optional human-requested semantic review. |
| Repair agent changes behavior to satisfy a test | Limit repair authority, reverify changes, escalate ambiguity. |
| False-negative AI audit | Disclose coverage/uncertainty and never claim safety guarantees. |
| False-positive AI audit | Require evidence and maintain human judgment. |
| PR/issue/CI contents attempt prompt injection | Treat external text as untrusted data. |
| Credential leakage or broad repository scope | Least privilege and log/secret hygiene. |
| Developer offline or process crash | Persist/reconcile partial outcomes and resume without duplication. |
| Multi-user conflicting ownership | Explicit role/claim/authorization policy. |
| Mistaken release or repeated publishing | Require approval, version/artifact validation and publication proof. |

## Safety invariants (condensed)

1. GitHub remains authoritative on PR merges, check results and repository access.
2. Submission, review, CI success, merge, and release are distinct states.
3. No remote destructive action without authority, scope and current-state validation.
4. No silent loss of dirty, unmerged, or differently-owned work.
5. No unbounded automated repair or retry loops.
6. No bypass of required CI/reviews/protection by force-push or direct push.
7. No treating AI output or untrusted GitHub text as a grant of authority.
8. No automatic Git Dynamic Conflict audit invocation; it is human-initiated and read-only.
9. No assumption of safety from an AI report with zero findings.
10. Do not block tasks unrelated to a failure unless actual shared-integration constraints require it.

## Verification priorities

- Test concurrency races, stale state and interrupted writes, not only happy paths.
- Test authorization failures and cross-task working-directory errors.
- Test PR lifecycle outcomes individually: open, draft, CI pending, failing, review blocked, conflict, merged, closed without merge.
- Test stale reports/results and mismatched SHA references.
- Test malicious text in issues, comments, diffs, and logs.
- Test that manual audit cannot mutate repository state.

## Outstanding design topics

Identity, locks/leases, branch integration policy, rollback/compensation, verification provenance, secret storage, cross-machine state and audit records all remain unselected pending the explicit design discussions in [D01–D29](05-decisions-register.md).
