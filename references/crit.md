# Crit — evaluator loop

The builder never grades its own work: agents reliably praise what they made. A separate evaluator agent judges the *rendered* interface, not the code.

## Protocol

1. Render the real thing: start/reload the dev server in the browser pane; screenshot at 375, 768 and 1440 (light and dark if the project themes).
2. Dispatch an evaluator subagent (Agent tool) with browser access to the running page, the screenshots, the brief, and the rubric below. Its mandate: *find the weakest 20% of this design and name a concrete fix for each weakness*. It scores each criterion 1–10 and must justify every score against what it saw, citing the brief.
3. Apply the fixes that survive your own judgement (the evaluator advises; the brief decides ties).
4. **Snapshot each round** — copy the screenshots to `.design/crit/round-N/` and note the scores. Improvement is not monotonic: round 3 sometimes beats round 5.
5. Repeat.

## Rubric (evaluator scores all four)

- **Design quality** — hierarchy, spacing rhythm, composition, color discipline. Does it look like a designed product?
- **Originality** — evidence of custom decisions, or template layouts, library defaults and AI-generated patterns? The signature element lands, or is decoration?
- **Craft** — alignment, consistency of radii/shadows/spacing against tokens, typographic detail, state coverage (hover/focus/empty/loading), motion on the house easing set (entrances focus into place; presses respond; nothing rides a browser-default curve).
- **Functionality** — the interface works: navigation, interactions, responsive behavior at all three widths, keyboard focus visible.

## Exit condition

Ship when **every criterion scores ≥ 8** or when **two consecutive rounds fail to raise the total** — whichever comes first, with a minimum of 2 rounds and a maximum of 6 for a full product surface (1 round for Brief-lite work). Ship the *best-scoring* snapshot, not the latest: if an earlier round scored higher, restore it and carry forward only the later fixes that don't regress it.
