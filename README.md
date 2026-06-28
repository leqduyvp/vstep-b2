# VSTEP AI Tutor

This repository is the single source of truth for a VSTEP B2 preparation course. It is designed to be read by humans and future language models alike, with all learning history, corrections, and guidance stored as plain Markdown.

## Daily Operating Loop

Use the repository in this order every day:

1. Check `progress.md` to find the latest completed day and the next day to run.
2. Read `ROADMAP.md` to get the target theme and skill focus for that day.
3. Use `prompts/session-planner-template.md` to generate the practice-session prompt.
4. Feed the generated prompt to Gemini and conduct the session.
5. Save the raw lesson in `sessions/day-XX.md` and the summary in `reports/day-XX-report.md`.
6. Update the long-term memory files and then advance `progress.md`.

## Session Sequence

When the practice session is running, keep this order:

Grammar → Reading → Vocabulary → Writing → Speaking → optional Listening → Evaluation → Memory Update

## Repository Rules

- Keep everything in Markdown.
- Prefer short, direct edits so Git diffs stay readable.
- Do not duplicate facts across files unless a file is the intended long-term record for that type of fact.
- Push every correction into one of the long-term memory files: `error-log.md`, `vocabulary-bank.md`, `grammar-bank.md`, or `examiner-notes.md`.
- Use `ROADMAP.md` as the planned path, `progress.md` as the tracker, and `prompts/session-planner-template.md` as the prompt generator.
- Use session files for raw lesson history and report files for compact summaries.

## File Roles

- `learner-profile.md` stores the stable profile of the learner.
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

## How To Use It

1. Read the learner profile and the latest progress entry.
2. Review the roadmap to pick the next study target.
3. Generate the session prompt from the planner template.
4. Save the raw interaction in `sessions/day-XX.md`.
5. Save the summary in `reports/day-XX-report.md`.
6. Update the long-term memory files with any corrected mistakes, vocabulary, or grammar notes.

## Current Course Goal

The learner is already around B2 and is now polishing output toward natural, examiner-safe English rather than learning fundamentals.