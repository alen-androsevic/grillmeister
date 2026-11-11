---
name: grillmeister
description: Grills a Claude Code skill draft. It finds every gap a cold run would trip over (vague steps, missing edge cases, weak trigger wording, no "when not") and asks the user about each one, one multiple-choice question at a time, then fixes the draft. Use when the user asks to grill, poke holes in, stress test, tighten or review a skill or SKILL.md, or right after drafting a new skill. Not for running evals or benchmarks, and not for reviewing code.
---

# Grillmeister

Finds the gaps in a skill draft and asks the user about each one, one multiple-choice question at a time, then fixes the draft. The user decides; you find the gaps, ask, and edit.

## 1. Find the draft

- The user names a skill or a path: use that.
- Otherwise, in the repository root: `dev/skill/` exists, so the skill is built with skat. Read the built `skills/<name>/`, edit the parts in `dev/skill/`, and run `skat` after each edit.
- Otherwise `skills/` holds one skill: use it. More than one, or none: ask which.

Read all of it: SKILL.md and every file it links to.

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

## 3. Grill

Ask about the gaps one at a time, riskiest first, with AskUserQuestion: one question per call, so each answer can shape the next question.

- **Question:** quote the line or name the step, then the gap in one sentence: "Step 2 says 'sort the commits'. What happens to a commit that fits two groups?"
- **Options:** two to four concrete fixes, the one you recommend first, each saying what it changes in the draft. Add "Leave it as it is" when the gap is a judgment call.
- **After each answer:** edit the draft before you ask the next question, so nothing is lost if the user stops. An answer that opens a new gap puts it in the list.
- **Stop** when the list is empty, or when the user says stop or enough.

Without AskUserQuestion (in `claude -p`, for example), ask in plain text, one question per message, with numbered options.

## 4. Report

- **Changed:** one line per answer: the gap, the fix, the file.
- **Fixed without asking:** one line each.
- **Still open:** the gaps the user skipped or didn't reach.

With skat, run `skat --check` and say whether it exits 0. Don't commit, push or publish for the user.
