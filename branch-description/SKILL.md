---
name: branch-description
description: Generate fixed-format GitLab pull/merge request descriptions from a branch commit range. Use when the user asks to summarize commits in a branch (especially release branches like release/x.y.z) into a deterministic PR/MR description with the exact same section structure every time.
---

# Branch Description

Generate a GitLab PR/MR description with a strict, repeatable structure.

## Workflow

1. Identify the target branch from user input.
2. Resolve the base branch:
- If target matches `release/x.y.z`, list all release branches from local and remote refs, normalize to `release/x.y.z`, and choose the highest version lower than target as base.
- If no lower release branch exists, use merge-base against `main` (or `origin/main` if needed).
3. Collect commits with first-parent, excluding merge commits:
- `git log --first-parent --no-merges --oneline <base>..<target>`
4. Classify commit subjects:
- `Main Changes`: `feat(...)` and feature-like additions.
- `Fixes`: `fix(...)` and bug-fix subjects.
- `Refactors`: `refactor(...)`, `perf(...)`, `style(...)`, `test(...)`, and non-release `chore(...)` cleanup.
- `Release/Build`: `build:` commits, version bump commits, and release tooling bumps.
5. Extract release/build metadata:
- Version from subjects like `bump version_name to X.Y.Z` or `build: app N vX.Y.Z`.
- Build range from `build: app <number> ...` commits using min/max values.
6. Rewrite bullets in concise product language while preserving factual scope.
7. Produce output using the exact template below.

## Output Template (Do Not Change Section Names or Order)

```md
## Summary
<1-2 sentence release summary>

## Main Changes
- ...

## Fixes
- ...

## Refactors
- ...

## Release/Build
- Version bumped to `<version>`.
- Includes build bumps `<min>` through `<max>`.
```

## Formatting Rules

- Always output all five sections in the same order.
- Keep heading text exactly as in the template.
- Use flat bullet lists only.
- If a section has no items, write `- None.`
- Use backticks for versions and build numbers.
- Keep descriptions concise and release-note friendly.
- Do not include commit hashes in final output unless user asks.
