# Session Planner Template

Use this template to generate the exact practice-session prompt for Gemini.

## Inputs

- Latest completed day from `progress.md`
- Next day to run
- Theme and skill targets from `ROADMAP.md`
- Learner strengths and weaknesses from `learner-profile.md`
- Recent corrections from `error-log.md`
- Recent vocabulary and grammar items from `vocabulary-bank.md` and `grammar-bank.md`
- Any notes from the latest `reports/day-XX-report.md`

## Planning Rules

1. Build one ready-to-paste prompt for Gemini.
2. Use the roadmap theme and the current progress state, not a random topic.
3. Reuse the learner's weak areas deliberately.
4. Keep the session examiner-style, practical, and around 30 minutes.
5. Include only the parts that still need practice for that day.
6. If a section has already been completed for the day, omit it from the generated prompt.

## Output Format

Return a single prompt with these parts:

1. Role and task instructions for Gemini.
2. The day theme and target focus.
3. The exact practice flow for the remaining sections.
4. The evaluation instructions Gemini should follow at the end.
5. A short reminder that the learner will send the summary back for repository updates.

## Prompt Shape

- Start with: "You are a strict VSTEP B2 tutor and examiner."
- State the day number and theme.
- State the skills to practice.
- Ask Gemini to conduct the session step by step.
- Ask Gemini to provide a concise evaluation at the end.
- End by telling Gemini to wait for the learner's summary to update the repository.