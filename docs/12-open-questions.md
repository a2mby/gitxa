# Design discussion agenda (not answers)

The owner explicitly wants to discuss the **tools and architecture next**. Do not silently select a technology, data model, runtime, storage, merge policy or deployment strategy in these documents.

## Product and execution

- Should Gitxa initially be skills-only, a deterministic local helper, a shared service, or a hybrid? What guarantees are actually possible in each case?
- How does a brief become a dependable list of tasks? Who approves decomposition and inferred dependencies?
- How are multiple threads identified across separate AI conversations and different machines?
- Does the factory execute coding agents, or just coordinate the tasks they work on?
- Who can cancel, hand off or change an active task?

## Git and integration

- Is each task always its own issue and PR? What makes intentional grouping acceptable?
- How can many branches be worked on from one IDE while preventing cross-task staging?
- How are long dependent chains integrated while independent tasks advance?
- How strictly must branches track latest `main`? Do all changes require rebasing?
- Can merge requests be initiated from the user's device or only an authorized remote actor?
- Which merge methods are allowed? Can this differ by repository or risk level?
- What exactly does `settle` finish synchronously versus later remotely?
- What happens if checks pass individually but combined code would fail?

## Policy and security

- Where do rules live, who may change them and which may not be overridden?
- How do the system and GitHub verify identities and merge authorization?
- What are safe/unsafe automated repairs? What retry budgets apply?
- How are secrets, untrusted PR text and malicious actions protected?
- What must be recorded in an audit log versus left to GitHub events?

## State and multi-user

- What durable state is necessary? What remains authoritative on GitHub?
- How does the factory recover when an API call succeeds but its response is lost?
- What coordination is needed when multiple people or processes settle the same tasks concurrently?
- What is the cleanup and expiration policy for abandoned tasks and workspaces?

## Git Dynamic Conflict

- What combined-state analysis is meaningful and affordable?
- How to report probable logical conflicts without pretending to mathematically prove correctness?
- Does an audit always remain advisory or can a repository require a manually initiated report?
- How do we track the exact analyzed revisions and prevent stale findings from being trusted?
- How are multi-PR interactions handled that do not show up in pairwise comparison?

## Packaging and release

- How should other repos adopt Gitxa without duplicating complex skill prompts?
- When is project-specific publishing part of Gitxa, and when delegated elsewhere?
- What is the minimal first vertical slice that delivers the concurrency benefit without extra platform building?

Each question links conceptually to one or more of [D01–D29](05-decisions-register.md). **Nothing here is a chosen option.**
