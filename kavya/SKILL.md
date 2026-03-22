---
name: kavya
description: Use when the user wants to save a note to the Kavya vault (Mis Notas). Triggers on "write to Kavya/Kavi", "save to Kavya/Kavi", "pon esto en Kavi", "guarda en Kavi", "hazme un md en Kavi", "sheet", "hacer un sheet".
user-invocable: true
---

# /kavya — Save note to Kavya vault

Write a markdown note directly to the Kavya vault without asking unnecessary questions.

## Vault path

Vault root: `/Users/jaganat/Kavya/`

Default: write to `Drafts/`.

### Folder override with /path

The user can specify a target folder with `/name` (approximate match). Searches both top-level folders AND all subfolders recursively:

- `/kavi /light` → finds `Light of Dharma/` and writes there
- `/kavi /voice` → finds `Voice Analisys/`
- `/kavi /radhanatha` → finds `Voice Analisys/Radhanatha Voice Investigar./`
- `/kavi /root` → writes to vault root (not Drafts)
- `/kavi` → writes to `Drafts/` (default)

**How to resolve /name:**
1. Run `find "/Users/jaganat/Kavya/" -type d` to list ALL folders and subfolders
2. Case-insensitive fuzzy match: find the folder whose name contains the /name text
3. If exactly one match → use it silently
4. If multiple matches → pick the best match (shortest name containing the text)
5. If zero matches → ask the user once, then act

## Filename format

`slugified-title-8charhex.md`

- Slugify the title: lowercase, replace non-alphanumeric with `-`, trim leading/trailing `-`, max 60 chars
- Append `-` followed by 8 random hex characters
- Example: `resumen-del-bhagavad-gita-a3f7c901.md`

## Content format

- YAML frontmatter with tags (if user specifies @tags)
- Then `# Title` as first line after frontmatter
- Then the body in markdown

### Frontmatter with tags

When the user specifies tags (e.g., `@inbox @juicio`), ALWAYS include them in the YAML frontmatter. Kavya reads tags ONLY from the frontmatter, not from the body text.

Example with tags:
```markdown
---
tags:
  - inbox
  - juicio
---
# My Title

Content here.
```

Example without tags:
```markdown
# My Title

Content here.
```

## Behavior

1. If invoked as `/kavi some title here`, use that as the title and ask for the content (or use context from the conversation)
2. If invoked as `/kavi` alone, ask: "What do you want to save?" — one question, one answer, then write
3. If the user already provided content in the conversation (e.g., "pon esto en Kavi"), use it directly — do NOT ask again
4. Write the file immediately with the Write tool — no confirmation step needed
5. Report only the filename. Done.

## Rules

- NEVER ask "are you sure?" or "shall I proceed?" — just write it
- NEVER ask for the title separately if it's obvious from the content
- ONE question maximum if something is unclear, then act
- If the content is in another language, keep it in that language
- If the user says "pon este texto en Kavi" referring to something already in the conversation, grab it and write — zero questions
- NEVER use the Edit tool on any file inside the Kavya vault — always Write the complete file
