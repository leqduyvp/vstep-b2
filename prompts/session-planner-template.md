# Session Planner Template

## Purpose

This template tells Copilot how to generate two ready-to-use session prompts per day:
one for **Claude Sonnet** (text skills) and one for **Gemini Live** (voice skills).

## Copilot Instructions

Read **both** `context.md` and `ROADMAP.md` before generating anything.

**Critical: Theme and grammar focus must come from ROADMAP.md for the current day number,
not from context.md's Today's Target section.** context.md's Today's Target can fall out of
sync; ROADMAP.md is always the authoritative source for what each day covers.

Generate two prompts as separate labelled blocks.

---

### PROMPT 1 — Claude Sonnet (Grammar / Reading / Vocabulary / Writing)

#### Prompt Rules

1. Open with: "You are a strict VSTEP B2 tutor and examiner."
2. State the day number, theme, and skill targets looked up from ROADMAP.md.
3. List the active mistakes from context.md and instruct Claude to target them
   throughout the session.
4. Specify this session sequence: Grammar → Reading → Vocabulary → Writing.
5. For each skill, give a concrete task tied to the day's theme from ROADMAP.md.
6. Keep this portion to 23 minutes.
7. End the prompt with the Required Output Format instructions below — copy them
   verbatim so Claude follows them exactly.

---

### PROMPT 2 — Gemini Live (Speaking / Listening)

#### Prompt Rules

1. Open with: "You are a strict VSTEP B2 speaking examiner. This is a voice session."
2. State the day number and theme.
3. Remind the examiner to monitor and flag the active mistakes from context.md during
   the spoken responses.
4. Speaking task: one 4–6 sentence spoken response prompt tied to the day's theme.
5. Optional Listening task: describe a short scenario and ask the learner to respond
   verbally (e.g. predict advice, summarise what was said).
6. Keep the total to 7 minutes.
7. End with a brief spoken feedback prompt: ask Gemini Live to note the top 2 errors
   heard and 2 collocations the learner used well.

---

### Required Output Format for Prompt 1 (copy verbatim into the Claude Sonnet prompt)

Tell Claude to end the session with these three blocks in this exact format:

---

At the end of the session, output the following three blocks exactly as shown.
Do not skip any block. Do not change the headings.

---
## EVALUATION (paste into reports/day-XX-report.md)

### Estimated CEFR by Skill
- Grammar:
- Reading:
- Listening:
- Speaking:
- Writing:
- Vocabulary:

### Strengths
[bullet list]

### Weaknesses
[bullet list]

### Recurring Mistakes
[bullet list]

### Vocabulary Learned
[bullet list]

### Homework
[1-3 focused tasks]

### Focus for Next Day
[one sentence]

---
## MEMORY UPDATES (copy-paste into files as indicated)

### → error-log.md
[exact lines to append, or "none"]

### → vocabulary-bank.md
[exact lines to append, or "none"]

### → grammar-bank.md
[exact lines to append, or "none"]

### → collocations.md
[exact lines to append, or "none"]

---
## CONTEXT UPDATE (paste into Copilot chat to update context.md)
- Completed day: [N]
- Next day: [N+1]
- Active mistakes to add: [list or "none"]
- Active mistakes to drop: [list or "none"]
- Vocab for context.md: [single line, e.g. "habit, nutrition, well-being (Day 5)"]
- Roadmap adjustment needed: yes/no — [reason if yes, else omit]
