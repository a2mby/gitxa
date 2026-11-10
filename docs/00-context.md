# Project context and origin

**Status:** requirements captured; no implementation architecture has been agreed.

## Origin: strict CI became a workflow bottleneck

The idea originated while building **Apixa**, a TypeScript networking library with strict GitHub CI checks: multiple Node.js baselines, frozen-lockfile installation, build, architectural boundaries, API/export contract checks, typechecking, tests, clean consumer installations, real browser/SSR verification, and Edge-runtime verification. This CI is valuable and **must not be removed to make development faster**.

The existing development flow was effectively sequential:

1. `/plan-change <brief>` opens a GitHub issue, identifies expected code/test/document paths, and creates `task/N-slug` from latest `main`.
2. Implement the change with tests.
3. `/git-push` reads the issue and task branch, updates the story/acceptance records, formats, commits, rebases, pushes, creates the PR, and attempts to squash-merge it. It expects the branch to be merged and cleaned up before finishing.
4. Starting the next task becomes awkward while CI or integration is pending, even if the tasks are unrelated.

The original skills are deliberately strict: issue traceability, branch isolation, per-change tests, no unrelated dirty files, no credential commits, recent `main`, squash history, change-log updates. Gitxa must preserve the **intent** of these controls while removing unnecessary serialized waiting.

## Product imagination

- A developer opens **Thread 1** asking for tasks 1–6; tasks 1→2→3 may be sequential, task 4 may depend on them, and tasks 5/6 run independently.
- A different thread asks for tasks 7–9 while Thread 1 is still active.
- The factory organizes distinct GitHub issues and branches per task; multiple tasks can be under development simultaneously without overwriting each other.
- One settlement request submits eligible work together or separately under explicit policy; CI, review, and merging continue independently of new development.
- Routine errors may be retried/fixed **within strict, bounded, authorized limits**. Major conflicts and design decisions return to the developer. Do not create an issue for every failing test.
- Gitxa supports a **single user with many agents**, **several developers**, **hybrid teams**, and **several repositories**, without requiring a particular IDE or AI platform.
- A merging developer may request a **read-only, on-demand AI semantic audit across PRs** to catch logic conflicts missed by ordinary textual merge checks.

## Current intent and project constraints

- Gitxa is primarily a **personal/reusable engineering tool for the owner's repositories**, not a commercial product plan.
- The interface should feel **skill-first**. Deterministic enforcement is required where instructions alone cannot guarantee concurrency or safety.
- The user explicitly asked for **a dedicated open-source GitHub repository** and **all documentation first** before discussing implementation tools and architecture.
- **No architecture is to be predicted or selected at this stage.** Previous discussions included examples such as CLI, worktrees, code-based rules, auto-merge, and GitHub adapters. These are **candidates for future decisions, not an accepted design**.
- Detailed questions about who can request merges, merge methods, task dependency strategies, state, coordination, audit authority, and release behavior are **open**.

## Project-level change discipline

New features should extend the existing numbered backlog/use cases/decision register rather than silently rewriting earlier agreements. Discussion examples must be labeled as examples and must not be reinterpreted as settled policies.
