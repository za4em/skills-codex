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
- Feature overview and scope.
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
- For small/medium scope: keep one execution checklist directly in `docs/plan.md`.
- For large scope: create phased plans `docs/plan_01.md`, `docs/plan_02.md`, etc.
- In split mode, keep `docs/plan.md` focused on shared context and phase index/checklist.
- For every task, add traceability reference to plan subsection and file/test/checkpoint.
- Keep checklist items focused on implementation work, not generic reminders.

7. Persist artifacts.
- Write/update `docs/plan.md`.
- Write/update `docs/plan_XX.md` files when split mode is needed.
- If unresolved critical decisions remain, ask targeted questions first, then finalize artifacts.

8. Recommend execution handoff.
- End by recommending: `Run $vibe-coder.`

## Blueprint Requirements (Mandatory)

The plan must include concrete implementation blueprint details:
- Module/file structure and ownership.
- Data model catalog (resources/entities/config/schema structs).
- Function/system/API/message contracts.
- Deterministic ordering (schedule/system sequence) where relevant.
- Persistence mapping and schema versioning behavior.
- Invariants and validation rules.
- Failure behavior and recovery expectations.
- Acceptance criteria and tests that prove the design.

Avoid vague language like "add support" without describing where and how.

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

Write `docs/plan.md` using this structure:

```md
# Implementation Plan: [Feature Name]

## 1. Context and Inputs
- Original request
- Prior handoff input (if any)
- Assumptions
- Input Traceability (decision -> source requirement)

## 2. Goals and Scope
- In scope
- Out of scope

## 3. Repository Constraints
- AGENTS.md and repository constraints that affect implementation

## 4. Existing Codebase Findings
- Reusable architecture/components
- Relevant files and extension points

## 5. Shared Technical Blueprint
### 5.1 Module and Ownership Design
- Module boundaries and responsibilities
- Existing files to extend and new files to add

### 5.2 Data Models and Schema
- Runtime resources/entities/value objects with fields
- Config/schema structs and validation rules

### 5.3 Contract Design
- Function/system signatures (or equivalent contracts)
- Message/event/API payloads and semantics
- Side effects and failure return paths

### 5.4 Execution and State Flow
- Deterministic ordering/scheduling
- State transitions and lifecycle rules
- Data/control flow between modules

### 5.5 Persistence and Compatibility
- Save/load model mapping
- Schema version behavior and compatibility policy

## 6. Error Handling and Invariants
- Failure scenarios and expected handling
- Invariants that must always hold

## 7. Testing and Verification
- Unit tests tied to contracts and invariants
- Integration tests tied to cross-module flows
- Manual verification checklist

## 8. High-Level Technical Decisions
- Decision and rationale (global, cross-phase decisions only)

## 9. Execution Tracking
### 9.1 Single-file mode (small/medium feature)
- [ ] [atomic task] (ref: plan §[section], file/test/checkpoint: [path or note])

### 9.2 Split mode (large feature)
- [ ] Phase 1: [name] -> [docs/plan_01.md](plan_01.md)
- [ ] Phase 2: [name] -> [docs/plan_02.md](plan_02.md)

## 10. Risks and Mitigations
- Key technical risks and mitigation strategy

## 11. Rollout Notes
- Implementation sequencing and checkpoints
- Exit/acceptance criteria
```

## `docs/plan_XX.md` Template (Split Mode)

When split mode is used, write each phase file (for example `docs/plan_01.md`)
using this structure:

```md
# Phase Plan [NN]: [Phase Name]

## 1. Phase Scope and Boundaries
- In scope for this phase
- Out of scope for this phase
- Dependency/entry criteria

## 2. Implementation Checklist
- [ ] [atomic task] (ref: plan §[section], file/test/checkpoint: [path or note])
- [ ] [atomic task] (ref: plan §[section], file/test/checkpoint: [path or note])

## 3. Verification for This Phase
- [ ] [test task] (ref: plan §[section], test: [path])
- [ ] [manual check] (ref: plan §[section], manual: [step])

## 4. Exit Criteria
- Conditions required before this phase is considered complete
```

## Guardrails

- Do not implement production code in this skill; produce design artifacts only.
- Keep design concrete enough that implementation does not require architecture guesswork.
- Reuse existing modules and patterns before introducing new abstractions.
- Prefer small, decoupled components and explicit contracts.
- Keep checklist entries directly traceable to plan subsections.
- End with: `Run $vibe-coder.`
