---
name: vibe-coder
description: Execute the next unchecked plan item from `docs/plan.md` (and optional `docs/plan_XX.md` phase files) by reading the plan, exploring code, planning implementation, implementing, and updating plan progress.
---

# Vibe Coder

## Overview

Implement one planned checklist item per run, unless batch explicitly requested.

Use `docs/plan.md` as source of truth. If phase plans exist
(`docs/plan_01.md`, `docs/plan_02.md`, etc.), execute from the active phase
file and keep `docs/plan.md` phase status in sync.

## Workflow

1. Read plan and pick the next step.
- Read `docs/plan.md`.
- If `docs/plan.md` is missing, stop and ask the user to provide or generate it.
- Detect split mode from phase links/references to `docs/plan_XX.md`.
- Single-file mode: pick the earliest unchecked item (`- [ ]`) in `docs/plan.md`.
- Split mode: pick the earliest unchecked phase in `docs/plan.md`, then the
  earliest unchecked item in that phase file.
- If no unchecked items remain, report completion.

2. Explore code and plan the implementation.
- Explore existing code relevant to the active item before deciding implementation details.
- Reuse existing modules/components/patterns where possible.
- Create a short implementation plan scoped only to the active item.
- If the item is ambiguous or too large, ask clarifying questions before coding.

3. Implement the active item.
- Change only what is required for the active item.
- Add or update tests needed for this item.

4. Mark done and correct plan if needed.
- Run focused validation for impacted code (tests/lint/build as relevant).
- Mark the active item `- [x]` only when fully complete.
- In split mode, if a phase file is fully checked, mark its phase checkbox
  `- [x]` in `docs/plan.md`.
- If implementation decisions changed, update `docs/plan.md` and/or
  `docs/plan_XX.md` so the plan matches reality.
- Report what changed, plan updates, and the next step.

## Output Format

Use this structure after each run:

### Active Item
- [copied checklist item]

### Implementation Plan
- [short plan based on explored code]

### Changes Made
- [what changed]

### Plan Updates
- [checkbox updates and any plan corrections in `docs/plan.md` and/or `docs/plan_XX.md`]

### Validation
- [commands run and outcomes]

### Next Item / Completion
- [next unchecked item, or completion]

### Blockers / Assumptions
- [only unresolved blockers/assumptions]

### Final Handoff (When Complete)
- `Clear context/start a new session, then run $vibe-coder.`

## Question Rules

- Ask questions only when ambiguity changes implementation.
- Each question should resolve one decision.

## Guardrails

- Always explore relevant existing code before planning implementation.
- Do not implement multiple checklist items in one pass unless the user asks.
- Do not mark items complete if acceptance is not met.
- If implementation changes the intended approach, correct the plan immediately.
- Do not drift beyond plan boundaries without user approval.
- Prefer minimal, targeted changes over broad refactors.
- Follow existing repository patterns and `AGENTS.md` constraints.
