# Contributing to Gitxa

Gitxa is currently in **requirements/discovery**. Contributions should first improve requirements clarity, examples, use cases, security constraints, and unresolved decision records.

## Documentation changes

- Preserve stable epic IDs (01–23), use-case IDs (UC01–UC61), and decision IDs (D01–D29). Add new IDs instead of renumbering existing ones.
- Mark design options as **proposed** or **open** until the owner explicitly chooses them.
- Give changes to requirements an explicit rationale and any impacted use cases/acceptance criteria.
- Do not add implementation dependencies, configuration schemas, concrete storage technologies, workflow code, or architectural patterns as if approved.
- Keep safety rules: no silent CI bypass, no unauthorized merge, no discarded unmerged work, bounded automatic repairs, and manual semantic-audit invocation.

## Before implementation

Each architecture/product decision should eventually record its question, candidate options, trade-offs, owner choice, consequences, and affected requirements. The current register intentionally contains questions rather than answered decisions.
