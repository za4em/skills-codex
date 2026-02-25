# Skills Workflow

Lean workflow skills for turning feature ideas into shipped code (excluding `.system` skills).

## Recommended Flow

1. Optional: `$prompt-engineer`
- Refine feature behavior, edge cases, constraints, and acceptance criteria.
- Use when requirements are not fully clear.

2. `$plan-designer`
- Produce a conceptual implementation plan in `docs/plan.md`.
- Focus on modules, key models/functions, major decisions, and checklist steps.
- Keep details provisional so they can be adjusted during implementation.
- Split into `docs/plan_01.md`, `docs/plan_02.md`, etc. for larger work.

3. `$vibe-coder`
- Read plan, take next unchecked step, explore relevant code, plan implementation, implement, and validate.
- Mark the step done and update/correct plan files when implementation changes the approach.
- When everything is complete, hand off to `$commit`.

## Utility Skills

4. `$commit`
- Create conventional commit messages and commit cleanly.

5. `$branch-description`
- Generate fixed-format GitLab PR/MR descriptions from commit ranges.

6. `$figma-implement`
- Implement UI from Figma nodes/URLs with close visual fidelity.

## Included Skills

- `prompt-engineer`
- `plan-designer`
- `vibe-coder`
- `commit`
- `branch-description`
- `figma-implement`
