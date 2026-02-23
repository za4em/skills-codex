---
name: tech-designer
description: Produce implementation blueprints for existing codebases. Use when requirements are ready and the user needs a concrete technical design with module structure, data models, function/system contracts, state ownership, execution order, persistence/schema changes, invariants, and an execution checklist in `docs/plan.md` (with optional phased `docs/plan_XX.md` files for large features).
---

# Tech Designer

## Overview

Convert approved requirements into an implementation blueprint that another engineer can implement without guessing architecture, ownership, or contracts.

Prioritize design precision over broad planning text. Reuse existing architecture and patterns before adding new abstractions.

## Default Deliverables

Always produce and persist:
- `docs/plan.md` as the master implementation plan.

`docs/plan.md` must include:
- Feature overview.
- High-level technical decisions that apply globally.
- Shared constraints, invariants, and acceptance criteria.
- Checklist tracking execution progress.

For large features with multiple phases:
- Split detailed execution into `docs/plan_01.md`, `docs/plan_02.md`, etc.
- Keep `docs/plan.md` as the index/router with links to each phase plan.
- Keep a phase-level checklist in `docs/plan.md` to track overall phase status.

## Workflow

1. Capture and normalize requirements.
- Consolidate current user request and any prior handoff (for example from `$product-manager`).
- Write a single requirement baseline with explicit assumptions.
- Include this baseline in `docs/plan.md` under Input Traceability.

2. Read repository constraints first.
- Read `AGENTS.md` before designing.
- Extract binding rules: architecture constraints, style constraints, workflow constraints.
- Treat repository-local policies as non-optional.

3. Analyze current codebase and identify reuse targets.
- Read only relevant entry points/modules.
- Identify existing resources, models, messages/events, schedules, persistence boundaries, and error types.
- Map concrete files that should be extended vs newly created.

4. Make key technical decisions.
- Choose module ownership boundaries and integration direction.
- Define runtime state ownership and invariants.
- Define contract style (functions, systems, events/messages, service methods).
- Define ordering/scheduling and side-effect sequencing.
- Ask questions only when the answer materially changes design.

5. Write blueprint-level technical plan.
- Specify exact models/resources/entities and their fields.
- Specify method/system contracts (inputs, outputs, side effects, failure paths).
- Specify module boundaries and responsibilities.
- Specify state/control/data flow, including transitions.
- Specify persistence schema changes and version behavior.
- Specify error handling strategy, invariants, and validation rules.
- Specify testing strategy linked to design guarantees.

6. Define checklist structure.
- For small/medium features: keep one execution checklist directly in `docs/plan.md`.
- For large features: create phased plans `docs/plan_01.md`, `docs/plan_02.md`, etc.
- In split mode, keep `docs/plan.md` focused on shared context and phase index/checklist.
- For every task, add traceability reference to plan subsection and file/test/checkpoint.
- Keep checklist items focused on implementation work, not generic reminders.

7. Persist artifacts.
- Write/update `docs/plan.md`.
- Write/update `docs/plan_XX.md` files when split mode is needed.
- If unresolved critical decisions remain, ask targeted questions first, then finalize artifacts.

8. Recommend execution handoff.
- End by recommending: `Run $vibe-coder.`

## Plan Requirements (Mandatory)

Keep plans practical and execution-ready.

Every plan must define:
- What is being built.
- Which files/modules are expected to change.
- Key technical decisions that affect implementation.
- A checklist of atomic tasks that can be checked off.
- Validation steps and acceptance criteria.
- Known risks, blockers, or unresolved questions.

Avoid "clever" structure or abstract prose. Prefer short, direct language.

## Question Rules

Ask only questions that change design decisions such as:
- module ownership,
- contract shape,
- state transition policy,
- persistence compatibility policy,
- user-control vs automatic behavior.

Prefer concise option-based questions with a recommended option first.

## Output Format

Use this response structure:

### Requirement Intake
- Consolidated baseline requirements
- Explicit assumptions

### AGENTS.md Constraints
- Binding constraints that shape implementation

### Codebase Analysis
- Existing architecture and reusable modules
- Key extension points and target files

### Technical Blueprint
- Architecture and module ownership
- Data model and schema design
- Contract definitions (functions/systems/messages/APIs)
- Execution order and state transitions
- Persistence/versioning strategy
- Error handling and invariants
- Test strategy tied to guarantees

### Open Technical Questions
1. Only if unresolved and material

### Artifact Write Status
- `docs/plan.md`: written/updated
- `docs/plan_XX.md`: written/updated when needed

### Next Step
- Recommend: `Run $vibe-coder.`

## `docs/plan.md` Template

Use one of these two formats based on feature size.

### Single-file mode (small/medium feature)

```md
# Implementation Plan: [Feature Name]

## Goal
- What we are building and why.

## Files and Modules
- Existing files to update
- New files to add (if any)

## Key Technical Decisions
- Decision: [what]
- Why: [reason/tradeoff]

## Checklist
- [ ] [atomic task] (file: [path], ref: [section])
- [ ] [atomic task] (file: [path], ref: [section])

## Validation
- [ ] [test or lint command]
- [ ] [manual verification]

## Risks / Open Questions
- [risk, blocker, or unresolved decision]
```

### Split mode (large feature)

```md
# Implementation Plan: [Feature Name]

## Goal
- What we are building and why.

## Shared Constraints
- Global constraints that apply to all phases.

## Shared Technical Decisions
- Cross-phase decisions that apply to all phases.

## Phase Index
- [ ] Phase 01: [name] -> [docs/plan_01.md](plan_01.md)
- [ ] Phase 02: [name] -> [docs/plan_02.md](plan_02.md)

## Global Validation
- [ ] [end-to-end checks spanning phases]

## Global Risks / Open Questions
- [cross-phase risks or blockers]
```

## `docs/plan_XX.md` Template (Split Mode)

When split mode is used, write each phase file (for example
`docs/plan_01.md`) using this structure:

```md
# Phase Plan [NN]: [Phase Name]

## Phase Goal
- What this phase delivers.

## Dependencies
- Dependencies/entry criteria

## Implementation Checklist
- [ ] [atomic task] (file: [path], ref: [section])
- [ ] [atomic task] (file: [path], ref: [section])

## Validation
- [ ] [test command or test task]
- [ ] [manual check]

## Done When
- Conditions required before this phase is complete
```

## Guardrails

- Do not implement production code in this skill; produce design artifacts only.
- Keep design concrete enough that implementation does not require architecture guesswork.
- Reuse existing modules and patterns before introducing new abstractions.
- Prefer small, decoupled components and explicit contracts.
- Keep checklist entries directly traceable to plan subsections.
- Keep templates simple and useful; remove sections that do not drive execution.
- End with: `Run $vibe-coder.`
