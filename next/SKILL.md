---
name: next
description: Actionable work queue — shows next task per category, blocked items, and completed categories
user-invocable: true
disable-model-invocation: true
---

# /next — Actionable Work Queue

Read `tasks.org` in the project root (org-mode format) and show the next actionable task per category. **Never modify `tasks.org`.**

## Steps

1. Read `tasks.org`
2. Parse org-mode headings and TODO/WORKING/DONE keywords
3. For each top-level category (Laowa Lens, MacBook Pro, Synology, etc.), determine the next action
4. Present in three groups:

### Output Format

**Unblocked — ready to start now**
For each category that has a TODO task with no dependencies, show the category and the first such task. If a task is WORKING, show that instead (it's already started).

**Blocked — waiting on something**
For each category where the next TODO task depends on something else, show the category, task, and what's blocking it (another task, user action, external dependency).

**Complete**
Categories where all tasks are DONE.

End with: "Which would you like to work on?"

## Rules

- Read-only: NEVER modify `tasks.org`
- Work with org-mode format directly (headings with *, TODO/WORKING/DONE keywords)
- Show only one task per category (the next actionable one)
- Skip the Guidelines and Session sections — only process task categories
- Keep it scannable: category name + task name + blocker reason if applicable
