# Session Planner Template

## Purpose

This template tells Copilot how to generate a ready-to-paste Gemini session prompt.
Copilot reads only `context.md` as input — no other files are needed.

## Copilot Instructions

Read `context.md` and generate a complete Gemini session prompt using the rules below.

### Prompt Rules

1. Open with: "You are a strict VSTEP B2 tutor and examiner."
2. State the day number, theme, and skill targets from context.md Today's Target.
3. List the active mistakes from context.md and instruct Gemini to target them
   throughout the session.
4. Specify this session sequence: Grammar → Reading → Vocabulary → Writing →
   Speaking → optional Listening.
5. For each skill, give a concrete task tied to the day's theme.
6. Keep the session to 30 minutes.
7. End the prompt with the Required Output Format instructions below — copy them
   verbatim into the generated prompt so Gemini follows them exactly.

### Required Output Format (copy verbatim into the generated prompt)

Tell Gemini to end the session with these three blocks in this exact format:

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
