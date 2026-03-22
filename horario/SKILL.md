---
name: horario
description: Activa recordatorios de agua (8 vasos para 2L) y The Most Important Thing (10am, 11am, 12pm). Invoca con /horario.
---

# Horario

Al invocar este skill, crea estos 11 cron jobs de una vez usando CronCreate:

## Water Tracker (8 recordatorios, meta 2L)

8 cron jobs, uno por vaso de 250ml cada ~1.5 horas:

- `3 8 * * *` (8:03)
- `33 9 * * *` (9:33)
- `3 11 * * *` (11:03)
- `33 12 * * *` (12:33)
- `3 14 * * *` (14:03)
- `33 15 * * *` (15:33)
- `3 17 * * *` (17:03)
- `33 18 * * *` (18:33)

- **Recurring:** true (todos)
- **Prompt (los 8 igual):** "Recuérdale al usuario que beba agua (vaso de 250ml). Si contesta 'sí' o similar, anota 250ml consumidos. Lleva la cuenta acumulada del día y dile cuánto lleva bebido y cuánto le falta para los 2 litros. Si no ha bebido, simplemente recuérdale con amabilidad."

Inicializa el contador del día en 0ml. Meta diaria: 2000ml (8 x 250ml).

## The Most Important Thing (3 recordatorios matutinos)

3 cron jobs:

- `3 10 * * *` (10:03) — recurring: true
- `3 11 * * *` (11:03) — recurring: true
- `3 12 * * *` (12:03) — recurring: true
- **Prompt (los 3 igual):** "Pregúntale al usuario: '¿Estás realizando ahora mismo The Most Important Thing?' Si dice que sí, cancela los 3 recordatorios de The Most Important Thing usando CronDelete y felicítalo. Si dice que no, recuérdale con amabilidad que lo priorice."

## Al activar

1. Crea los 11 cron jobs de una sola vez
2. Confirma con una tabla de los jobs creados y sus IDs
3. Recuérdale que son de sesión (se pierden al cerrar Claude) y auto-expiran en 3 días
