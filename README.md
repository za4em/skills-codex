# Skills Workflow

This repository contains workflow skills that can be used to run a structured end-to-end development flow (excluding `.system` skills).

## Recommended Flow

1. `$product-manager`
- Refine a feature idea from a product perspective without technical design.
- Ask only feature-specific clarification questions that affect behavior.
- Produce a lean finalized brief:
  - Feature behavior definition
  - Critical edge cases
  - Dependencies and constraints
  - Acceptance criteria
  - Open assumptions
- Handoff to `$tech-designer`.

2. `$tech-designer`
- Analyze inputs + `AGENTS.md` + current codebase patterns.
- Define implementation approach and file-level design.
- Write `docs/spec.md` and `docs/todo.md` (phase-based checklist).
- Advise: run `$vibe-coder`.

3. `$vibe-coder`
- Implement the next unchecked item from `docs/todo.md`.
- Keep code aligned to `docs/spec.md` and todo boundaries.
- Mark completed checklist items in `docs/todo.md`.
- When all items are done, advise: clear context/start new session, then run `$code-reviewer`.

4. `$code-reviewer`
- Review uncommitted changes against `docs/spec.md`, `docs/todo.md`, and repository patterns.
- Report findings by severity with concrete fixes.
- If no issues remain, recommend running `$commit`.

## Additional Utility Skill

5. `$commit`
- Stage changes and create a conventional commit message.
- Keep message scope/type/subject/body aligned with repository commit style.

6. `$branch-description`
- Generate fixed-format GitLab PR/MR descriptions from a branch commit range.
- Useful for release branches (for example `release/x.y.z`) and deterministic changelog-style summaries.

## Skills Included

- `product-manager`
- `tech-designer`
- `vibe-coder`
- `code-reviewer`
- `commit`
- `branch-description`
