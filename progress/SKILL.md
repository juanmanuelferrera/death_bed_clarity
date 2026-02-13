---
name: progress
description: Full project overview — progress table, percentages, accomplishments, and blockers
user-invocable: true
disable-model-invocation: true
---

# /progress — Full Project Overview

Read `tasks.org` in the project root (org-mode format) and present a comprehensive progress report. **Never modify `tasks.org`.**

## Steps

1. Read `tasks.org`
2. Parse org-mode headings and TODO/WORKING/DONE keywords
3. Build a progress table and summary

### Output Format

**Progress by Category**

Show a table with columns: Category | Done | TODO | Working | Total | %

Include every top-level category (skip Guidelines and Session). Count tasks under each.

**Overall Progress**
Show total tasks done / total tasks and overall percentage.

**Key Accomplishments**
Summarize what's been completed — pull from DONE tasks and the Session > What's Done section. Keep it brief, 1 line per accomplishment.

**Current Blockers**
List anything preventing forward progress: tasks waiting on user actions, external dependencies, tasks blocking other tasks.

## Rules

- Read-only: NEVER modify `tasks.org`
- Work with org-mode format directly (headings with *, TODO/WORKING/DONE keywords)
- Use a markdown table for the progress breakdown
- Percentages should be rounded to nearest whole number
- Keep accomplishments concise — focus on outcomes, not process
