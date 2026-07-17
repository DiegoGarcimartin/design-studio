# Extraction — reference → raw material

Runs before the brief when the user supplies a visual reference. Output: `.design/extracted-tokens.json` plus extraction notes inside the brief.

Boundary: if the user wants the result to *match* the reference faithfully ("clone this", "same style as"), stop — that is a fidelity job for a dedicated cloning skill (or an explicit scope conversation), not this one. Here the reference is inspiration: raw material the brief may inherit from or deliberately depart from.

## Reference is a URL

1. Try `npx dembrandt <url>` — extracts colors, typography, spacing, borders, shadows, motion and component styles from the live site in one command.
2. Dembrandt unavailable or fails: open the URL in the browser pane and read computed styles directly (theme CSS variables, font stacks, spacing rhythm, radii, shadows, motion durations).

## Reference is a screenshot

Read the image and estimate: palette (sample dominant + accent hexes), type classification (serif/sans/mono, weight range), spacing rhythm, layout archetype, mood in 3 adjectives. Mark every estimated value `~approx` in the notes.

## Hand off to the brief

Write into the brief's "References consulted" section: what the reference does well worth inheriting, and what the new direction deliberately does differently. The taken-directions check and choice test still apply — an inherited palette is a choice like any other and must be defended.
