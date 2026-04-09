# Dota 2 Draft Assistant

A single-file drafting tool built around the **Save / Damage / Catch** framework.

---

## The Core Idea

Every functional Dota 2 draft needs three things:

| Category | What it means |
|----------|---------------|
| **Save** | Ability to protect teammates or negate enemy initiation |
| **Damage** | Ability to kill heroes, scale, and win fights |
| **Catch** | Ability to start fights, control targets, or punish positioning |

Each hero is rated 0–3 in each category:

- `0` — None
- `1` — Light / situational
- `2` — Consistent contribution
- `3` — Core identity

---

## How It Works

1. **Pick heroes** for Radiant and Dire using the hero pool (or search by name, alias, or abbreviation)
2. **SDC totals** are calculated live per team
3. **Alerts** flag missing categories, imbalanced spreads, or contextual threats
4. **Three suggestion columns** update live to help you decide what to pick next
5. **Reset Draft** clears both teams instantly for a fresh iteration

---

## Suggestion Systems

### SDC Suggestions
Recommends heroes that fill your draft's weakest category. Penalises overstacking and adjusts dynamically for context:
- If your team already has a S3 hero (e.g. Oracle, Omniknight), save weight drops to near zero
- If the enemy has strong catch, save weight increases significantly
- Applies a priority mode when one category is significantly behind the others

### Counter Suggestions
Looks at every enemy pick and aggregates which heroes counter them. Uses Spectral.gg matchup win-rate data when available, falling back to the curated `hero_counters.json`.

- Heroes good into **multiple** enemy picks rank higher
- Enemy portraits are shown as mini-icons next to each suggestion card
- If a hero counters the **entire current enemy draft**, a gold **★ Whole Draft** badge replaces the individual icons and the reason line reads *"Counters the whole draft"*

### Hybrid Suggestions
Only appears when real overlap exists between the SDC and Counter lists. These are the picks that both fix your draft *and* beat the enemy — usually the highest-value picks on the board. Surfaced only when the overlap is genuine.

---

## Features

### Visual Ranking
Suggestion ranks 1–10 use a descending green colour ramp — rank 1 is large and bright green, rank 10 is small and muted. The top pick also gets a subtle green background tint so it reads instantly at a glance.

### Enemy Mini-Icons
Counter and Hybrid suggestions show small circular portraits of the enemy heroes the candidate counters. When a hero is good into the entire enemy lineup, a **★ Whole Draft** gold badge is shown instead.

### Spectral.gg Integration
When `stats.spectral.gg.json` is present and loaded, counter scoring uses real win-rate differential data (`diff` field) for matchup quality. A **Spectral** badge appears on items scored this way. Falls back to `hero_counters.json` silently when not available.

### Alias Search
The search box understands common abbreviations, alternate names, and community shorthand loaded from `heroes.json`:

| Query | Finds |
|-------|-------|
| `am` | Anti-Mage |
| `np` / `furion` | Nature's Prophet |
| `qop` | Queen of Pain |
| `ls` / `naix` | Lifestealer |
| `aa` | Ancient Apparition |
| `potm` | Mirana |
| `wr` | Windranger |
| `kotl` | Keeper of the Light |
| `od` | Outworld Destroyer |
| `cw` | Clockwerk |
| `ta` | Templar Assassin |
| `lc` | Legion Commander |
| `dk` | Dragon Knight |
| `sf` | Shadow Fiend |
| `pa` | Phantom Assassin |
| `sd` | Shadow Demon |
| `et` | Elder Titan |
| `sk` | Sand King |
| `cm` | Crystal Maiden |
| `tb` | Terrorblade |
| ...and more from the full alias table in `heroes.json` |

### Reset Draft
A **Reset Draft** button in the header clears both teams instantly. All bars, alerts, and suggestion columns update immediately — designed for fast iteration during live drafting practice.

---

## Files

| File | Purpose |
|------|---------|
| `index.html` | The full app — open directly in browser, or serve locally |
| `heroes.json` | Hero metadata: IDs, image tags, aliases, alt names |
| `hero_counters.json` | Curated top-5 counters per hero |
| `sdc_values.json` | SDC ratings — loaded at runtime and overrides embedded values |
| `stats.spectral.gg.json` | Spectral.gg matchup win-rate data (optional, enhances counter scoring) |

> **Running locally:** The app renders immediately with embedded SDC data. All JSON files are loaded via `fetch()`, which requires a local server. Run `python3 -m http.server` in the project folder and open `http://localhost:8000`. Without a server, alias search falls back gracefully to name-only matching, and counter scoring uses the embedded fallback data.

---

## Design Principles

- Suggestions fix what is *missing*, not what is already strong
- The system never over-recommends a category that is already covered
- Elite save (S3) heroes suppress save priority for remaining picks
- Enemy catch strength dynamically increases save weighting
- Hybrid picks are only surfaced when the overlap is genuine
- All scoring is explainable and based on the SDC values + counter data
- The whole-draft indicator only fires when a hero is legitimately good into every current enemy pick — it is not a display overflow artefact
