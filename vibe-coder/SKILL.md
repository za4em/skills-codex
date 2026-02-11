---
name: vibe-coder
description: Implement the next planned work item from project docs. Use when a user asks to execute development based on `docs/spec.md` and `docs/todo.md`, requiring code changes aligned with the approved spec, existing architecture/style/patterns, reuse of existing components, and automatic marking of completed todo checklist steps.
---

# Vibe Coder

## Overview

Execute implementation incrementally from approved planning docs.

Read `docs/spec.md` and `docs/todo.md`, implement the next unchecked checklist step, verify alignment with the spec and repository conventions, and mark that step done.

## Workflow

1. Load planning context.
- Read `docs/spec.md` and `docs/todo.md`.
- If either file is missing, stop and ask the user to provide or generate it.
- Extract constraints, acceptance criteria, boundaries, and explicit non-goals.

2. Select the next step.
- Find the earliest unchecked checklist item (`- [ ]`) in `docs/todo.md`.
- Treat that item as the active scope.
- Respect boundaries defined for that phase/task in `docs/todo.md`.
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
- Check implemented behavior against `docs/spec.md` acceptance criteria.
- Check consistency with current codebase conventions.
- Run focused validation commands when feasible (tests/lint/build for impacted area).

6. Mark completion.
- Update `docs/todo.md` by converting the completed item from `- [ ]` to `- [x]`.
- Mark only items fully completed.
- If partially completed, keep it unchecked and note what remains.

7. Report outcome.
- Summarize what was implemented.
- List updated files and validations run.
- Note follow-up risks, blockers, or remaining questions.

8. Recommend handoff when done.
- If no unchecked checklist items remain in `docs/todo.md`, advise the user to clear context/start a new session and run `$code-reviewer`.

## Output Format

Use this structure after each execution cycle.

### Active Todo Step
- [copied checklist item from `docs/todo.md`]

### Implementation Summary
- [what changed]

### Spec Alignment
- [how the change satisfies spec requirements]

### Todo Boundary Alignment
- [how implementation stayed inside defined in-scope/out-of-scope boundaries]

### Codebase Alignment
- [how existing patterns/components were reused]

### Validation
- [tests/lint/build commands run and outcomes]

### Todo Update
- [state whether the step was marked `- [x]` in `docs/todo.md`]

### Next Item
- [next unchecked checklist item, if any]

### Final Handoff (When Todo Complete)
- [if all items are complete: `Clear context/start a new session, then run $code-reviewer.`]

## Guardrails

- Do not implement multiple checklist items in one pass unless the user explicitly requests batching.
- Do not mark a step done if acceptance criteria are not met.
- Do not drift beyond `docs/spec.md` scope or `docs/todo.md` boundaries without user approval.
- Prefer minimal, targeted changes over broad refactors.
- Prefer existing components and established repository approaches before creating new ones.
- When all checklist items are complete, end with: `Clear context/start a new session, then run $code-reviewer.`
