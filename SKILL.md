---
name: design-studio
description: Design product UI from an idea to a verified interface — landing pages, web apps, dashboards, redesigns, any user-facing surface judged as product design. Use when the user asks to design or build product UI, whether the input is a vague idea, a visual reference (URL/screenshot), or both. Brand-locked slide/deck work and faithful reference cloning belong to dedicated skills when installed.
---

Run as a design **studio** taking on a new client. The studio's process is identical every engagement; its output never repeats — a studio that ships the same identity to two clients loses both. The user is the creative director: when present, they pick the direction; the studio never asks them to do legwork.

## Intake (every engagement)

1. Read [style-history.md](style-history.md) — every row is a direction this studio has already shipped, and its header defines the rule that keeps the new direction from being a rerun.
2. Classify the input and branch:
   - **Reference given** (URL or screenshot) → load [references/extraction.md](references/extraction.md) and extract raw material before briefing.
   - **Idea only** → go straight to Brief.
3. Scale the engagement: full pipeline for product surfaces (landing, app, dashboard, multi-screen flow); for one small component inside an existing design, run Brief-lite (direction + tokens check only) → Build → one crit pass.

## Pipeline

### 1. Brief — binding
Load [references/brief.md](references/brief.md); produce `.design/brief.md` in the project.
Done when the file exists and passes every check listed in brief.md.
Hard gate: interface code is written only after `.design/brief.md` exists; once written, the brief is a contract — later work cites it, it doesn't drift.

### 2. Tokens first
From the brief, write the token layer before any component: `.design/tokens.json` (DTCG syntax: `$value`/`$type`) plus the project's theme file (CSS variables / Tailwind config).
Every color, font, size, radius, shadow, easing curve and duration in components resolves to a token — motion is tokenized like color (the house easing set, defined in [references/craft.md](references/craft.md)). When a component needs a new value, the token file grows first, then the component consumes it.
Done when tokens.json exists and the theme file loads without errors.

### 3. Build
Load [references/craft.md](references/craft.md). Build against tokens, matching the brief. The signature element ships — it is what makes the result this client's product and nobody else's. Every interactive component ships its full state system (craft.md defines the bar).
Quality floor, silent: responsive at 375/768/1440, visible keyboard focus, `prefers-reduced-motion` respected, WCAG AA contrast.

### 4. Crit
Load [references/crit.md](references/crit.md). Render the real interface in the browser, screenshot it, and run the crit loop with a separate evaluator agent against the rubric.
Done when crit.md's exit condition is met — never on the first pass for a product surface.

### 5. Handover
Load [references/handover.md](references/handover.md); produce the design-ops artifacts in `.design/`.
Done when every artifact handover.md lists exists and none contradicts the brief.

### 6. Close
Append the shipped direction as a new row in [style-history.md](style-history.md) (format defined at the top of that file). Done when the row exists.
