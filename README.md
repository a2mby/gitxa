# Gitxa

**Gitxa** is a proposed **skill-first, policy-driven GitHub development factory** for coordinating independent and dependent software changes across multiple tasks, conversations, developers, and AI coding agents **without weakening repository protections**.

> **Status: discovery / requirements only.** No implementation stack, runtime architecture, branch policy, merge strategy, approval model, licensing for contributions beyond the included project license, concurrency mechanism, toolchain, or delivery model has been selected. This repository is a preserved product specification for future discussion, **not an implemented factory**.

## Why it exists

A strict workflow of **issue → task branch → implementation → commit → PR → CI → merge** produces clean history, but becomes unnecessarily sequential if agents or users must wait for a PR to finish CI or merge before starting unrelated work. Gitxa aims to separate **development progress** from **integration readiness**, with explicit dependencies, safe isolation, recoverable operations, and strict policy enforcement.

## The imagined experience

- **Thread A:** `plan-change 1 2 3 4 5 6`. Tasks **1 → 2 → 3 → 4** depend on each other; **5** and **6** may progress independently.
- **Thread B:** `plan-change 7 8 9`. These tasks may progress alongside Thread A.
- Each task is traceable through a GitHub issue, branch, workspace, implementation, tests, and PR according to yet-to-be-decided policies.
- A **settle** action submits/integrates eligible work, notifies users of unresolved blockers, and does not block unrelated development while CI runs.
- A **human-initiated Git Dynamic Conflict audit** compares PRs for *logical* incompatibilities even when Git has no textual merge conflict. It is not an automatic check or an autonomous merge/fix mechanism.

## Documentation (the project's source of truth)

| File | Content |
| --- | --- |
| [Context](docs/00-context.md) | Origin, current pain, existing skills, constraints |
| [Vision and boundaries](docs/01-vision-and-scope.md) | Goals, non-goals, user personas, workflow vision |
| [Requirements](docs/02-requirements.md) | Functional and nonfunctional requirements; hard invariants |
| [Complete backlog](docs/03-backlog.md) | **23 epics** with detailed tasks and priorities |
| [Use cases](docs/04-use-cases.md) | **61 use cases** (UC01–UC61) |
| [Open decisions](docs/05-decisions-register.md) | **29 architectural/product decisions** (D01–D29), intentionally unresolved |
| [Milestones](docs/06-milestones-and-acceptance.md) | M1–M5 with acceptance criteria, no architecture commitments |
| [Scenarios](docs/07-scenarios.md) | Multi-thread, CI, collaboration, recovery and audit examples |
| [Potential skill interfaces](docs/08-skill-interface-candidates.md) | Exploratory user-facing commands; none frozen |
| [Git Dynamic Conflict](docs/09-git-dynamic-conflict.md) | Manually invoked semantic PR audit concept and constraints |
| [Safety and risks](docs/10-safety-and-risks.md) | Correctness, permissions, failure and recovery requirements |
| [Previous workflow](docs/11-existing-workflow.md) | Pre-factory Apixa `/plan-change` and `/git-push` behavior |
| [Questions for design](docs/12-open-questions.md) | Decision agenda before any implementation choices |
| [Glossary](docs/13-glossary.md) | Domain terms and distinctions |

## Requirements discipline

1. **Preserve the requirements and traceability.** Changes to backlog, use cases, and decision outcomes should be explicit and reviewable.
2. **Do not silently select architecture.** Tool choices, storage, execution model, worktree-versus-clone strategy, state management, integration method, and AI provider are **open**.
3. **Treat safety as a requirement, not a marketing claim.** Gitxa must not silently bypass CI, GitHub permissions, branch protections, reviews, or authorization.
4. **Do not promise perfect automation.** Merge safety, semantic conflict detection, and automatic repairs always have limitations and require appropriate escalation.
5. **Use the project for one developer and many, with or without agents.** AI is optional to the basic workflow; it is part of the proposed semantic audit feature.

## Current stage

- [x] Vision and motivating scenario documented
- [x] 23 epics, 61 use cases, 29 open decisions documented
- [x] Dynamic Conflict concept added as Epic 23
- [ ] Discuss tools and architecture, one decision at a time
- [ ] Approve implementation contracts and milestones
- [ ] Write executable code and tests

This is a **documentation-first open-source project**. Contributions should not treat discussion examples as settled engineering decisions. See [CONTRIBUTING.md](CONTRIBUTING.md).
