# design-studio

A [Claude Code skill](https://code.claude.com/docs/en/skills) that runs product UI design like a studio engagement: binding brief → design tokens → build → adversarial crit with a real browser → design-ops handover — with **persistent aesthetic memory across projects**, so no two things you ship look alike.

## Why this exists

Agents produce competent, samey UI. The failure isn't the model — it's the harness. Tools like v0 and Lovable get their consistency from process: a brief that acts as a contract, hard numeric constraints, semantic tokens, and evaluation separated from generation. All of that is portable to a generalist agent. This skill ports it.

One piece exists nowhere else, as far as a fairly exhaustive sweep of GitHub, marketplaces, X and Reddit (July 2026) could tell: **cross-project anti-repetition memory**. Every published approach fights genericness with more prompting, and even Anthropic's own material admits the model then converges on the *next* default (Space Grotesk, anyone?). The structural fix is state: [`style-history.md`](style-history.md) records every direction the studio has shipped — typefaces, palette family, layout archetype, signature element — and each new brief must differ from every row on at least two axes. Your history is something no third-party tool can package. That file is the reason this repo isn't just another prompt pack.

## What it covers

| Component | How |
|---|---|
| Binding design brief | Written before any code, with v0-grade numeric constraints (3–5 colors, ≤2 typefaces, exactly one signature element) and a per-dimension "choice, not default" test. Vague input → three candidate directions for the human to pick. |
| Anti-repetition memory | `style-history.md`, read at intake, appended at close. The genuinely novel piece. |
| Tokens first | DTCG-syntax `tokens.json` + theme file before any component; motion (easing curves, durations) tokenized like color. |
| Craft floor | A polish layer of numbers, not adjectives: house easing set, blur-in entrances, layered hairline+ambient shadows, tactile press states, full state systems per component. |
| Separated crit | An evaluator agent (not the builder) scores the *rendered* page in a real browser against a four-criterion rubric — design quality, originality, craft, functionality — over 2–6 snapshot rounds; the best round ships, not the last. |
| Reference intake | URL → token extraction (via [dembrandt](https://github.com/dembrandt/dembrandt) or live inspection); screenshot → estimated tokens. Inspiration, not cloning. |
| Design-ops handover | Every engagement leaves `.design/`: brief, tokens, design-system.md (with extension checklist + version log), decisions.md, crit snapshots — a stranger can extend the UI without the original conversation. |
| Existing design systems | **System-locked mode**: when the repo already has a system, the system *is* the direction — tokens are consumed rather than invented, crit scores fidelity to the system instead of originality, and the anti-repetition veto is skipped (there, consistency is the deliverable). Zero-to-one and inside-a-company are both first-class. |

## Who it's for

PMs, product designers and engineers who design-and-build in the same flow with Claude Code — anyone shipping user-facing surfaces without a dedicated design team, or inside a company system they must not break. If you can run `git clone`, you can use it.

## Install

```bash
git clone https://github.com/DiegoGarcimartin/design-studio ~/.claude/skills/design-studio
```

That's it. The skill is model-invoked: Claude Code fires it when you ask for product UI. Your `style-history.md` starts empty and becomes yours — it is the point of the whole thing, so don't reset it between projects.

Optional plugs, used when present, skipped when not:

- **Mobbin MCP** (`claude mcp add mobbin --scope user --transport http https://api.mobbin.com/mcp`, paid plan) — the brief phase consults real app screens of your category before choosing a direction.
- **Are.na** — point the brief at a channel and it reads your moodboard.

## Layout

```
SKILL.md                 the pipeline (read this first)
style-history.md         cross-project memory — the novel piece
references/
  brief.md               brief rules, constraints, template
  extraction.md          reference → raw material
  craft.md               the polish layer (motion, depth, touch, states)
  crit.md                evaluator protocol + rubric
  handover.md            design-ops artifacts
```

The structure follows [writing-great-skills](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-great-skills): a short SKILL.md holding only the steps, each with a checkable completion criterion; everything else disclosed behind pointers that load per branch; positive steering over prohibitions; one source of truth per rule (the anti-repetition rule lives in `style-history.md` and nowhere else).

## References

Built on the shoulders of, and verified against:

- [Anthropic — frontend-design plugin](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design) — the two-pass plan and the "default or choice" self-review.
- [Anthropic — Prompting for frontend aesthetics](https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics) — the documented convergence biases.
- [Anthropic — Harness design for long-running agents](https://www.anthropic.com/engineering/harness-design-long-running-apps) — the separated evaluator with browser access and the four-criterion rubric.
- [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools) — v0's numeric constraints and binding design brief; Lovable's semantic-tokens-only discipline.
- [Kevin Kld — The 10 rules to ship truly polished UI](https://x.com/kvnkld/status/2066863634949779464) — the craft layer, nearly verbatim in spirit.
- [julianoczkowski/designer-skills](https://github.com/julianoczkowski/designer-skills) — the `.design/` artifact structure.
- [superdesign](https://github.com/superdesigndev/superdesign-skill) — the persistent per-project design-system.md pattern.
- [W3C DTCG Design Tokens spec (2025.10)](https://www.designtokens.org/tr/2025.10/format/) — the token format.
- [mattpocock/skills — writing-great-skills](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-great-skills) — how the docs and skill files themselves are written.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) — the bar is behavioral: every line of a skill file must change what the agent does.

## License

MIT
