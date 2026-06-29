# VSTEP Workflow Refactor Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refactor the repo so the daily AI study loop requires only two Copilot commands and no manual file-hunting, by adding a compact `context.md` snapshot and restructuring Gemini's output into three copy-pasteable blocks.

**Architecture:** A new `context.md` file at the repo root replaces reading 6+ files as Copilot's input. The rewritten session-planner-template instructs Copilot to read only `context.md` and instructs Gemini to output three structured blocks (EVALUATION, MEMORY UPDATES, CONTEXT UPDATE). A new `WORKFLOW.md` gives the user exact daily steps.

**Tech Stack:** Plain Markdown files only. No scripts, no tooling.

## Global Constraints

- All files must be Markdown.
- `context.md` must never exceed ~30 lines.
- Active mistakes in `context.md` are capped at 5 items.
- Gemini's three output blocks must use the exact delimiters and headings defined in this plan — Copilot and the user rely on them being consistent.
- Do not modify `learner-profile.md`, `ROADMAP.md`, `progress.md`, `error-log.md`, `vocabulary-bank.md`, `grammar-bank.md`, `collocations.md`, `examiner-notes.md`, `sessions/`, `reports/`, `prompts/tutor-system-prompt.md`, `prompts/evaluation-template.md`, or `prompts/update-memory-template.md`.

---

### Task 1: Create context.md with Day 5 state

**Files:**
- Create: `context.md`

**Interfaces:**
- Produces: `context.md` — the single input file Copilot reads to generate the session prompt

- [ ] **Step 1: Create context.md**

Write the following content exactly to `context.md` at the repo root:

```markdown
# Context

## Status
- Completed: Day 4
- Next: Day 5
- Phase: Foundation complete — moving to Health and Lifestyle

## Today's Target
- Theme: Health and lifestyle
- Grammar: Countable and uncountable nouns
- Reading: Health advice article
- Writing: Give advice with natural collocations
- Speaking: Speak about a healthy habit
- Vocab theme: Health

## Active Mistakes (top 5)
- Verb form slips (e.g. "comes with" instead of "come with")
- Subject-verb agreement (e.g. "it saves")
- Word-form slips mid-sentence (e.g. capitalising "Nowadays" mid-sentence)
- Unnatural collocations — needs deliberate practice
- Comparative modifier accuracy

## Recent Vocabulary
- convenient, reliable, user-friendly, practical (Day 4)

## Roadmap Notes
- No adjustments. On track.
```

- [ ] **Step 2: Verify context.md**

Open `context.md` and confirm:
- File has all five sections: Status, Today's Target, Active Mistakes, Recent Vocabulary, Roadmap Notes
- Active Mistakes has exactly 5 items
- Total lines are under 30
- Content matches Day 4 report in `reports/day-04-report.md` and Day 5 row in `ROADMAP.md`

- [ ] **Step 3: Commit**

```bash
git add context.md
git commit -m "add: context.md compact daily snapshot for Day 5"
```

---

### Task 2: Rewrite prompts/session-planner-template.md

**Files:**
- Modify: `prompts/session-planner-template.md`
- Delete: `prompts/daily-session-template.md`

**Interfaces:**
- Consumes: `context.md` (Task 1)
- Produces: A Copilot instruction template that outputs a complete Gemini prompt with all three structured output blocks

- [ ] **Step 1: Overwrite session-planner-template.md**

Replace the entire content of `prompts/session-planner-template.md` with:

```markdown
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
```

- [ ] **Step 2: Delete daily-session-template.md**

```bash
git rm prompts/daily-session-template.md
```

- [ ] **Step 3: Verify session-planner-template.md**

Open `prompts/session-planner-template.md` and confirm:
- Input section says `context.md` only — no other files listed
- All three output block headings are present: EVALUATION, MEMORY UPDATES, CONTEXT UPDATE
- The EVALUATION block matches the structure in `reports/day-04-report.md`
- The MEMORY UPDATES block lists all four memory files: error-log.md, vocabulary-bank.md, grammar-bank.md, collocations.md
- The CONTEXT UPDATE block has all six fields: Completed day, Next day, mistakes to add, mistakes to drop, vocab, roadmap adjustment

- [ ] **Step 4: Commit**

```bash
git add prompts/session-planner-template.md
git commit -m "refactor: session-planner-template reads only context.md, outputs three structured blocks"
```

---

### Task 3: Create WORKFLOW.md

**Files:**
- Create: `WORKFLOW.md`

**Interfaces:**
- Consumes: `context.md` (Task 1), `prompts/session-planner-template.md` (Task 2)
- Produces: `WORKFLOW.md` — the user's daily operating checklist

- [ ] **Step 1: Create WORKFLOW.md**

Write the following content exactly to `WORKFLOW.md` at the repo root:

```markdown
# Daily Workflow

Follow these steps every day in order.

## Step 1 — Generate the session prompt (Copilot)

1. Open Copilot Chat in VSCode.
2. Type exactly:
   > Read context.md and generate today's Gemini session prompt following
   > prompts/session-planner-template.md
3. Copy the full output.

## Step 2 — Run the session (Gemini)

1. Paste the prompt into Gemini Flash and run the session.
2. When Gemini finishes, it will output three blocks: EVALUATION, MEMORY UPDATES,
   and CONTEXT UPDATE. Keep the full output visible.

## Step 3 — Save the evaluation

1. Create `reports/day-XX-report.md` (replace XX with today's day number).
2. Paste the **EVALUATION** block from Gemini into it.

## Step 4 — Update memory banks

Copy-paste each section of the **MEMORY UPDATES** block from Gemini into the
indicated file. Append to the bottom of the file. Skip any section marked "none".

- `error-log.md`
- `vocabulary-bank.md`
- `grammar-bank.md`
- `collocations.md`

## Step 5 — Update context.md (Copilot)

1. In Copilot Chat, type:
   > Update context.md using this context update:

   Then paste the **CONTEXT UPDATE** block from Gemini directly into the chat.
2. Review Copilot's edits to `context.md`. Confirm or adjust.
3. Also update `progress.md`: move the completed day to the Completed list and
   set the next day under Next Up.

## Step 6 — Commit

```bash
git add context.md progress.md reports/day-XX-report.md \
        error-log.md vocabulary-bank.md grammar-bank.md collocations.md
git commit -m "session: complete Day XX"
```

---

## Reference: Copilot command cheat sheet

| When | What to type in Copilot Chat |
|---|---|
| Morning (generate prompt) | "Read context.md and generate today's Gemini session prompt following prompts/session-planner-template.md" |
| After session (update context) | "Update context.md using this context update: [paste CONTEXT UPDATE block]" |
```

- [ ] **Step 2: Verify WORKFLOW.md**

Open `WORKFLOW.md` and confirm:
- All 6 steps are present
- Step 1 Copilot command exactly matches what session-planner-template.md describes
- Step 5 Copilot command uses the CONTEXT UPDATE block (not the report file)
- The cheat sheet table at the bottom has both commands
- Commit command in Step 6 includes all affected files

- [ ] **Step 3: Commit**

```bash
git add WORKFLOW.md
git commit -m "add: WORKFLOW.md daily checklist with Copilot commands"
```

---

### Task 4: Update README.md

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: `WORKFLOW.md` (Task 3), `context.md` (Task 1)

- [ ] **Step 1: Replace the Daily Operating Loop section**

In `README.md`, replace the entire **Daily Operating Loop** section (lines 5–14) with:

```markdown
## Daily Operating Loop

See `WORKFLOW.md` for the full daily checklist with exact Copilot commands.

The short version:
1. Ask Copilot to read `context.md` and generate today's Gemini session prompt.
2. Run the session in Gemini Flash.
3. Paste Gemini's EVALUATION block into `reports/day-XX-report.md`.
4. Copy-paste Gemini's MEMORY UPDATES into the indicated files.
5. Ask Copilot to update `context.md` with Gemini's CONTEXT UPDATE block.
6. Update `progress.md` and commit.
```

- [ ] **Step 2: Update the File Roles section**

In `README.md`, add `context.md` and `WORKFLOW.md` to the File Roles list. Insert these two lines after the `learner-profile.md` line:

```markdown
- `context.md` is the compact daily snapshot Copilot reads to generate the session prompt.
- `WORKFLOW.md` is the daily operating checklist with exact Copilot commands.
```

- [ ] **Step 3: Update the Repository Rules section**

In `README.md`, replace the line:
```
- Use `ROADMAP.md` as the planned path, `progress.md` as the tracker, and `prompts/session-planner-template.md` as the prompt generator.
```
With:
```
- Use `ROADMAP.md` as the planned path, `progress.md` as the historical tracker, `context.md` as the live daily snapshot, and `prompts/session-planner-template.md` as the Copilot instruction template.
```

- [ ] **Step 4: Remove the How To Use It section**

Delete the entire **How To Use It** section (lines 45–52) — it duplicates the Daily Operating Loop and is now superseded by `WORKFLOW.md`.

- [ ] **Step 5: Verify README.md**

Open `README.md` and confirm:
- Daily Operating Loop points to `WORKFLOW.md`
- File Roles lists `context.md` and `WORKFLOW.md`
- Repository Rules mentions `context.md`
- "How To Use It" section is gone
- No remaining references to reading 6+ files to generate a prompt

- [ ] **Step 6: Commit**

```bash
git add README.md
git commit -m "update: README points to WORKFLOW.md and documents context.md role"
```

---

### Task 5: Clean up and final verification

**Files:**
- Delete: `claude-temp.md` (scratch file no longer needed)

- [ ] **Step 1: Delete the scratch file**

```bash
git rm claude-temp.md
```

- [ ] **Step 2: Full repo walkthrough**

Open each of the following and confirm it matches the spec:

| File | Check |
|---|---|
| `context.md` | Under 30 lines, 5 sections, 5 active mistakes, reflects Day 5 state |
| `WORKFLOW.md` | 6 steps, 2 Copilot commands in cheat sheet |
| `prompts/session-planner-template.md` | Input = context.md only; 3 output blocks with exact headings |
| `README.md` | Daily loop → WORKFLOW.md; File Roles includes context.md and WORKFLOW.md |
| `prompts/daily-session-template.md` | Does not exist |
| `claude-temp.md` | Does not exist |

- [ ] **Step 3: Final commit**

```bash
git add -A
git commit -m "chore: remove scratch files, complete workflow refactor"
```
