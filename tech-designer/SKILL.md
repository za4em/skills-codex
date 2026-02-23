---
name: tech-designer
description: Produce implementation plans for existing codebases. Use when requirements are ready and the user needs a concrete technical design with models/entities, method/system contracts, module boundaries, and an execution checklist in `docs/plan.md` (with optional phased `docs/plan_XX.md` files for large features).
---

# Tech Designer

## Overview

Turn approved requirements into an implementation plan that can be executed
without architecture guesswork.

## Default Deliverables

Always produce and persist:
- `docs/plan.md` as the master implementation plan.

`docs/plan.md` must include:
- Feature overview.
- High-level technical decisions that apply globally.
- Shared constraints and acceptance criteria.
- Checklist tracking execution progress.

For large features with multiple phases:
- Split detailed execution into `docs/plan_01.md`, `docs/plan_02.md`, etc.
- Keep `docs/plan.md` as the index/router with links to each phase plan.
- Keep a phase-level checklist in `docs/plan.md` to track overall phase status.

## Workflow

1. Normalize input.
- Merge the current request and any prior handoff into one requirement baseline.
- Record assumptions explicitly.

2. Load constraints and codebase context.
- Read `AGENTS.md` first and treat it as binding policy.
- Scan only relevant modules and list reuse targets + likely touched files.

3. Define the technical blueprint.
- Specify exact models/resources/entities and their fields.
- Specify method/system contracts (inputs, outputs, side effects, failure paths).
- Specify module boundaries and responsibilities.

4. Write plan artifacts.
- Always write/update `docs/plan.md`.
- For large features, split execution into `docs/plan_01.md`, `docs/plan_02.md`, etc.
- Keep checklist items atomic and traceable to files/tests.

5. Handoff.
- If critical decisions are unresolved, ask targeted questions before finalizing.
- End with: `Run $vibe-coder.`

## Plan Requirements (Mandatory)

Every plan must include:
- Goal
- Files/modules to change
- Key technical decisions
- Execution checklist (atomic tasks in `docs/plan.md` or `docs/plan_XX.md`)
- Validation and acceptance criteria
- Risks or open questions

Use short, direct language.

## Question Rules

Ask only questions that materially change models/entities, contracts, or module
boundaries. Prefer concise option-based questions.

## Output Format

Use this response structure:

### Requirement Baseline
- Final requirement summary
- Explicit assumptions

### AGENTS.md Constraints
- Rules that affect design

### Codebase Analysis
- Reuse targets and files likely to change

### Technical Plan
- Models/entities and fields
- Contracts (inputs, outputs, side effects, failure paths)
- Module boundaries and responsibilities
- Validation approach

### Open Technical Questions
- Only unresolved, material blockers

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

## Constraints
- Constraints that affect implementation.

## Files and Modules
- Existing files to update
- New files to add (if any)

## Technical Decisions
- Decision: [what]
- Why: [reason/tradeoff]

## Dependencies
- Prerequisites required before implementation starts.

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

## Constraints
- Constraints that apply across all phases.

## Files and Modules
- Shared files/modules expected to change across phases.
- Note: phase-specific file changes live in each `docs/plan_XX.md`.

## Technical Decisions
- Cross-phase decisions that apply to all phases.

## Phase Index
- [ ] Phase 01: [name] -> [docs/plan_01.md](plan_01.md)
- [ ] Phase 02: [name] -> [docs/plan_02.md](plan_02.md)

## Validation
- [ ] [end-to-end checks spanning phases]

## Risks / Open Questions
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

## Files and Modules
- Files/modules expected to change in this phase.

## Technical Decisions
- Phase-specific decisions and rationale.

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
