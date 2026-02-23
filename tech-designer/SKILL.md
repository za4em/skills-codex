---
name: tech-designer
description: Produce implementation blueprints for existing codebases. Use when requirements are ready and the user needs a concrete technical design with module structure, data models, function/system contracts, state ownership, execution order, persistence/schema changes, invariants, and a phased todo mapped 1:1 to spec sections.
---

# Tech Designer

## Overview

Convert approved requirements into an implementation blueprint that another engineer can implement without guessing architecture, ownership, or contracts.

Prioritize design precision over broad planning text. Reuse existing architecture and patterns before adding new abstractions.

## Default Deliverables

Always produce and persist:
- `docs/spec.md` as the implementation blueprint.
- `docs/todo.md` as a phased checklist mapped directly to blueprint sections.

If the project uses split specs (for example MVP/full), write all required spec files and keep `docs/spec.md` as index/router.

## Workflow

1. Capture and normalize requirements.
- Consolidate current user request and any prior handoff (for example from `$product-manager`).
- Write a single requirement baseline with explicit assumptions.
- Include this baseline in the final spec under Input Traceability.

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

5. Write blueprint-level technical specification.
- Specify exact models/resources/entities and their fields.
- Specify method/system contracts (inputs, outputs, side effects, failure paths).
- Specify module boundaries and responsibilities.
- Specify state/control/data flow, including transitions.
- Specify persistence schema changes and version behavior.
- Specify error handling strategy, invariants, and validation rules.
- Specify testing strategy linked to design guarantees.

6. Write implementation todo mapped to blueprint.
- Build phases aligned with implementation order.
- Make tasks atomic and execution-ready.
- For every task, add traceability reference to spec subsection and file/test/checkpoint.
- Keep todo focused on implementation work, not generic reminders.

7. Persist artifacts.
- Write/update `docs/spec.md` (or split specs + `docs/spec.md` index when needed).
- Write/update `docs/todo.md`.
- If unresolved critical decisions remain, ask targeted questions first, then finalize artifacts.

8. Recommend execution handoff.
- End by recommending: `Run $vibe-coder.`

## Blueprint Requirements (Mandatory)

The spec must include concrete implementation blueprint details:
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
- `docs/spec.md`: written/updated
- `docs/todo.md`: written/updated

### Next Step
- Recommend: `Run $vibe-coder.`

## `docs/spec.md` Blueprint Template

Write `docs/spec.md` using this structure:

```md
# Technical Specification: [Feature Name]

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

## 5. Technical Blueprint
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

## 8. Risks and Mitigations
- Key technical risks and mitigation strategy

## 9. Rollout Notes
- Implementation sequencing and checkpoints
- Exit/acceptance criteria
```

## `docs/todo.md` Template

Write `docs/todo.md` using this structure:

```md
# Implementation Todo: [Feature Name]

## Phase 1: Contracts and Foundations
- [ ] [atomic task] (ref: spec §[section], file: [path])
- [ ] [atomic task] (ref: spec §[section], file: [path])

## Phase 2: Core Runtime Implementation
- [ ] [atomic task] (ref: spec §[section], file: [path])
- [ ] [atomic task] (ref: spec §[section], file: [path])

## Phase 3: Integration and State Flow
- [ ] [atomic task] (ref: spec §[section], file: [path])
- [ ] [atomic task] (ref: spec §[section], file: [path])

## Phase 4: Persistence and Compatibility
- [ ] [atomic task] (ref: spec §[section], file: [path])
- [ ] [atomic task] (ref: spec §[section], file: [path])

## Phase 5: Validation and Hardening
- [ ] [atomic task] (ref: spec §[section], file: [path])
- [ ] [atomic task] (ref: spec §[section], file: [path])

## Phase 6: Tests and Verification
- [ ] [test task] (ref: spec §[section], test: [path])
- [ ] [manual check] (ref: spec §[section], manual: [step])

## Phase 7: Rollout Readiness
- [ ] [checkpoint] (ref: spec §[section], checkpoint: [note])
- [ ] [checkpoint] (ref: spec §[section], checkpoint: [note])
```

## Guardrails

- Do not implement production code in this skill; produce design artifacts only.
- Keep design concrete enough that implementation does not require architecture guesswork.
- Reuse existing modules and patterns before introducing new abstractions.
- Prefer small, decoupled components and explicit contracts.
- Keep todo entries directly traceable to spec subsections.
- End with: `Run $vibe-coder.`
