---
name: tech-designer
description: Technical design and implementation-spec creation for existing codebases. Use when the user provides feature requirements directly or via a previous skill (for example `$product-manager`) and needs a concrete spec for how to implement it in the current repository. Analyze `AGENTS.md`, existing architecture, design approach, code style, patterns, and reusable components; ask targeted implementation-decision questions; then write `docs/spec.md` and `docs/todo.md` with phased implementation checklists, and recommend `$vibe-coder`.
---

# Tech Designer

## Overview

Convert approved feature requirements into an implementation-ready technical specification for the current repository.

Use existing architecture and patterns first. Keep decisions traceable to user input and previous skill output.

## Workflow

1. Capture and normalize inputs.
- Collect requirements from current user prompt and any prior handoff (for example from `$product-manager`).
- Build a single requirement baseline before designing.
- Keep this baseline in the final spec so context persists.

2. Read repository policy and constraints.
- Locate and read `AGENTS.md` first.
- Extract mandatory rules, architecture conventions, and workflow constraints.
- Treat repository-local policy as binding.

3. Analyze existing codebase.
- Read only relevant modules and entry points.
- Identify architecture style, design patterns, code style conventions, and reusable components.
- Map where feature changes should live with concrete file paths.

4. Design the implementation approach.
- Propose the implementation approach grounded in current codebase patterns.
- When needed, offer 1-3 approach options with tradeoffs and a recommendation.
- Ask targeted questions when decisions are ambiguous (what to use, where to place logic, which approach to choose).

5. Produce full technical specification.
- Define what should be built and how it should be implemented.
- Specify responsibilities by layer/module and file-level impact.
- Include integration points, state/data flow, error handling, and validation strategy.
- Include testing strategy and rollout/verification approach.

6. Produce phased implementation checklist.
- Build implementation phases that map to the technical design (for example: setup, core build, integration, verification).
- Under each phase, add actionable checklist items.
- Each checklist item must reference where it traces back in `docs/spec.md` (section or file-level change).

7. Persist artifacts.
- Write or update `docs/spec.md` with the finalized technical spec.
- Include an explicit "Input Traceability" section linking final design decisions back to user requirements and prior handoffs.
- Write or update `docs/todo.md` with implementation phases and checklists aligned to the finalized spec.
- If critical decisions remain unresolved, ask questions first, then finalize and write both `docs/spec.md` and `docs/todo.md` after answers.

8. Advise next skill.
- End by recommending start a new session and use `$vibe-coder` for implementation execution.

## Output Format

Use this response structure:

### Requirement Intake
- [consolidated requirement baseline from user and prior handoff]

### AGENTS.md Constraints
- [rules and conventions that must shape implementation]

### Codebase Analysis
- [architecture, style, reusable patterns/components, relevant files]

### Technical Design Proposal
- [recommended approach and why]
- [file-by-file implementation plan]
- [data/state flow and integration points]
- [failure handling and edge cases]
- [test strategy and verification]

### Open Technical Questions
1. [question that changes implementation approach]
2. [question that changes component/module placement]

### Artifact Write Status
- [confirm `docs/spec.md` written, or list blockers]
- [confirm `docs/todo.md` written, or list blockers]

### Next Step
- Recommend: `Run $vibe-coder.`

## `docs/spec.md` Template

Write `docs/spec.md` using this structure:

```md
# Technical Specification: [Feature Name]

## 1. Context and Inputs
- Original request
- Prior handoff input (if any)
- Input Traceability (decision -> source requirement)

## 2. Goals and Scope
- In scope
- Out of scope

## 3. Repository Constraints
- AGENTS.md rules that affect implementation
- System/module constraints

## 4. Existing Codebase Findings
- Relevant architecture and patterns
- Reusable components/modules
- Key files to modify

## 5. Proposed Implementation Design
- Design overview
- Responsibilities by layer/module
- Detailed file-level changes
- Data/state/control flow
- APIs/contracts/events impacted

## 6. Error Handling and Edge Cases
- Failure scenarios
- Recovery behavior

## 7. Testing and Verification
- Unit/integration/UI tests to add or update
- Manual verification checklist

## 8. Risks and Mitigations
- Technical risks, impact, mitigation

## 9. Rollout Notes
- Migration/backward-compatibility considerations
- Release/verification checkpoints
```

## `docs/todo.md` Template

Write `docs/todo.md` using this structure:

```md
# Implementation Todo: [Feature Name]

## Phase 1: Setup and Contracts
- [ ] [task] (ref: spec §[section], file: [path])
- [ ] [task] (ref: spec §[section], file: [path])

## Phase 2: Core Implementation
- [ ] [task] (ref: spec §[section], file: [path])
- [ ] [task] (ref: spec §[section], file: [path])

## Phase 3: Integration and Data Flow
- [ ] [task] (ref: spec §[section], file: [path])
- [ ] [task] (ref: spec §[section], file: [path])

## Phase 4: Validation and Error Handling
- [ ] [task] (ref: spec §[section], file: [path])
- [ ] [task] (ref: spec §[section], file: [path])

## Phase 5: Tests and Verification
- [ ] [task] (ref: spec §[section], test: [path])
- [ ] [task] (ref: spec §[section], manual: [verification step])

## Phase 6: Rollout Readiness
- [ ] [task] (ref: spec §[section], checkpoint: [note])
- [ ] [task] (ref: spec §[section], checkpoint: [note])
```

## Question Rules

- Ask only questions that materially change implementation design.
- Tie each question to a specific uncertainty in module ownership, flow, contract, or behavior.
- Prefer concise, decision-oriented questions with clear options.
- Avoid generic questions that do not affect the final spec.

## Guardrails

- Always analyze `AGENTS.md` and relevant existing code before finalizing design.
- Reuse existing patterns/components over introducing unnecessary abstractions.
- Keep recommendations aligned with current architecture and code style.
- Preserve earlier approved input from user or `$product-manager` in the final spec.
- Do not start coding in this skill; produce and persist specification + todo artifacts only.
- End with a recommendation to run `$vibe-coder`.
