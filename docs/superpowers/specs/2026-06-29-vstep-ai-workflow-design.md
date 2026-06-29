# VSTEP B2 AI Workflow Design

**Date:** 2026-06-29
**Status:** Approved

## Goal

Refactor the repo so the daily AI-assisted English practice workflow is reliable with a small-context model (GitHub Copilot in VSCode) and requires minimal manual file-hunting.

## Daily Loop

```
[Copilot reads context.md]
        ↓
  Outputs Gemini session prompt
        ↓
[User pastes into Gemini → runs 30-min session]
        ↓
  Gemini outputs three structured blocks:
    1. EVALUATION       → paste into reports/day-XX-report.md
    2. MEMORY UPDATES   → copy-paste into indicated files
    3. CONTEXT UPDATE   → tells Copilot what changed
        ↓
[Copilot updates context.md from the new report]
        ↓
      Done
```

Two Copilot commands per day. No manual file-hunting.

## context.md

A new file at the repo root. This is the single input Copilot reads to generate the session prompt. It is always up to date and never exceeds ~30 lines.

### Structure

```markdown
# Context

## Status
- Completed: Day N
- Next: Day N+1
- Phase: [current phase label]

## Today's Target
- Theme: [from ROADMAP]
- Grammar: [from ROADMAP]
- Reading: [from ROADMAP]
- Writing: [from ROADMAP]
- Speaking: [from ROADMAP]
- Vocab theme: [from ROADMAP]

## Active Mistakes (top 5)
- [mistake 1]
- [mistake 2]
- [mistake 3]
- [mistake 4]
- [mistake 5]

## Recent Vocabulary
- [word/phrase (Day N)]

## Roadmap Notes
- [any deviation from the 28-day plan, or "No adjustments. On track."]
```

### Rules

- Active mistakes capped at 5. Drop resolved ones, add new ones each session.
- Recent vocabulary shows last session only. Full history stays in `vocabulary-bank.md`.
- Roadmap notes only appear when something deviates from the plan.
- Copilot updates this file after each session using the CONTEXT UPDATE block from Gemini.

## Gemini Session Prompt Output Format

The session prompt instructs Gemini to end with three clearly delimited blocks:

### Block 1: EVALUATION
Matches the existing `reports/` format exactly. User pastes directly into `reports/day-XX-report.md`.

```
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
...

### Weaknesses
...

### Recurring Mistakes
...

### Vocabulary Learned
...

### Homework
...

### Focus for Next Day
...
```

### Block 2: MEMORY UPDATES
Append-only lines for each memory bank file. User copies each section to the bottom of the indicated file.

```
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
```

### Block 3: CONTEXT UPDATE
Tells Copilot exactly what to change in `context.md`. Makes the Copilot update command fast and reliable.

```
---
## CONTEXT UPDATE (for Copilot to update context.md)
- Completed day: N
- Next day: N+1
- Active mistakes to add: [list or "none"]
- Active mistakes to drop: [list or "none"]
- Vocab for context.md: [single line summary of session vocab]
- Roadmap adjustment needed: yes/no — [reason if yes]
```

## WORKFLOW.md

A new file at the repo root with the daily checklist and exact Copilot commands.

```markdown
# Daily Workflow

## Morning: Generate session prompt
1. Open Copilot Chat in VSCode
2. Type: "Read context.md and generate today's Gemini session prompt"
3. Copy the output → paste into Gemini → run the session

## After session: Save the evaluation
1. Create reports/day-XX-report.md
2. Paste the EVALUATION block from Gemini into it
3. Copy-paste each MEMORY UPDATES block into the indicated file (append to bottom)

## After session: Update context
1. In Copilot Chat, type: "Update context.md using this context update:" then paste
   the CONTEXT UPDATE block from Gemini directly into the chat
2. Review Copilot's edits to context.md — confirm or adjust
3. Commit everything
```

Note: The CONTEXT UPDATE block goes into the Copilot chat, not into any file. Only the
EVALUATION block goes into the report file.

## File Changes

| Action | File | Reason |
|---|---|---|
| Add | `context.md` | Compact daily snapshot — Copilot's single input |
| Add | `WORKFLOW.md` | Daily checklist with exact Copilot commands |
| Rewrite | `prompts/session-planner-template.md` | Input is now only `context.md`; output includes all 3 structured blocks |
| Update | `README.md` | Point daily loop to `WORKFLOW.md`; simplify |
| Delete | `prompts/daily-session-template.md` | Merged into session-planner-template |
| Keep | `learner-profile.md` | Stable reference, rarely changes |
| Keep | `ROADMAP.md` | Source of truth for 28-day plan |
| Keep | `progress.md` | Historical completion tracker |
| Keep | `error-log.md`, `vocabulary-bank.md`, `grammar-bank.md`, `collocations.md`, `examiner-notes.md` | Memory banks, updated via MEMORY UPDATE blocks |
| Keep | `sessions/`, `reports/` | Unchanged role |
| Keep | `prompts/tutor-system-prompt.md`, `prompts/evaluation-template.md` | Reference material |
| Keep | `prompts/update-memory-template.md` | Reference material |

## Design Constraints

- Copilot (GPT mini or better via VSCode extension) reads only `context.md` to generate the prompt.
- Gemini Flash runs the session and outputs the structured blocks.
- No custom scripts or tooling — pure markdown and copy-paste.
- The repo must remain usable by a small model without forgetting key context.
