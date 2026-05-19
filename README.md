# Uma Musume Trackblazer Scheduler

A browser-based race schedule optimizer for Uma Musume's Trackblazer mode. Plans the full Junior → Senior schedule to maximize stats, skill points, and epithet completions.

This is a **personal fork**. I add features I find useful for my own runs; it's public so the changes don't disappear into a private repo, but I'm not actively chasing parity with upstream or taking feature requests. If something here looks broken or odd, the upstream version is probably the better starting point.

Original work by [SkyeNat21](https://github.com/SkyeNat21/umamusume_trackblazer_scheduler), upstream maintained by [daftuyda](https://github.com/daftuyda/umamusume_trackblazer_scheduler).

---

## What this fork adds

On top of the upstream feature set (MILP solver via GLPK.js, character presets, manual locks, epithet tracking, share links, light/dark themes):

- **Turn stepper** — Walk through the schedule one race at a time with Confirm / Skip / Lost / Back. Auto-jumps over training turns, highlights the current turn on the calendar.
- **CM target presets** — Real Champions Meeting calendar (CM1–CM15) with build-target weights auto-derived from each CM's distance, surface, handedness, and season. Plus a Custom CM form for manual conditions.
- **Build-target hint weighting** — Per-race scoring bonus based on how well each race matches the targeted CM attributes. Includes seasonal axis (Spring / Summer / Fall / Winter).
- **Max race distance cap** — Hard filter to avoid stayer-trap epithets when training Mile/Sprint. Optional toggle to show over-cap races in the picker without letting the solver pick them.
- **Quadruplet (4-in-a-row) penalty** — Optional, models the heavier in-game conditioning hit beyond the existing 3-in-a-row penalty. Late Dec exemption respected.
- **Skippable race highlighting** — Races that contribute to epithets but aren't uniquely required are visually flagged (dashed amber outline).
- **Epithet progress fractions** — Shows current / required count on each completed epithet (e.g. "5 / 3" surplus), and optionally lists in-progress epithets in grey.

---

## Running it

Static site, no build step. Serve the directory with any local HTTP server:

```bash
python -m http.server 8000
# or: npx serve .
```

Open `http://localhost:8000`.

---

## Layout

| File | Purpose |
| --- | --- |
| `index.html` | Page shell |
| `app.js` | UI, state, stepper, tooltip interactions |
| `solver-browser.js` | MILP model, GLPK interface, CM calendar |
| `styles.css` | Themes + layout |
| `races.json` | Race database |
| `epithets.json` | Epithet definitions |

### Dependencies

- [GLPK.js](https://github.com/jvail/glpk.js) (CDN) — MILP solver
- Google Fonts — M PLUS Rounded 1c, Outfit

No npm, no bundler, vanilla ES modules.

---

## License

Inherits from upstream. Contact the upstream repo owner for terms.