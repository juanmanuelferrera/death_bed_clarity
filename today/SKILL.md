---
name: today
description: Show today's tasks from Kavya (today + week combined), fill capacity based on remaining time
user-invocable: true
disable-model-invocation: true
---

# /today — Daily Task Overview (Kavya)

Combines tasks tagged `today` and `week`, fills capacity based on remaining hours, rest goes to backlog.

## Quick Implementation

```bash
python3 << 'PYEOF'
import subprocess
import math
import re
from datetime import datetime
from pathlib import Path
import html as html_lib

# === PATHS ===
VAULT = "/Users/jaganat/Library/CloudStorage/Dropbox/Kavya"
HTML_OUT = "/Users/jaganat/Library/Mobile Documents/com~apple~CloudDocs/today-tasks.html"

DIRS = [
    f"{VAULT}/Miscelanea",
    f"{VAULT}/Kavya app",
    f"{VAULT}/Personal",
    f"{VAULT}/Juicio",
    f"{VAULT}/Inbox"
]

# === CAPACITY ===
now = datetime.now()
current_hour = now.hour + now.minute / 60
remaining_hours = max(0, 22 - current_hour)
capacity = math.floor(remaining_hours * 0.8)

# === FIND TASKS ===
def find_tagged_files(tag):
    files = []
    for d in DIRS:
        try:
            result = subprocess.run(
                ["grep", "-l", f"^  - {tag}$", *list(Path(d).glob("*.md"))],
                capture_output=True, text=True
            )
            files.extend(result.stdout.strip().split("\n"))
        except:
            pass
    return [f for f in files if f]

def get_title_from_file(path):
    try:
        with open(path, 'r', encoding='utf-8') as f:
            content = f.read()
        match = re.search(r'^#\s+(.+)$', content, re.MULTILINE)
        if match:
            return match.group(1).strip()
        name = Path(path).stem
        name = re.sub(r'-[a-f0-9]{8}$', '', name)
        return name.replace('-', ' ').strip()
    except:
        return Path(path).stem

def is_quick_task(title):
    """Returns True if task seems quick (< 10 min) based on text analysis"""
    t = title.lower()
    quick_verbs = ("comprar ", "llamar", "enviar", "responder", "revisar", "ver ",
                   "mirar", "poner", "quitar", "borrar", "añadir", "abrir", "cerrar",
                   "leer ", "checar", "chequear", "mandar", "sacar", "guardar",
                   "correr ", "hacer ", "lavar", "seguir")
    quick_indicators = ("rápido", "rapido", "quick", "5 min", "10 min", "5min", "10min")
    long_indicators = ("investigar", "buscar", "arreglar", "renovar", "escribir",
                       "crear", "desarrollar", "implementar", "analizar", "estudiar",
                       "https://", "http://", ".com", ".es", ".org")

    for ind in long_indicators:
        if ind in t: return False
    for ind in quick_indicators:
        if ind in t: return True
    for verb in quick_verbs:
        if t.startswith(verb): return True
    if len(title) < 50 and not any(ind in t for ind in long_indicators):
        return True
    return False

def priority_score(title):
    """Lower = more important"""
    t = title.lower()
    if "urgente" in t: return 0
    if "importante" in t: return 1
    if t.startswith(("pagar", "renovar", "arreglar")): return 2
    if t.startswith(("llamar", "responder", "enviar")): return 3
    if t.startswith(("comprar", "hacer", "revisar")): return 4
    return 5

def sort_key(task):
    """Sort: quick tasks first, then by importance"""
    title = task["title"]
    quick = 0 if is_quick_task(title) else 1
    importance = priority_score(title)
    return (quick, importance, title.lower())

# Combine today + week (deduplicated)
today_files = set(find_tagged_files("today"))
week_files = set(find_tagged_files("week"))
all_files = today_files | week_files

all_tasks = [{"title": get_title_from_file(f), "path": f} for f in all_files]
all_tasks.sort(key=sort_key)

# Split by capacity
hoy_tasks = all_tasks[:capacity]
backlog = all_tasks[capacity:]

# === TERMINAL OUTPUT ===
day_name = now.strftime("%A")
date_str = now.strftime("%Y-%m-%d")
time_str = now.strftime("%H:%M")

print(f"\n## Today: {date_str} ({day_name}) — {time_str}")
print(f"## {remaining_hours:.1f}h restantes | Capacidad: {capacity} tareas\n")

print(f"### Hoy ({len(hoy_tasks)})")
for i, t in enumerate(hoy_tasks, 1):
    print(f"{i}. {t['title']}")
print()

if backlog:
    print(f"### Backlog ({len(backlog)})")
    for t in backlog[:5]:
        print(f"- {t['title']}")
    if len(backlog) > 5:
        print(f"- [+{len(backlog) - 5} más]")
    print()

print(f"---\n{len(hoy_tasks)} tareas para hoy | {len(backlog)} en backlog")

# === HTML ===
html = f'''<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hoy</title>
  <style>
    * {{ box-sizing: border-box; margin: 0; padding: 0; }}
    body {{ font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
           background: #f5f5f7; padding: 20px; max-width: 600px; margin: 0 auto; }}
    h1 {{ font-size: 1.5rem; margin-bottom: 5px; }}
    .meta {{ color: #86868b; font-size: 0.9rem; margin-bottom: 20px; }}
    .section {{ background: white; border-radius: 12px; padding: 16px; margin-bottom: 16px;
               box-shadow: 0 1px 3px rgba(0,0,0,0.1); }}
    .section-title {{ font-size: 0.8rem; font-weight: 600; text-transform: uppercase;
                     letter-spacing: 0.5px; margin-bottom: 12px; color: #ff3b30; }}
    .section-title.backlog {{ color: #86868b; cursor: pointer; }}
    .task {{ display: flex; align-items: flex-start; padding: 8px 0; border-bottom: 1px solid #f0f0f0; }}
    .task:last-child {{ border-bottom: none; }}
    .checkbox {{ width: 22px; height: 22px; border: 2px solid #d1d1d6; border-radius: 50%;
                margin-right: 12px; flex-shrink: 0; cursor: pointer; -webkit-tap-highlight-color: transparent; }}
    .checkbox.checked {{ background: #34c759; border-color: #34c759; }}
    .section-title.backlog {{ -webkit-tap-highlight-color: transparent; }}
    .task-title {{ flex: 1; line-height: 1.4; }}
    .task.done .task-title {{ text-decoration: line-through; color: #86868b; }}
    .backlog-content {{ display: none; }}
    .backlog-content.show {{ display: block; }}
    .summary {{ text-align: center; color: #86868b; font-size: 0.9rem; padding: 10px; }}
  </style>
</head>
<body>
  <h1>Hoy</h1>
  <div class="meta">{date_str} ({day_name}) — {remaining_hours:.1f}h restantes</div>
  <div class="section">
    <div class="section-title">Hoy ({len(hoy_tasks)})</div>
'''

for i, t in enumerate(hoy_tasks):
    title_escaped = html_lib.escape(t["title"])
    html += f'''<div class="task" data-id="hoy-{i}">
      <div class="checkbox"></div>
      <div class="task-title">{title_escaped}</div>
    </div>'''

html += '</div>'

if backlog:
    html += f'''<div class="section">
      <div class="section-title backlog">Backlog ({len(backlog)}) ▼</div>
      <div class="backlog-content" id="backlog">'''
    for i, t in enumerate(backlog):
        title_escaped = html_lib.escape(t["title"])
        html += f'''<div class="task" data-id="backlog-{i}">
          <div class="checkbox"></div>
          <div class="task-title">{title_escaped}</div>
        </div>'''
    html += '</div></div>'

html += f'''
  <div class="summary">{len(hoy_tasks)} tareas para hoy | {len(backlog)} en backlog</div>
  <script>
    const done = JSON.parse(localStorage.getItem("todayDone") || "{{}}");
    document.querySelectorAll(".task").forEach(t => {{
      if (done[t.dataset.id]) {{
        t.classList.add("done");
        t.querySelector(".checkbox").classList.add("checked");
      }}
      t.addEventListener("click", function(e) {{
        e.preventDefault();
        const id = this.dataset.id;
        this.classList.toggle("done");
        this.querySelector(".checkbox").classList.toggle("checked");
        done[id] = this.classList.contains("done");
        localStorage.setItem("todayDone", JSON.stringify(done));
      }});
    }});
    document.querySelectorAll(".section-title.backlog").forEach(el => {{
      el.addEventListener("click", function(e) {{
        e.preventDefault();
        document.getElementById("backlog").classList.toggle("show");
      }});
    }});
  </script>
</body>
</html>'''

Path(HTML_OUT).write_text(html, encoding='utf-8')
print(f"\nHTML: {HTML_OUT}")
PYEOF

open "/Users/jaganat/Library/Mobile Documents/com~apple~CloudDocs/today-tasks.html"
```

## Logic

1. **Find tasks**: grep for `^  - today$` and `^  - week$` in YAML frontmatter
2. **Combine**: Merge both sets (deduplicated)
3. **Sort by priority**: urgente → llamar/comprar → hacer/arreglar/renovar → investigar/leer/buscar → rest
4. **Fill capacity**: `floor((22 - current_hour) * 0.8)` tasks
5. **Rest → Backlog**

## Directories

- Miscelanea
- Kavya app
- Personal
- Juicio
- Inbox

## Output

- Terminal: task list
- HTML: `/Users/jaganat/Library/Mobile Documents/com~apple~CloudDocs/today-tasks.html`
