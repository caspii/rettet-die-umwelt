# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

**Rettet die Umwelt** ("Save the Environment") is the design of a browser game, created **by and with Josephine, age 11**. It is currently in the **concept phase** — there is **no code yet**. The repository holds a design document and title artwork, not a codebase.

There is no build system, no tests, no linter, no package manager, and no git repository. Do not invent or run build/test commands. When code eventually gets written, update this file with the real commands.

## Files

- `Rettet-die-Umwelt-Konzept.md` — the game design document (German). The source of truth for what the game is. Section 8 is a checklist of next steps; section 9 tracks progress. Keep both in sync when decisions are made.
- `Rettet Die Umwelt.png` — the current title-screen artwork and **art north-star**: a warm, glossy 3D cartoon (Pixar-ish) underwater scene, "Welt 1: Das verschmutzte Meer", with the snorkel-diver hero, a net, black oil blobs, colorful fish, coral. Match new art to this look.
- `Rettet-die-Umwelt-Konzept.md.pdf` — PDF export of the concept doc.
- `Ideen-Bilder/` — gameplay/decision mockups generated to help Josephine choose directions (see workflow below). The HTML pages in here are full standalone documents, double-click-openable like `Entscheidungen/`. **Rule: every HTML file in this repo must be a complete document with `<meta charset="utf-8">`** — they get opened via `file://`, where a missing charset garbles the German umlauts (Artifact-fragment style files without a `<head>` are not allowed to live here).

## Decisions locked in (as of 4 Jul 2026)

Chosen via the picture-decision pages and prototypes: hero **Carl der Otter** 🦦 (canonical sprites: `Ideen-Bilder/Carl-Otter-Seitenansicht.png` = side view facing right; `Held-4-Otter.png` = front portrait); **Welt 1: Das verschmutzte Meer**; **free-swim** movement (all directions, floaty — this refines/overrides the earlier "side-scroller/seitwärts laufen" pick); oil collected with an active **net-scoop** (press a button to catch, not auto-on-touch).

**REOPENED (9 Jul 2026):** the earlier "peaceful — no enemies" pick. Josephine changed her mind and wants danger/opponents. She picks the level in `Entscheidungen/prototyp-4-gefahr.html` (4-step ladder: Friedlich / fleeing Öl-Monster / Qualle that knocks 3 collected blobs loose + stuns / Herzen-Modus where 3 jellyfish hits gently restart the round). Guardrail that stays regardless of her pick: **losing is always soft and instantly retryable — no scary game-over.** Kid-changed-their-mind is a supported workflow: reopen the decision in all three docs (concept §2/§4/§9, decision log, here), don't paper over the history.

**Build tech (decided):** a **real HTML5 browser game — plain JavaScript + Canvas, no framework, no build step**, self-hostable. Explicitly **not Scratch** (Scratch was only ever a beginner on-ramp; rejected because the goal is an ownable, extensible browser game — dad codes, Josephine designs/tests). **No sound** in the MVP.

**Win condition:** *Das saubere Meer* — clear all the oil → water turns clear, animals rejoice (art: `Ideen-Bilder/Sieg-A-Sauberes-Meer.png`). **Scope of v1 (decided):** one **open-sea area** (single screen, not a scrolling level), **tablet-first** (on-screen buttons; keyboard also works), minimal (swim + net-scoop + win + short start screen).

**Still open** (see `Entscheidungen/`): (1) the **danger level** — Prototyp 4, see above; (2) the **difficulty/challenge** tuning — `Entscheidungen/prototyp-3-schwierigkeit.html` (slider panel for oil count, drift, oil-spreads-if-slow, 1–3 stars, optional gentle timer; water visibly clears as you collect; win = the chosen clean-sea screen). The values she settles on become the real game's constants. Then: start-screen look. Source of truth for decisions is concept doc §2. Design principle for challenge: skill comes from aiming the net at drifting/fleeing oil, soft pressure from opponents that cause setbacks (never harsh fail states), replay value from optional stars.

## Decision documentation & prototypes — `Entscheidungen/`

Standalone, double-click-openable local HTML files (full docs with `<meta charset="utf-8">` — required for umlauts over `file://`). `index.html` is the **master** decision log (numbered progression of settled decisions + open ones + links). `prototyp-1-bewegung.html` and `prototyp-2-sammeln.html` are **playable Canvas prototypes** (embed Carl as a data URI so they work from `file://`) that let Josephine *feel* an option rather than judge a static picture — the right tool when a decision is about game-feel. To verify these locally: `python3 -m http.server` in the repo root, then drive with Playwright (the Claude-in-Chrome extension can't open the private claude.ai artifacts or `file://`).

## Working style: decide with pictures

Josephine (11) makes design decisions by **looking at options, not reading questions**. For each open question in the concept doc, generate 2–3 illustrated variations in the established art style and let her pick. Generate images with the `mcp__gemini-nanobanana-mcp__edit_image` tool using `Rettet Die Umwelt.png` as the input image — editing the poster keeps the hero and style consistent across mockups. Save mockups to `Ideen-Bilder/` with descriptive German filenames. Decision backlog: how you play (swim vs. side-scroller) → who the hero is → friends/foes → buildable art style.

## Working with this project — important context

- **Everything is in German.** The design doc, the game, and any UI text should be German. Write to Josephine and about the game in German unless asked otherwise.
- **Audience is an 11-year-old beginner.** Keep explanations, code, and tooling suggestions simple, encouraging, and age-appropriate. Josephine is just starting to learn to build games.
- **The intended scope is deliberately staged** (see concept sections 6–7). Start tiny: one world, one character, one task, single-player. Add multiplayer (MMO) and voice chat only much later — they are explicitly flagged as the hardest parts, for adults to help with.
- **Recommended tooling path** from the concept: begin with **Scratch** (scratch.mit.edu) or **MakeCode Arcade** for the first playable world; graduate to **Phaser** or **Construct 3** ("real" browser-game tools) only once the basics work. The end goal is a browser game (side-scroller) that runs on tablet and computer.

## The game, in brief

A colorful side-scroller where players solve environmental tasks across different worlds (underwater / oil cleanup, desert / plant trees, forest, city, mountains, recycling factory). Long-term vision is an MMO with voice chat; the near-term plan is a single small, fun, single-player world.
