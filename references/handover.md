# Handover — design-ops artifacts

Every full engagement leaves the project resumable by someone (or some session) that never saw this conversation. All artifacts live in `.design/`.

- `brief.md` — already written in phase 1; verify it still matches what shipped, and amend (with a dated note) where the crit loop changed a decision.
- `tokens.json` — the DTCG token file, matching the theme file in force. If the project would benefit from generated platform outputs (CSS vars, Tailwind preset, TS constants), wire Style Dictionary or Terrazzo and note the build command here.
- `design-system.md` — for a human or future agent: the token vocabulary and how to use it, component inventory with their states, the signature element and where it may (and may not) be reused, do/don't examples for extending the UI without breaking the direction. Ends with two short sections: an **extension checklist** (the minimums any new asset passes before shipping — visual, voice, message) and a **version log** (dated entries; when a system change affects existing key assets, the log names which ones need redoing).
- `decisions.md` — the why-dictionary: each consequential choice (direction, palette, type, layout, signature, anything the crit loop reversed) in one line: *decision — reason — date*.
- `crit/` — the round snapshots and scores from phase 4, kept as evidence of what was tried.
- `voice.md` + `messaging.md` — only when the surface carries real copy (landings, product marketing): how the brand speaks (tone, sentence length, words it uses and avoids) and its key messages, so future assets start from on-brand sentences instead of placeholder filler.

Done when all five exist, none contradicts the brief, and a stranger could extend the UI from `design-system.md` alone.
