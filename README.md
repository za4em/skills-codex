# Skills Workflow

This repository contains workflow skills that can be used to run a structured end-to-end development flow (excluding `.system` skills).

## Recommended Flow

1. `$product-manager`
- Refine a feature idea from product perspective.
- Ask feature-specific questions.
- Produce finalized feature brief and handoff for technical design.

2. `$tech-designer`
- Analyze inputs + `AGENTS.md` + current codebase patterns.
- Define implementation approach and file-level design.
- Write `docs/spec.md`.

3. `$project-manager`
- Convert `docs/spec.md` into execution plan.
- Create boundary-defined checklist phases/tasks.
- Write `docs/plan.md`.
- Advise: clear context/start new session, then run `$vibe-coder`.

4. `$vibe-coder`
- Implement the next unchecked item from `docs/plan.md`.
- Keep code aligned to `docs/spec.md` and plan boundaries.
- Mark completed checklist items in `docs/plan.md`.
- When all items are done, advise: clear context/start new session, then run `$code-reviewer`.

5. `$code-reviewer`
- Review uncommitted changes against `docs/spec.md`, `docs/plan.md`, and repository patterns.
- Report findings by severity with concrete fixes.
- If no issues remain, recommend running `$commit`.

6. `$commit`
- Stage changes and create a conventional commit message.
- Keep message scope/type/subject/body aligned with repository commit style.

## Additional Utility Skill

7. `$branch-description`
- Generate fixed-format GitLab PR/MR descriptions from a branch commit range.
- Useful for release branches (for example `release/x.y.z`) and deterministic changelog-style summaries.

## Skills Included

- `product-manager`
- `tech-designer`
- `project-manager`
- `vibe-coder`
- `code-reviewer`
- `commit`
- `branch-description`
