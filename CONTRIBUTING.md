# Contributing

Contributions welcome. This skill's files are prompts under version control, so the bar is behavioral, not stylistic.

## What fits

- Sharper rules, with the reasoning or evidence that produced them (a source, a before/after run, a failure you hit).
- Coverage for a branch the pipeline handles poorly (file an issue describing the input and what went wrong).
- Corrections where a rule has aged — this space moves in months; a claim true at commit time may be stale.

## The bar

Skill files follow [writing-great-skills](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-great-skills). In practice:

- **Every line must change the agent's behavior.** Prose the model already obeys by default is a no-op and will be declined, however true it is.
- **One source of truth per rule.** If your change restates something that lives elsewhere (e.g. the anti-repetition rule in `style-history.md`), move it or point to it — never copy it.
- **Steer positively.** State the target behavior; keep prohibitions only where no positive phrasing exists, paired with what to do instead.
- **Steps end on checkable criteria.** "Done when the file exists and passes X" — not "when it looks good".
- **Disclose by branch.** Material only some runs need goes in `references/`, behind a pointer; `SKILL.md` stays short.

## How

Open a PR describing the behavior change your edit produces — ideally with a run (or screenshots of output) before and after. For anything structural, open an issue first.
