---
name: organize
description: Reorganize ALL tasks (today + future + backlog) and distribute optimally
user-invocable: true
disable-model-invocation: true
---

# /organize — Full Task Reorganization

Fetch ALL tasks from HyperFiler (MCP), redistribute everything optimally across days, respecting only @event and @bhoga rules.

## Core Principles

1. **@event stays FIXED** — never moves (real appointments/deadlines)
2. **@bhoga goes to NEXT MONDAY** — shopping list items grouped together
3. **Everything else gets redistributed** — optimally across today and future days
4. **Backlog empties completely** — all 2099-01-01 tasks get scheduled

## Steps

1. **Get current time**: Run `date +%H:%M` via Bash. If user provides time (e.g., `/organize 14:00`), use that instead. Also get today's date and calculate next Monday.

2. **Fetch ALL tasks**:
   - `mcp__hyperfiler__hf_list_tasks` with status `pending` to get everything

3. **Categorize tasks**:
   - **@event**: `isEvent: true` OR `@event` in notes → KEEP on current date, don't touch
   - **@bhoga**: `@bhoga` in notes → MOVE to next Monday
   - **Flexible**: Everything else (today, future-dated, backlog) → redistribute

4. **Update @bhoga tasks immediately**: Move all to next Monday via `mcp__hyperfiler__hf_update_task`

5. **Estimate duration using AI judgment**:
   - Very quick (5-10 min): comprobar, verificar, anotar, llamar, email, contactar
   - Quick (15-20 min): revisar enlace, poner/quitar/sacar, afeitarse, ducha
   - Medium (30-45 min): limpiar, lavar, ejercicio, comprar, cocinar, rellenar papeles, instalar
   - Long (60 min): escribir, programar, investigar, arreglar
   - Very long (90+ min): capítulo, libro, proyecto grande
   - If title contains "X min" or "X hora" → use that explicitly

6. **Score importance** (1=highest, 7=lowest):
   1. Legal/administrative (juicio, hacienda, notario, deadline, cita médica)
   2. Real-world urgent (llamar, cita, farmacia, comprar, recoger, entregar)
   3. Active projects (libro, marketing, publicar, capítulo)
   4. Digital/tech (code, fix, deploy, backup, programar)
   5. Personal care (ejercicio, ducha, ropa, yoga)
   6. Household (limpiar, barrer, ordenar, fregar)
   7. Reference/low priority (rest)

7. **Sort all flexible tasks**: By importance (lowest number first), then by shortest duration

8. **Define time slots** (in minutes from midnight):
   - 07:00-09:00 (420-540)
   - 09:30-10:00 (570-600) — after desayuno
   - 13:00-14:00 (780-840) — after TOT block
   - 14:45-19:00 (885-1140) — after cocinar
   - **06:00-07:00 is ALWAYS Programa Espiritual** — never schedule here
   - **NEVER schedule past 19:00**

9. **Fixed time rules** (apply before filling slots):
   - "Programa Espiritual" → 06:00
   - "desayuno" → 09:00
   - "TOT" (any task with TOT) → 10:00 (all TOT share 10:00-13:00 block)
   - "cocinar" or "comer" → 14:00

10. **Fill slots starting from today**:
    - For today: skip slots before current time
    - Place tasks sequentially in available slots
    - When day is full → continue to tomorrow
    - Continue until ALL tasks are placed (max 60 days)

11. **Update ALL tasks immediately** via `mcp__hyperfiler__hf_update_task`:
    - Set `due_date`
    - Set `due_time`
    - NO approval needed — execute immediately

12. **Show results**:
    - Timeline for today
    - Summary per future day
    - Confirm backlog = 0 and @bhoga on Monday

## Rules Summary

| Tag/Type | Behavior |
|----------|----------|
| `@event` or `isEvent` | NEVER moves — stays on its date |
| `@bhoga` | ALWAYS moves to next Monday |
| Everything else | Redistributed optimally |

## Additional Rules

- "comprar" tasks get `@recados` added to notes if not present
- Tasks start from 06:00 minimum, max 19:00
- Do NOT ask for approval — update immediately and show result
- Ensure "Programa Espiritual" exists for each day being scheduled

## Example Output

```
Current time: 14:30
Next Monday: 2026-02-10

## @bhoga → Moved to Monday Feb 10
- 27 shopping items moved to 2026-02-10

## @event (not touched)
- Juicio Feb 12 @ 10:00
- Cita dentista Feb 15 @ 11:00

## Today (Feb 4) - from 14:45
| Hora  | Tarea                          | Dur.   |
|-------|--------------------------------|--------|
| 14:45 | Preparar solicitud pension     | 45 min |
| 15:30 | Limpiar habitación             | 30 min |
| 16:00 | Ejercicio caminar              | 45 min |
| 16:45 | Revisar emails                 | 20 min |
| 17:05 | Fin                            |        |

## Future days
- Feb 5: 12 tasks (420 min)
- Feb 6: 11 tasks (415 min)
- Feb 7: 10 tasks (380 min)
...

## Summary
- Today: 4 tasks
- Future: 98 tasks across 9 days
- Backlog remaining: 0
- @bhoga on Monday: 27 items

Done. Refresh the app.
```
