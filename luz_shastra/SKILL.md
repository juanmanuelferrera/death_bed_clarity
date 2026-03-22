---
name: luz_shastra
description: Use when processing questions from Gaudiya Vaishnava classes or study groups to generate analyzed answers and a videoblog script for A la Luz del Shastra. Triggers on "luz del shastra", "clase grabada", "preguntas de clase", "script de episodio", "A la Luz del Shastra", or when given philosophical questions that need shastric answers and a video/podcast script.
---

# A la Luz del Shastra — Question Processor

## The Show

**A la Luz del Shastra** (shastra.bhaktiyoga.es) is a weekly Spanish-language videoblog by Jagannatha Mishra Dasa. Filosofía védica sin censura. Every claim grounded in Bhagavad-gita, Srimad Bhagavatam, Caitanya-caritamrta, and Prabhupada's writings. Addresses questions that people actually have and nobody answers — about philosophy, life, institutions, applied Krishna consciousness. No institutional filter. 40+ years of bhakti yoga practice behind it.

**Categories:** Filosofía aplicada, Vida práctica, Crítica ISKCON, Observatorio brahmínico.

**Format:** ~20 min videoblog episodes on YouTube. Questions come from classes, study groups, or listener submissions via the website.

## What This Skill Does

Takes raw questions and produces:
1. Verified philosophical answers (for study/reference)
2. A ready-to-record videoblog script

## Input

Questions from a class, study group, or listener. Can be:
- Raw text pasted directly
- A file path to read
- A list of questions with context (verse being studied, topic)

If no questions provided, ask: "Pega las preguntas o dame la ruta del archivo."

## Pipeline

```dot
digraph pipeline {
  rankdir=LR;
  "Questions" -> "Siddhanta Analysis";
  "Siddhanta Analysis" -> "Verse Verification";
  "Verse Verification" -> "Draft Answers";
  "Draft Answers" -> "Videoblog Script";
  "Videoblog Script" -> "Clipboard";
}
```

### Phase 1: Siddhanta Analysis

For each question, determine:

1. **What is really being asked?** — Strip the surface phrasing. Find the philosophical core. A question about "feeling young inside" is really about the distinction between atma and deha.
2. **Which category does it touch?** — Tattva (ontology), Sadhana (practice), Pramana (epistemology), Achara (conduct), Rasa-tattva (devotional aesthetics), Historical accuracy.
3. **What is the correct siddhantic answer?** — Based exclusively on the parampara: Six Goswamis, Vishvanatha Chakravarti, Baladeva Vidyabhushana, Bhaktivinoda, Bhaktisiddhanta, Prabhupada.
4. **What common errors could arise here?** — Mayavada tendencies, sahajiya errors, mixing traditions, imprecise terminology.
5. **What shastra supports the answer?** — Identify candidate verses (BG, SB, CC, NOI, BRS, Upanishads). DO NOT cite yet — just note them for Phase 2.

Output: Internal analysis (not shown to user). Feeds Phase 2 and 3.

### Phase 2: Verse Verification (MANDATORY)

Before using ANY verse reference, verify via WebSearch.

**Search targets:** vedabase.io, prabhupadabooks.com, vaniquotes.org

**Confirm for each verse:**
- Correct book and numbering (is it really BG 2.13 and not 2.14?)
- Correct content (does it actually say what you think?)
- Correct attribution (not a Bhagavatam verse cited as Gita)

**If a verse doesn't check out:** find the correct one, or paraphrase without number.

**NEVER guess a verse number. NEVER put a paraphrase in quotation marks.**

### Phase 3: Draft Answers

Write a complete answer for each question. These are the "raw material" — thorough, with references, suitable for study. Copy all answers to clipboard when done.

- Each answer: 150-300 words
- Verified shastra references woven naturally
- Distinguish established siddhanta from debated topics
- Sanskrit terms with brief inline definitions on first use
- Tone: knowledgeable but not pedantic

### Phase 4: Videoblog Script

Transform answers into a single ~20 min videoblog episode.

**Structure:**
```
INTRO (~1:30-2:00)
  - Brief context: what verse or topic the class was on
  - Set up the questions naturally — don't list them, just ease in
  - Paraphrase the verse content (never "cite" it formally)

QUESTION 1 (~3-4 min)
QUESTION 2 (~3-4 min)
...
QUESTION N (~3-4 min)

CIERRE (~1:30-2:00)
  - Thread all questions together (one shared theme)
  - "La frase de la semana es..."
  - Brief sign-off
```

**Timing:** ~130 words/min in spoken Spanish. Total: ~2,400-2,700 words for 20 min.

## Voice & Tone

The show sounds like a guy with 40 years of practice thinking out loud with you. Not a lecture. Not a sermon. Not a motivational talk. A conversation where one person happens to know the shastra well and isn't afraid to say what he thinks.

### What it sounds like:

- **Direct.** Goes straight to the point. "Sí. Y esto es algo que en el fondo todos sabemos pero no le damos importancia."
- **Grounded in real life.** The grandmother who says "estas no son mis manos". The guy with three Wikipedia facts playing cosmologist. A rotten apple in the fridge. The monkey hugging its baby. Specific beats abstract, always.
- **Honest.** Calls things by their name. If something is wrong, says it's wrong. If something is debatable, says it's debatable. "Eso ya es decisión de cada uno, pero al menos hay que hacerse la pregunta."
- **Funny when it comes naturally.** "Brillante — literalmente" about the sun. "Y ya estás dando una clase de cosmología con tres datos de Wikipedia." Never forced.
- **Verses woven in, not presented.** "Krishna explica que el alma va pasando por las distintas etapas..." — NOT "En BG 2.13 Krishna dice: dehino 'smin yathā dehe..." The shastra flows inside the conversation, not on top of it.
- **Trusts the listener.** Says it once, says it well, moves on. No recaps. No "como dijimos antes". No explaining why the example you just gave was a good example.
- **Lets uncomfortable questions land.** "Si el mono siente, y lo metemos en una jaula... eso ya es decisión de cada uno." Present the logic. Don't force the conclusion.

### What it does NOT sound like:

- **No rhetorical filler.** Kill these on sight: "Fíjense en algo", "Piensen en eso un momento", "Qué linda pregunta", "Me encanta esta pregunta", "Esto es muy interesante". Go straight to the content.
- **No bridge paragraphs.** Don't announce what you're about to say. Just say it. "Esto nos lleva a..." — no. Just go there.
- **No preacher cadence.** Statement → rhetorical question → statement → rhetorical question → dramatic pause → revelation. That's a TED talk. Cut it.
- **No charlatán energy.** "Esto cambia absolutamente todo", "Esto es radical", "Prepárense porque..." — once in an episode, maybe. Twice, no.
- **No Sanskrit walls.** One term per idea, max. Define it inline, three words. Don't stack "tatastha-shakti", "cit-tattva" and "karanāpāṭava" in the same breath.
- **No motivational poster closings.** "Y eso debería cambiar radicalmente la forma en que vivimos" — too much. Prefer dry and open: "Pero al menos hay que hacerse la pregunta."

### Verse Reference Style in Script

| Context | How to say it |
|---------|---------------|
| Teaching a concept | "Krishna explica que..." / "En el Gītā se dice que..." |
| Supporting a point | "Prabhupāda lo compara con..." / "La tradición védica describe..." |
| Technical term | "Los ṣaḍ-vikāra — las seis transformaciones de la materia —" |
| Only when really needed | "En el segundo capítulo, verso trece..." (spoken, not coded) |
| NEVER in script | "BG 2.13 states:" / any academic citation format |

### The "Frase de la Semana"

- One sentence that distills the whole episode
- Quotable — sticky-note material
- Comes FROM the content, not imposed on it
- Presented simply: "La frase de la semana: [frase]"
- Then one short paragraph applying it to everyday life
- Example: "Yo no estoy cambiando. Estoy observando el cambio."

## After Script Generation

1. **Copy script to clipboard** via `pbcopy`
2. **Save** to `~/.emacs.d/git_projects/a-la-luz-del-shastra/scripts/` as `claseNN-[verse-ref]-script.md`
3. Confirm: "Script copiado al clipboard y guardado en [path]."

## Common Mistakes

- **Answering from academia instead of parampara.** The standard is acharya-vani, not comparative religion.
- **Listing verses instead of teaching.** This is a videoblog, not a shastra class. Verses support the conversation, they don't structure it.
- **Making every question equally long.** Some are deeper. Give more time to the ones that need it. A simple question gets a simple answer.
- **Forgetting the listener might be new.** Define terms. Give context. Don't assume they know what "tatastha-shakti" means.
- **Over-explaining.** If the example already made the point, move on. Don't explain why your example was good.
- **Sounding institutional.** This show has no institutional filter. If a question touches ISKCON politics or uncomfortable topics, address it directly with shastra. Don't dodge.
