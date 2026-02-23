---
name: vibe-coder
description: Implement the next planned work item from project docs. Use when a user asks to execute development based on `docs/plan.md` (and optional `docs/plan_XX.md` phase files), requiring code changes aligned with the approved plan, existing architecture/style/patterns, reuse of existing components, and automatic checklist updates.
---

# Vibe Coder

## Overview

Execute implementation incrementally from approved planning docs.

Read `docs/plan.md`, implement the next unchecked checklist step, verify
alignment with plan requirements and repository conventions, and mark that step
done. When phased plans exist (`docs/plan_01.md`, `docs/plan_02.md`, etc.),
execute from the active phase file while keeping `docs/plan.md` phase status
in sync.

## Workflow

1. Load planning context.
- Read `docs/plan.md`.
- If `docs/plan.md` is missing, stop and ask the user to provide or generate it.
- Detect split mode by phase links/references to `docs/plan_XX.md` in `docs/plan.md`.
- In split mode, read the active phase file(s) needed for the next step.
- Extract constraints, acceptance criteria, boundaries, and explicit non-goals.

2. Select the next step.
- Single-file mode: find the earliest unchecked checklist item (`- [ ]`) in `docs/plan.md`.
- Split mode: find the earliest unchecked phase in `docs/plan.md`, then find the earliest unchecked checklist item in that phase file (`docs/plan_XX.md`).
- Treat that item as the active scope.
- Respect boundaries defined in `docs/plan.md` and the active phase plan file (if split mode).
- If the step is ambiguous or too large, ask clarifying questions before coding.

3. Map implementation to current codebase.
- Identify relevant modules, components, and existing approaches.
- Reuse existing components/utilities/patterns when applicable.
- Avoid introducing new abstractions when an existing approach fits.

4. Implement the step.
- Make only the code changes required for the active checklist item.
- Keep changes aligned with architecture boundaries and code style.
- Update or add tests needed for the behavior introduced by this step.

5. Verify alignment.
- Check implemented behavior against acceptance criteria and technical decisions in `docs/plan.md` (and active phase plan if applicable).
- Check consistency with current codebase conventions.
- Run focused validation commands when feasible (tests/lint/build for impacted area).

6. Mark completion.
- Update the active plan checklist item from `- [ ]` to `- [x]`.
- In split mode, when a phase file has no unchecked items left, mark the corresponding phase checkbox as done in `docs/plan.md`.
- Mark only items fully completed.
- If partially completed, keep it unchecked and note what remains.

7. Report outcome.
- Summarize what was implemented.
- List updated files and validations run.
- Note follow-up risks, blockers, or remaining questions.

## Output Format

Use this structure after each execution cycle.

### Active Plan Step
- [copied checklist item from active plan file]

### Implementation Summary
- [what changed]

### Plan Alignment
- [how the change satisfies plan requirements]

### Plan Boundary Alignment
- [how implementation stayed inside defined boundaries]

### Codebase Alignment
- [how existing patterns/components were reused]

### Validation
- [tests/lint/build commands run and outcomes]

### Plan Update
- [state whether the step was marked `- [x]` in the active plan file]
- [if split mode: state whether phase status was updated in `docs/plan.md`]

### Next Item
- [next unchecked checklist item, if any]

### Final Handoff (When Plan Is Complete)
- [if all items are complete: `Clear context/start a new session, then run $commit.`]

## Guardrails

- Do not implement multiple checklist items in one pass unless the user explicitly requests batching.
- Do not mark a step done if acceptance criteria are not met.
- Do not drift beyond `docs/plan.md` scope and active plan boundaries without user approval.
- Prefer minimal, targeted changes over broad refactors.
- Prefer existing components and established repository approaches before creating new ones.
