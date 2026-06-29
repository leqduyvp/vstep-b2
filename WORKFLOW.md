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
