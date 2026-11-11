## 2. List the gaps

Read the draft as the model that will run it: cold, with nothing but the description in context when it decides to load the skill, and nothing but the skill once it has. Write down every place where that model would guess, and rank the list by how likely the guess is to make a run go wrong.

- **Trigger:** does the description say what the skill does, when to use it in the words a user would type, and when not to? Would a near-miss request load it? Would a plain request for exactly this job miss it?
- **Steps:** a step two runs would do differently. Words like "as needed", "appropriately" or "handle errors" with no how.
- **Inputs:** what happens when an input is missing, empty, huge, or not what the skill expects.
- **Output:** the shape, and where it goes.
- **Stops:** when the skill stops, asks or hands over. Anything that sends, deletes, pays, pushes or publishes without asking first.
- **Scope:** two jobs in one skill.
- **Sources:** text copied from docs that will go stale, where a pointer would do. A step that must come out the same every time, without a script.
- **Size:** SKILL.md over 500 lines; a reference file with no line saying when to read it.

Fix what needs no decision from the user (a typo, a broken link, a missing heading) right away, and note it for the report. Keep at most 10 gaps for questions.
