# VSTEP AI Tutor

This repository is the single source of truth for a VSTEP B2 preparation course. It is designed to be read by humans and future language models alike, with all learning history, corrections, and guidance stored as plain Markdown.

## Daily Operating Loop

See `WORKFLOW.md` for the full daily checklist with exact Copilot commands.

The short version:
1. Ask Copilot to read `context.md` and generate today's Gemini session prompt.
2. Run the session in Gemini Flash.
3. Paste Gemini's EVALUATION block into `reports/day-XX-report.md`.
4. Copy-paste Gemini's MEMORY UPDATES into the indicated files.
5. Ask Copilot to update `context.md` with Gemini's CONTEXT UPDATE block.
6. Update `progress.md` and commit.

## Session Sequence

When the practice session is running, keep this order:

Grammar → Reading → Vocabulary → Writing → Speaking → optional Listening → Evaluation → Memory Update

## Repository Rules

- Keep everything in Markdown.
- Prefer short, direct edits so Git diffs stay readable.
- Do not duplicate facts across files unless a file is the intended long-term record for that type of fact.
- Push every correction into one of the long-term memory files: `error-log.md`, `vocabulary-bank.md`, `grammar-bank.md`, or `examiner-notes.md`.
- Use `ROADMAP.md` as the planned path, `progress.md` as the historical tracker, `context.md` as the live daily snapshot, and `prompts/session-planner-template.md` as the Copilot instruction template.
- Use session files for raw lesson history and report files for compact summaries.

## File Roles

- `learner-profile.md` stores the stable profile of the learner.
- `context.md` is the compact daily snapshot Copilot reads to generate the session prompt.
- `WORKFLOW.md` is the daily operating checklist with exact Copilot commands.
- `progress.md` tracks study completion and the current focus.
- `ROADMAP.md` defines the 28-day study path.
- `error-log.md` records recurring mistakes and their corrections.
- `vocabulary-bank.md` stores learned vocabulary by theme.
- `grammar-bank.md` records grammar topics that have already appeared.
- `collocations.md` keeps high-value multiword expressions.
- `examiner-notes.md` contains examiner-style observations and scoring trends.
- `sessions/` stores detailed day-by-day lesson records.
- `reports/` stores structured summaries after each completed day.
- `prompts/` stores reusable templates for future LLM sessions.

## Current Course Goal

The learner is already around B2 and is now polishing output toward natural, examiner-safe English rather than learning fundamentals.