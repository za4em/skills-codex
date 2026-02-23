---
name: vibe-coder
description: Implement the next unchecked plan item from `docs/plan.md` (and optional `docs/plan_XX.md` phase files). Use when the user asks to execute planned development with minimal scoped code changes, focused validation, and checklist updates.
---

# Vibe Coder

## Overview

Implement one planned checklist item per run.

Use `docs/plan.md` as source of truth. If phase plans exist
(`docs/plan_01.md`, `docs/plan_02.md`, etc.), execute from the active phase
file and keep `docs/plan.md` phase status in sync.

## Workflow

1. Load plan context.
- Read `docs/plan.md`.
- If `docs/plan.md` is missing, stop and ask the user to provide or generate it.
- Detect split mode from phase links/references to `docs/plan_XX.md`.
- In split mode, read only the active phase file needed for the next item.

2. Select the active checklist item.
- Single-file mode: pick the earliest unchecked item (`- [ ]`) in `docs/plan.md`.
- Split mode: pick the earliest unchecked phase in `docs/plan.md`, then the
  earliest unchecked item in that phase file.
- If no unchecked items remain, report completion and recommend `$commit`.
- If the item is ambiguous or too large, ask clarifying questions before coding.

3. Implement the item.
- Change only what is required for the active item.
- Reuse existing modules/components/patterns.
- Add or update tests needed for this item.

4. Validate and update plan files.
- Run focused validation for impacted code (tests/lint/build as relevant).
- Mark the active item `- [x]` only when fully complete.
- In split mode, if a phase file is fully checked, mark its phase checkbox
  `- [x]` in `docs/plan.md`.

5. Report outcome.
- Summarize what changed and why.
- List validations run and outcomes.
- State plan updates made.
- Provide the next item or completion handoff.

## Output Format

Use this structure after each run:

### Active Item
- [copied checklist item]

### Changes Made
- [what changed]

### Validation
- [commands run and outcomes]

### Plan Updates
- [checkbox updates made in `docs/plan.md` and/or `docs/plan_XX.md`]

### Next Item
- [next unchecked item, if any]

### Blockers / Assumptions
- [only unresolved blockers/assumptions]

### Final Handoff (When Complete)
- `Clear context/start a new session, then run $commit.`

## Question Rules

- Ask questions only when ambiguity changes implementation.
- Ask at most 3 questions per turn.
- Each question should resolve one decision.

## Guardrails

- Do not implement multiple checklist items in one pass unless the user asks.
- Do not mark items complete if acceptance is not met.
- Do not drift beyond plan boundaries without user approval.
- Prefer minimal, targeted changes over broad refactors.
- Follow existing repository patterns and `AGENTS.md` constraints.
