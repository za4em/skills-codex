---
name: plan-designer
description: Produce conceptual implementation plans for existing codebases. Use when requirements are ready and the user needs a high-level technical design with modules, important models/functions, key decisions, and an execution checklist in `docs/plan.md` (with optional phased `docs/plan_XX.md` files for large features).
---

# Plan Designer

## Overview

Turn approved requirements into an implementation plan that can be executed
without architecture guesswork while staying implementation-agnostic.

## Default Deliverables

Always produce and persist:
- `docs/plan.md` as the master implementation plan.

`docs/plan.md` must include:
- Feature overview.
- High-level technical decisions that apply globally.
- Shared constraints and acceptance criteria.
- Checklist tracking execution progress.
- A note that implementation details can change based on better findings during execution.

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
- Scan only relevant areas and list reuse targets at the module/pattern level.

3. Define the technical blueprint.
- Specify important models/entities and their responsibilities.
- Specify high-level function/system responsibilities and expected behavior.
- Specify module boundaries and responsibilities.
- Do not prescribe concrete file paths, exact class signatures, or low-level implementation details.

4. Write plan artifacts.
- Always write/update `docs/plan.md`.
- For large features, split execution into `docs/plan_01.md`, `docs/plan_02.md`, etc.
- Keep checklist items atomic and traceable to conceptual modules/capabilities.
- Mark all proposed design details as provisional and adjustable when better implementation decisions are discovered.

5. Handoff.
- If critical decisions are unresolved, ask targeted questions before finalizing.
- End with: `Run $vibe-coder.`

## Plan Requirements (Mandatory)

Every plan must include:
- Goal
- Modules/capabilities to evolve
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
- Reuse targets and relevant module/pattern areas

### Technical Plan
- Conceptual models/entities and responsibilities
- High-level functions/contracts and expected behavior
- Module boundaries and responsibilities
- Validation approach
- Adaptability note (which decisions are provisional and can change)

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
- All design details in this plan are provisional and may be revised in place if better decisions are found during implementation.

## Modules and Capabilities
- Existing modules/capabilities to extend
- New modules/capabilities to introduce (if any)

## Technical Decisions
- Decision: [what]
- Why: [reason/tradeoff]

## Conceptual Design
- Key models/entities: [name + responsibility only]
- Key functions/services: [name + responsibility only]
- Module boundaries: [high-level ownership and interactions]

## Dependencies
- Prerequisites required before implementation starts.

## Checklist
- [ ] Define/update conceptual model/module decisions for [capability].
- [ ] Validate approach against constraints and acceptance criteria.
- [ ] Capture implementation readiness notes for the next execution step.

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
- All design details in this plan are provisional and may be revised in place if better decisions are found during implementation.

## Modules and Capabilities
- Shared modules/capabilities expected to evolve across phases.
- Note: phase-specific conceptual design lives in each `docs/plan_XX.md`.

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

## Modules and Capabilities
- Modules/capabilities expected to evolve in this phase.

## Technical Decisions
- Phase-specific decisions and rationale.

## Conceptual Design
- Key models/entities: [name + responsibility only]
- Key functions/services: [name + responsibility only]
- Module boundaries: [high-level ownership and interactions]

## Implementation Checklist
- [ ] Define/update conceptual model/module decisions for this phase.
- [ ] Validate phase approach against constraints and done conditions.
- [ ] Capture phase readiness notes for implementation.

## Validation
- [ ] [test command or test task]
- [ ] [manual check]

## Done When
- Conditions required before this phase is complete
```

## Guardrails

- Do not implement production code in this skill; produce design artifacts only.
- Keep design high-level and conceptual; avoid concrete file paths and low-level implementation details.
- Reuse existing modules and patterns before introducing new abstractions.
- Prefer small, decoupled components and explicit contracts.
- State clearly that any plan detail can be changed in place when a better technical decision is found.
- Keep checklist entries directly traceable to conceptual plan subsections.
- Keep templates simple and useful; remove sections that do not drive execution.
- End with: `Run $vibe-coder.`
