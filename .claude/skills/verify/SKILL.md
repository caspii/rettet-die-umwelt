---
name: verify
description: How to run and verify the browser game Spiel/index.html (and the Entscheidungen/ prototypes) end-to-end with Playwright
---

# Verifying the game (`Spiel/index.html`)

No build step, no deps — a single self-contained HTML file. Serve + drive with the Playwright MCP tools:

1. `python3 -m http.server 8741 --bind 127.0.0.1` in the repo root (run_in_background).
2. Navigate to `http://127.0.0.1:8741/Spiel/index.html` — the Playwright MCP blocks `file:` URLs, so `file://` readiness is verified statically instead (see gotchas).
3. The game exposes a console/test API: `window.spiel` — `zustand()` (`'start' | 'spiel' | 'gewonnen'`), `gefangen()`, `holOel()` (blob array, `weg` = caught), `carl` (mutable x/y/vx/vy/blick), `fangen()`, `starten()`.

Flows worth driving:
- Start: click `#losKnopf` (or press Space) → `zustand() === 'spiel'`.
- Swim: real ArrowRight/WASD keydown+keyup with a delay between → `carl.x/y` change, `blick` flips when moving left.
- Catch: set `carl` next to a blob (`x = blob.x - 56, y = blob.y - 8, blick = 1`), press real Space → `gefangen()` +1, HUD `#hud` updates. Cooldown is 0.3s — wait ≥340ms between scoops.
- Win: catch all blobs → after ~800ms `#siegBildschirm` loses `.verborgen`; `#nochmalKnopf` resets to a fresh round.
- Tablet controls: dispatch `pointerdown`/`pointerup` on `.pad button` and `#fangKnopf`.
- Layout: resize to 1180×820 and 820×1180 → no page scroll, `.pad` and `#fangKnopf` fully in viewport.
- Finish with `browser_console_messages` — must be 0 errors/warnings.

Gotchas:
- `#losKnopf` / `#nochmalKnopf` hide themselves on click, which makes Playwright's `browser_click` time out **after the click already landed**. Don't retry — check `window.spiel.zustand()`; or click via `el.click()` in `browser_evaluate`.
- The game must stay double-click-openable (`file://`): no `fetch`, no ES modules, no external `src`/`href` (Carl is a base64 data URI). After edits, grep for those.
- Repo rule: every HTML file needs `<meta charset="utf-8">` or German umlauts garble over `file://`.
