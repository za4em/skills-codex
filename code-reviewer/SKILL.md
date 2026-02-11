---
name: code-reviewer
description: Review uncommitted repository changes for correctness and quality in a spec-and-todo driven workflow. Use when a user asks for review before commit, validating changes against `docs/spec.md`, `docs/todo.md` boundaries/checklists, existing codebase architecture and patterns, code style conventions, and clean code practices.
---

# Code Reviewer

## Overview

Review uncommitted changes with a code-review mindset.
Compare diffs to approved implementation artifacts (`docs/spec.md` and `docs/todo.md`) and repository patterns, identify issues by severity, and request concrete fixes before re-review.

When working in a repository that has an `AGENTS.md`, treat it as mandatory local policy.
Apply its rules, architecture guidance, and workflow conventions while evaluating the changes.

## Workflow

1. Collect review inputs.
- Inspect uncommitted changes (`git status`, staged + unstaged diffs).
- Read `docs/spec.md` and `docs/todo.md` if present.
- Read relevant codebase areas to understand architecture and existing patterns.

2. Load repository guidance.
- Locate and read `AGENTS.md` in the active repository before finalizing review conclusions.
- Extract applicable constraints: coding rules, architecture patterns, review expectations, and documentation limits.
- Treat `AGENTS.md` instructions as higher-priority than generic review defaults when they conflict.

3. Validate against implementation checklist.
- Check that changed behavior maps to checklist items and phase boundaries in `docs/todo.md`.
- Flag changes that implement out-of-checklist scope or violate defined in-scope/out-of-scope boundaries.
- Flag missing work if `docs/todo.md` marks tasks complete but code/tests do not satisfy completion criteria.
- If `docs/todo.md` is missing, state that as a review limitation and continue.

4. Validate against specification.
- Check whether changed behavior matches `docs/spec.md` scope and acceptance criteria.
- Flag missing required behavior, incorrect behavior, and out-of-scope additions.
- If `docs/spec.md` is missing, state that as a review limitation and continue with todo/code-quality review.

5. Validate architecture and patterns.
- Check module ownership, layering boundaries, and dependency direction.
- Check consistency with existing navigation/state/error/loading/testing patterns and `AGENTS.md` architecture conventions.
- Flag new abstractions that duplicate existing patterns without clear need.

6. Validate style and clean code.
- Check naming clarity, cohesion, function/class size, and readability.
- Check error handling, null safety, edge-case handling, and maintainability.
- Check test coverage for changed behavior and regression risk.

7. Report findings and request fixes.
- Report findings first, ordered by severity.
- Provide file references and clear remediation guidance.
- Ask the user to fix issues, then request a re-review.

8. Recommend next skill when clean.
- If there are no findings, recommend running `$commit`.

## Severity Model

Use these levels:
- `Blocking`: Must fix before merge. Correctness, security, data loss, contract breakage, or clear todo/spec violation.
- `Major`: High-priority quality or maintainability risk likely to cause defects.
- `Minor`: Improvement that should be addressed soon.

## Output Format

Use this structure in every review.

### AGENTS.md Constraints
- [applicable local rules and patterns used during review]

### Findings
1. `[Severity]` [short title]
- File: `[path:line]`
- Why: [impact/risk]
- Fix: [concrete change to make]

2. `[Severity]` [short title]
- File: `[path:line]`
- Why: [impact/risk]
- Fix: [concrete change to make]

### Todo Alignment (`docs/todo.md`)
- [what aligns with todo boundaries/checklist intent]
- [what is missing, out-of-boundary, or inconsistent with marked completion]

### Spec Alignment (`docs/spec.md`)
- [what matches spec]
- [what is missing or out of scope]

### Architecture/Pattern Alignment
- [consistency notes and deviations]

### Testing Gaps
- [missing tests or weak coverage]

### Required User Action
- [if findings exist: ask user to fix and request re-review]
- [if no findings: recommend running `$commit`]

If there are no findings, state exactly: `No blocking, major, or minor issues found in current uncommitted changes.`
Then recommend: `Run $commit.`

## Review Guardrails

- Always read and apply repository `AGENTS.md` guidance before finalizing recommendations.
- If `AGENTS.md` and this skill conflict, follow `AGENTS.md` for repository-local behavior.
- Prioritize bugs, behavioral regressions, todo/spec violations, and missing tests over stylistic nitpicks.
- Avoid broad rewrites when a targeted fix is sufficient.
- Do not modify files during review unless user explicitly asks for fixes.
- Keep feedback actionable and tied to changed lines.
- Treat absence of `docs/spec.md` or `docs/todo.md` as documented limitations, not a blocker for all review feedback.
- When no findings remain, end by recommending `$commit`.
