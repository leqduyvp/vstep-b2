# Daily Workflow

Follow these steps every day in order.

## Step 1 — Generate the session prompts (Copilot)

1. Open Copilot Chat in VSCode.
2. Type exactly:
   > Read context.md and ROADMAP.md, then generate today's session prompts following
   > prompts/session-planner-template.md
3. Copilot outputs **two prompts**: one for Claude Sonnet and one for Gemini Live.
4. Copy each prompt separately.

## Step 2 — Run the main session (Claude Sonnet)

1. Paste the **Claude Sonnet prompt** into Claude Sonnet and complete the session.
   - This covers: Grammar → Reading → Vocabulary → Writing.
2. At the end, Claude outputs three blocks: EVALUATION, MEMORY UPDATES, CONTEXT UPDATE.
   Keep the full output visible.

## Step 3 — Run speaking and listening (Gemini Live)

1. Open Gemini Live (voice mode).
2. Use the **Gemini Live prompt** to run the Speaking section (and Listening if time allows).
3. Note any spoken errors or new vocabulary observed during the conversation.

## Step 4 — Save the evaluation

1. Create `reports/day-XX-report.md` (replace XX with today's day number).
2. Paste the **EVALUATION** block from Claude Sonnet into it.
3. Add a brief note on Gemini Live speaking/listening outcomes (errors noticed, fluency level).

## Step 5 — Update memory banks

Copy-paste each section of the **MEMORY UPDATES** block from Claude Sonnet into the
indicated file. Append to the bottom of the file. Skip any section marked "none".

- `error-log.md`
- `vocabulary-bank.md`
- `grammar-bank.md`
- `collocations.md`

## Step 6 — Update context.md (Copilot)

1. In Copilot Chat, type:
   > Update context.md using this context update:

   Then paste the **CONTEXT UPDATE** block from Claude Sonnet directly into the chat.
2. Review Copilot's edits to `context.md`. Confirm or adjust.
3. Also update `progress.md`: move the completed day to the Completed list and
   set the next day under Next Up.

## Step 7 — Commit

```bash
git add context.md progress.md reports/day-XX-report.md \
        error-log.md vocabulary-bank.md grammar-bank.md collocations.md
git commit -m "session: complete Day XX"
```

---

## Reference: Copilot command cheat sheet

| When | What to type in Copilot Chat |
|---|---|
| Morning (generate prompts) | "Read context.md and ROADMAP.md, then generate today's session prompts following prompts/session-planner-template.md" |
| After session (update context) | "Update context.md using this context update: [paste CONTEXT UPDATE block]" |

---

## Platform roles

| Platform | Covers | Notes |
|---|---|---|
| Claude Sonnet (Copilot) | Grammar, Reading, Vocabulary, Writing, Evaluation | Primary session AI |
| Gemini Live | Speaking, Listening | Voice mode; run after the Claude session |
