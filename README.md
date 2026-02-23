# Skills Workflow

This repository contains workflow skills that can be used to run a structured end-to-end development flow (excluding `.system` skills).

## Recommended Flow

1. `$prompt-engineer`
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
- Write `docs/plan.md` with overview, high-level technical decisions, and checklist.
- For large features, split into `docs/plan_01.md`, `docs/plan_02.md`, etc., and keep phase links/checklist in `docs/plan.md`.
- Advise: run `$vibe-coder`.

3. `$vibe-coder`
- Implement the next unchecked item from `docs/plan.md` (or active `docs/plan_XX.md` phase file).
- Keep code aligned to plan constraints, high-level decisions, and boundaries.
- Mark completed checklist items in the active plan file and update phase status in `docs/plan.md` when applicable.
- When all items are done, advise: clear context/start new session, then run `$commit`.

## Additional Utility Skills

4. `$commit`
- Stage changes and create a conventional commit message.
- Keep message scope/type/subject/body aligned with repository commit style.

5. `$branch-description`
- Generate fixed-format GitLab PR/MR descriptions from a branch commit range.
- Useful for release branches (for example `release/x.y.z`) and deterministic changelog-style summaries.

6. `$figma-implement`
- Translate Figma nodes into production-ready UI code with 1:1 visual fidelity.
- Use when implementing UI directly from Figma URLs or node IDs.

## Skills Included

- `prompt-engineer`
- `tech-designer`
- `vibe-coder`
- `commit`
- `branch-description`
- `figma-implement`
