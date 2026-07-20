# design-studio

A [Claude Code skill](https://code.claude.com/docs/en/skills) that runs product UI design like a studio engagement: binding brief → design tokens → build → adversarial crit with a real browser → design-ops handover — with **persistent aesthetic memory across projects**, so no two things you ship look alike.

## Why this exists

AI is bad at design for five specific, well-documented reasons — Phil Morton's ["Why is AI bad at design?"](https://www.philmorton.co/why-is-ai-bad-at-design/) is the clearest public statement of them. This skill exists to attack each one structurally instead of with more prompting. The failure isn't the model — it's the harness: tools like v0 and Lovable get their quality from process (a binding brief, hard numeric constraints, semantic tokens, evaluation separated from generation), and all of that is portable to a generalist agent.

| Why AI design fails | What this skill does about it |
|---|---|
| **Pull toward the average** — models gravitate to the middle of their training distribution; every output looks like every other AI output | The core of the skill: a taken-directions veto ([`style-history.md`](style-history.md)) including never-expiring rows for the known AI-default looks; a per-dimension "choice, not default" test in the brief; one mandatory aesthetic risk per engagement |
| **Repetition across projects** — banned from one default, the model converges on the *next* one (Anthropic documents this) | The genuinely novel piece: **cross-project memory**. Every shipped direction becomes a permanent row; each new brief must differ from every row on at least two of four axes. Your history is something no third-party tool can package |
| **Visual blindness** — the model writes interfaces it never sees, "drawing with its eyes closed" | Nothing ships unrendered: the crit phase screenshots the real page in a real browser at three widths, and the evaluator judges pixels, not code |
| **No design compiler** — code has tests; design quality has no objective grader | A four-criterion rubric with measured (not eyeballed) findings is the best available proxy — and the skill states its limit openly: the evaluator can only certify "ready for the director"; **the human verdict outranks every score** |
| **Same model, same blind spots** — an evaluator sharing the generator's weights shares its missing taste (it has scored AI-default palettes as "original") | Mitigated, not solved: separated evaluator agent, adversarial mandate, stranger-test score cap — and the human-director gate above as the honest backstop |
| **Screens without reasoning** — training data shows *what* interfaces look like, never *why* they work | Rules carry their why: craft recipes as numbers with rationale, [field notes measured live](references/craft.md) from Vercel/Supabase/Resend computed styles, and a per-project `decisions.md` that records the reason behind every choice |

Two notes on scope. The cross-project memory row is — as far as a fairly exhaustive July-2026 sweep of GitHub, skill marketplaces, X and Reddit could tell — this skill's original contribution; nothing published covers it. And this skill deliberately does *not* adopt the "use AI only for parts of design" conclusion: the whole pipeline runs, with the human at exactly two gates — picking the direction, and the closing verdict. Several of the skill's mechanisms (the binding brief with numeric constraints, the measured craft floor, design-ops artifacts, system-locked mode for existing design systems) address failures no diagnosis article names at all.

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

**Personal** (all your projects, one shared aesthetic memory):

```bash
git clone https://github.com/DiegoGarcimartin/design-studio ~/.claude/skills/design-studio
```

**Team / company** (one repo, everyone gets it via git):

```bash
git clone https://github.com/DiegoGarcimartin/design-studio your-repo/.claude/skills/design-studio
rm -rf your-repo/.claude/skills/design-studio/.git   # vendor it; your repo owns the copy
```

Commit it and every teammate's Claude Code picks it up — no per-person setup.

That's it either way: the skill is model-invoked, so Claude Code fires it when someone asks for product UI. In personal installs, `style-history.md` starts empty and becomes yours — don't reset it between projects; it is the point of the whole thing.

### Plugging in your existing design system

Nothing to configure. If your repo already carries a token/theme layer (CSS variables, Tailwind config, a `tokens.json`, a design-system doc), the skill detects it at intake — or you say "use our design system" — and runs **system-locked**: your system becomes the constraint set, new values enter only through your conventions, and the crit loop scores *fidelity to your system* instead of originality. If your tokens live somewhere unusual, mention the path once; the brief records it and later phases cite the brief.

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
- [OneRedOak/claude-code-workflows](https://github.com/OneRedOak/claude-code-workflows/tree/main/design-review) — the live-environment-first review discipline and the three-viewport check.
- [Dyad](https://github.com/dyad-sh/dyad) and [Onlook](https://github.com/onlook-dev/onlook) — open-source reference implementations of the v0/Lovable class; fixed stack and live-preview-to-code mapping, respectively.
- [W3C DTCG Design Tokens spec (2025.10)](https://www.designtokens.org/tr/2025.10/format/) — the token format; [Style Dictionary](https://styledictionary.com/) and [Terrazzo](https://terrazzo.app/) turn it into platform outputs headlessly.
- [Design Arena](https://www.designarena.ai/) — the human-preference benchmark where agent-built UI is actually judged; useful for calibrating expectations.
- [mattpocock/skills — writing-great-skills](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-great-skills) — how the docs and skill files themselves are written.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) — the bar is behavioral: every line of a skill file must change what the agent does.

## License

MIT
