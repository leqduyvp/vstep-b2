I'm preparing for an English exam to get a VSTEP certification of at least B2 level in four skills: reading, writing, speaking and listening.

I want to setup a personal AI workflow for helping me learn and practice english daily. My proposed setup is:
1. Using this repo as a tracker and planner. 
2. It will plan the roadmap, and might update the roadmap according to the progress. The roadmap will contains the daily practice session.
3. Every day I will use a prompt or a command to generate a daily 30-min practice session prompt that I can feed to an external model - like Gemini to conduct the practice session, and then bring the evaluation back to this repo for tracking. The prompt should clearly define the goal of the current session.
4. This repo will track the evaluation to update the road map if needed, and also use it as the input for the prompt generation tommorow

This setup is to keep the context of this repo small enough so the model working on its data should not forget things or hallucinate
Some technology limit:
- I might have to use this repo with a small model like GPT mini, and practice session with gemini flash only

Review this setup and give suggestion if needed. After that, plan and execute the refactor to have the repo ready