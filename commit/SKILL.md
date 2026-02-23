---
name: commit
description: Create or update git commit messages following a conventional commit format with strict subject/body rules and scope selection. Use when the user asks to create a commit, write a commit message, or run a /commit workflow.
---

# Commit

## Overview

Create conventional commit messages with enforced subject/body quality rules and a fixed pre-commit review sequence.

## Workflow

1. Run `git status` to see changed files.
2. Stage all changes with `git add -A`.
3. Run `git diff --staged` to review staged changes only.
4. Run `git log --oneline -5` to match repository style.
5. Select a type from: `feat`, `fix`, `refactor`, `build`, `docs`, `test`, `chore`, `perf`, `ci`.
6. Derive the scope from the affected module(s) and choose the most specific single scope, or ommit.
7. Write the subject in imperative mood, 50–72 chars, no trailing period.
8. Write a body that wraps at 72 chars and explains why, not just what.
9. Ensure the message never mentions AI tools or vendors.
10. Do not ask the user which files to stage; always commit all unstaged changes.
11. When running `git commit`, pass subject and body in one `-m` message block; do not use repeated `-m` flags unless explicitly requested.

## Scope selection

- Use a module name like `ui`, `core`, `auth`, `data`, `app`, or a feature module name.
- If changes span multiple modules, choose the most user-facing or highest-level module touched (for example `core` or `product`) instead of `*`.
- When unsure, prefer the most user-facing or highest-level module touched. For types like  `build`, `docs`, `chore`, `ci` can be ommited.

## Quality rules

- Subject length: 50–72 characters.
- Subject voice: imperative mood.
- Subject punctuation: no trailing period.
- Body: wrap at 72 characters; focus on intent and rationale.
- Avoid vague or informal wording.
- Never mention AI tools (e.g., Claude, Anthropic, Gemini).

## Examples

Good:
- `feat(user): add UserCard component for user data`
- `fix(auth): resolve token refresh race condition on logout`
- `refactor(ui): simplify line chart drawing and improve performance`
- `build: update app_version to 2.3`
- `docs: add payment module description and file structure`

Bad:
- `Claude fixed this`
- `made things better`
- `updated stuff`
