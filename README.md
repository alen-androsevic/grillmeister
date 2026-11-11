# grillmeister

A Claude Code skill that grills a skill draft. It reads the draft as the model that will run it, cold, and lists every place where that model would have to guess: vague steps, missing edge cases, weak trigger wording, no "when not". Then it asks you about each gap, one multiple-choice question at a time with its recommendation first, and fixes the draft after every answer.

## Install

From the [alen-androsevic marketplace](https://github.com/alen-androsevic/skills):

```bash
claude plugin marketplace add alen-androsevic/skills
claude plugin install grillmeister@alen-androsevic
```

Then ask Claude Code to grill a skill, for example "grill skills/release-notes". The [skat](https://github.com/alen-androsevic/skat) plugin's `new-skill` runs it on every new draft.

## Working on the skill

`skills/grillmeister/` is built from the parts in `dev/skill/` by [skat](https://github.com/alen-androsevic/skat); don't edit it by hand.

```bash
cargo install --git https://github.com/alen-androsevic/skat
skat            # build skills/grillmeister/ from dev/skill/
skat --check    # exit 1 if skills/grillmeister/ is out of date
```
