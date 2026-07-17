# Brief — rules and template

The brief is written before any interface code and is binding afterwards. It lives at `.design/brief.md`.

## Gather taste before choosing

- If the Mobbin MCP is connected: search 5–10 real screens of this product category first and note in the brief what current, well-crafted examples of the category actually do. Reference feeds judgement; the direction is still an original choice.
- If the user keeps an Are.na channel for this project or names one: read it the same way.
- Neither available: proceed on the brief's own terms.

## Direction

State one named aesthetic direction (e.g. "editorial brutalism", "clinical warmth", "terminal luxe") and justify it in one sentence that could only apply to *this* brief. Take one real aesthetic risk you can defend.

When the user is present and the input was vague, draft **three distinct candidate directions** (one paragraph each, naming palette mood, type feel, layout archetype and signature) and let them pick before continuing. Running autonomously: pick one, record the two runners-up in the brief.

## Numeric constraints (v0 discipline — exceed only with the user's explicit permission)

- Palette: **3–5 colors total**, each a named hex — 1 primary, 2–3 neutrals, 1–2 accents. Light and dark values for each.
- Typography: **at most 2 font families**, with roles (display / body / mono as needed).
- Exactly **one signature element**: a custom visual move (layout device, interaction, illustration system, distinctive component) that a generic template would never contain.

## The choice test

For each of palette, typography, layout and motion, answer in the brief: *"Is this a choice this brief demands, or the default I would produce for any similar page?"* Rewrite anything that reads as a default until every choice is defensible in one sentence tied to the brief. Fonts, palettes and layouts that dominate AI-generated sites are, by definition, defaults — a choice looks chosen.

## Taken-directions check

Apply the rule defined at the top of the skill's `style-history.md` against every row. Record in the brief which rows were compared and on which axes the new direction differs. A direction that fails the rule is a rerun — choose again.

## Template (`.design/brief.md`)

```markdown
# Design brief — <project>
Date: · Client/product: · Audience: · Job of this surface:
Tone: <3 adjectives>
References consulted: <Mobbin/Are.na/URL findings, or "none">

## Direction: <name>
<one-sentence justification specific to this brief>
Runners-up considered: <if any>

## Palette (3–5, light/dark)
<name — hex/hex — role> per line

## Typography (≤2 families)
<family — role — why it fits>

## Layout archetype
<name + one line>

## Signature element
<what it is, where it appears>

## Motion
<stance: what moves, what never moves; the house easing set (2–3 named curves + durations) tuned to this direction>

## Imagery (when the surface uses images)
<one treatment rule for ALL imagery — e.g. dithered/duotone real photos, generative only for covers — so images carry the identity instead of diluting it>

## Choice test
<one line per dimension: why this is a choice, not a default>

## Taken-directions check
<rows compared, axes on which this differs>
```

Brief-lite (small components): Direction + numeric constraints + choice test only, appended to the existing `.design/brief.md`.
