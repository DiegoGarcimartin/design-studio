# Craft — the polish layer (loaded at Build)

Polish is numbers, never adjectives. Distilled from Kevin Kld's "10 rules to ship truly polished UI" (x.com/kvnkld/status/2066863634949779464). Every recipe below pulls its values from the token layer — when a recipe needs a value the tokens lack, grow the tokens first.

## Motion

- The token layer defines a **house easing set**: 2–3 named curves plus durations, and every transition in the project names one. Starting points to tune by feel: `--ease-smooth: cubic-bezier(0.22, 1, 0.36, 1)`; `--ease-pop: cubic-bezier(0.35, 1.55, 0.65, 1)` (slight overshoot, for things that pop in); `--duration-fast: 150ms`, `--duration-base: 280ms`. Tuning them to this project's feel is part of the direction.
- **Entrances focus into place**: opacity 0→1 + translateY 6px→0 + blur 2px→0, ~280ms on the smooth curve. The clearing blur is what reads as premium.
- **Expand/collapse** animates `grid-template-rows: 0fr → 1fr` (real content height, no jump). Elements that move between containers animate with FLIP (measure first, measure last, invert, play).
- **Draggables behave like physical objects**: velocity-aware momentum on release, coasting to rest; edges stretch slightly and spring back. Meaningful values get magnetic snap points — tight pull-in zone, larger release zone, label pulse when it catches.
- Long lists and large surfaces animate transform and opacity only; heavy effects (shadow stacks, height) are reserved for small deliberate moments. `prefers-reduced-motion` collapses animation to instant and stops decorative loops.

## Depth

- Edges are defined by light: a hairline ring (`0 0 0 0.5px rgba(0,0,0,0.08)`) where a 1px border would go.
- Depth is many faint layers, each at 2–8% opacity: tight contact shadow + wide soft ambient, e.g. `0 1px 2px rgba(0,0,0,0.05), 0 2px 4px rgba(0,0,0,0.02), 0 0 0 0.5px rgba(0,0,0,0.08)`. Two presets in the tokens — card and elevated — reused everywhere, animated as a whole stack on hover.
- **Product surfaces run flatter than marketing surfaces**: in-app panels and tables get hairline edges and background-layer contrast only; the layered shadow stack is reserved for true overlays (modals, popovers, dragged items).

## Field notes — measured live from Vercel, Supabase and Resend (Jul 2026)

Palette-independent rules, read from computed styles of shipping dashboards; they hold for any direction the brief picks:

- No pure extremes in the ink/ground pair: grounds at ~oklch(0.99)/#FAFAFA, inks at ~oklch(0.1)/#171717, light-on-dark text at ~#F0F0F0 (Resend's pure-black ground is the one exception, on the ground only).
- **Borders are the ink at 6–20% alpha, never a third invented gray.** Supabase derives its entire neutral ramp (borders, muted, hovers) from two anchor colors via oklch calc; the portable version: define ink + ground as tokens, derive every neutral from them with alpha.
- Controls at 6px radius (Vercel and Resend agree); pills fully rounded.
- Transition durations 150–300ms on the cubic-bezier(0.4, 0, 0.2, 1) family — consistent with the house set above.
- Focus is a double ring: 2px in the surface color plus 4px in the accent, so it reads on any background.

## Touch

- Every clickable element responds to press: scale to 0.98 on the fast duration — firm press, not collapse.
- Tooltips and overlays lift in (fade + 4px rise + blur clearing), on the same house curves.

## States are the component

Before building any interactive component, list its states — idle / hover / pressed / loading / disabled / empty / success — and build all of them. Expect the build to surface 2–3 states the plan missed; adding those discovered micro-interactions (numbers that roll digit-by-digit, a shimmer sweeping a busy label, icons that cross-fade) is where the polish actually lives, so budget for them rather than treating them as scope creep.

## Detail density

Perceived quality scales with the density of visible decisions: context captions under headings, secondary metadata lines, in-chart annotations, unit labels, tooltips, a second affordance where one would do. A restrained palette must be earned with *more* of these, never fewer — quiet plus sparse reads as unfinished; quiet plus dense reads as expensive.

## Iterating

Tune one variable at a time — only the shadow stack, only the entrance, only the easing. Describe targets as feel plus reference plus numbers ("like an iOS sheet: weighty, slightly springy, settles fast; ~280ms on --ease-smooth").
