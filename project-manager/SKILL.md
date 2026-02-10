---
name: project-manager
description: Execution planning from an approved technical specification. Use when `docs/spec.md` exists and the user needs a strict implementation plan with checkboxes, clear boundaries per step, and traceability back to the spec. Produce and write `docs/plan.md`, then advise the user to clear context/start a new session and run `$vibe-coder`.
---

# Project Manager

## Overview

Convert `docs/spec.md` into an execution-ready implementation plan.

Build a checklist-based plan that follows the spec exactly, defines boundaries for each step, and makes progress trackable for agents.

## Workflow

1. Load planning inputs.
- Read `docs/spec.md` as the primary source of truth.
- Optionally read recent approved decisions from the user or prior skill outputs.
- If spec and later decisions conflict, ask the user which one is authoritative.

2. Validate plan readiness.
- Check whether the spec contains enough detail for implementation planning.
- Identify missing decisions that block sequencing or ownership.
- Ask only blocker questions that are necessary to create an executable plan.

3. Derive plan structure from spec.
- Split work into phases and ordered tasks based on spec sections.
- Keep strict scope discipline: include only tasks required by the spec.
- Add explicit boundaries for each task:
  - In scope
  - Out of scope
  - Completion criteria

4. Add execution controls.
- Use Markdown checkboxes for every task so agents can track completion.
- Add dependencies and sequencing notes where order matters.
- Add verification checkpoints tied to the spec acceptance criteria.

5. Persist plan.
- Write or update `docs/plan.md` with the finalized checklist plan.
- Preserve traceability: each task should map back to the relevant part of `docs/spec.md`.

6. Advise next skill.
- End by recommending the user clear context/start a new session.
- Then recommend running `$vibe-coder`.

## Output Format

Use this response structure:

### Spec Intake
- [summary of what was extracted from `docs/spec.md`]
- [blockers/missing info if any]

### Clarification Questions (Only If Blocked)
1. [question]
2. [question]

### Proposed Plan Structure
1. [phase name and objective]
2. [phase name and objective]

### Plan Write Status
- [confirm `docs/plan.md` written, or list blockers]

### Next Step
- Recommend: `Clear context/start a new session, then run $vibe-coder.`

## `docs/plan.md` Template

Write `docs/plan.md` using this structure:

```md
# Implementation Plan

## Source Specification
- Spec: `docs/spec.md`
- Planning assumptions: [resolved assumptions]

## Phase 1 - [Name]
Objective: [what this phase delivers]
Boundary:
- In scope: [items]
- Out of scope: [items]
- Done when: [completion criteria]
Tasks:
- [ ] [task 1]
- [ ] [task 2]
Dependencies:
- [dependency or `None`]
Verification:
- [how to verify this phase is complete]
Spec Traceability:
- [spec section(s) covered]

## Phase 2 - [Name]
Objective: [what this phase delivers]
Boundary:
- In scope: [items]
- Out of scope: [items]
- Done when: [completion criteria]
Tasks:
- [ ] [task 1]
- [ ] [task 2]
Dependencies:
- [dependency or `None`]
Verification:
- [how to verify this phase is complete]
Spec Traceability:
- [spec section(s) covered]
```

Add as many phases as needed, but keep tasks atomic and execution-ordered.

## Guardrails

- Treat `docs/spec.md` as authoritative unless the user explicitly overrides it.
- Do not add feature scope beyond the specification.
- Do not begin coding in this skill.
- Keep each task actionable, testable, and assignable.
- Ensure each phase has explicit boundaries and completion criteria.
- Ensure all tasks use Markdown checkboxes.
- Write `docs/plan.md` before finishing.
- End with: `Clear context/start a new session, then run $vibe-coder.`
