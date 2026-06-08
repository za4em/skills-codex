---
name: visualize
description: Creates an HTML page for human to review.
disable-model-invocation: true
---

Create a single self-contained HTML review page for a PR, local changes, or user-specified scope.

Do not create generic documentation.
Do not over-explain every file.
The goal is to help a human reviewer quickly build a mental model.

## Visual system

Start from [template.html](template.html). Keep its CSS intact; adapt structure and content to the change set.

Use these building blocks:

| Class / element | Use for |
|-----------------|---------|
| `header` + `h1` | Title and scope line |
| `section` + `h2` | Major areas — pick sections that fit |
| `.card` | Changed areas, concepts, grouped notes |
| `.warn` | Risky logic, breaking behavior, things to verify |
| `table` | Files and responsibilities |
| `ol` / `ul` | Flows, lists |
| `pre` / `code` | Short snippets when words are not enough |
| `details` | Optional depth without cluttering the main view |

Rules for the page:

- One self-contained HTML file — keep template colors, fonts, and CSS; no JS or frameworks.
- Font: Commit Mono via template CDN links; falls back to locally installed `CommitMono`.
- Write to the workspace (e.g. `review.html`) and tell the user the path.
- Accent CSS vars (`--red`, `--gold`, `--teal`, etc.) and `.accent-*` classes are available for emphasis.

## Content

Choose what helps the reviewer understand the change. Common useful sections:

- Summary of what changed and why it matters
- Main concepts
- Runtime or data flow
- Changed files grouped by responsibility
- Risk areas and review focus

Use judgment on depth and length — match the complexity of the change, not a fixed template.
