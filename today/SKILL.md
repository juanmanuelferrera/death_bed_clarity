---
name: today
description: Show today's HyperFiler tasks organized by time, plus tasks.org status
user-invocable: true
disable-model-invocation: true
---

# /today — Daily Overview

Show a complete view of today combining HyperFiler tasks and tasks.org status.

## Steps

1. **Fetch HyperFiler tasks**: Use `mcp__hyperfiler__hf_list_tasks` with today's date
2. **Show today's schedule** as a timeline table:
   - Sort by time
   - Mark events with [EVT]
   - Mark completed tasks with [DONE]
   - Show @compra tasks separately if any exist for today
3. **Read `tasks.org`** and show:
   - Any WORKING tasks (in progress)
   - Pending User Actions from Session section
4. **Summary stats**: total tasks, completed, remaining, next upcoming task

## Output Format

```
## Today: 2026-02-01 (Saturday)

### Schedule
| Hora  | Task                              | Status  |
|-------|-----------------------------------|---------|
| 06:00 | Programa Espiritual               | pending |
| 09:00 | desayuno hipoglucemico            | pending |
| 10:00 | TOT Revisar capitulos             | pending |
| 14:00 | cocinar verduras                  | done    |

### In Progress (tasks.org)
- [WORKING] Some task from tasks.org

### Stats
- 12 tasks total, 3 completed, 9 remaining
- Next: 14:45 — ejercicios
```

## Rules

- Read-only: do NOT modify any tasks
- Show times in 24h format
- If no tasks for today, say so and show tomorrow's count
- Keep it concise
