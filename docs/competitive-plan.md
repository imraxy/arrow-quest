# "Arrow Quest" — Development Plan (Arrow Puzzle-style, better, publishable)

Working title options: **Arrow Quest**, **TapFlow**, **Escape Arrows**
Genre: hybrid-casual directional tap puzzle. Reference: Easybrain "Arrow Puzzle" (93M installs, ~$1M+/mo, #1 puzzle India, launched Nov 2025 — proven market, still hot, but saturated with clones).

---

## 1. Why this can win (research summary)

**Market facts:**
- Arrow puzzle was a top-5 most-downloaded mobile game category in June 2026 (Arrows – Puzzle Escape 25.3M installs/mo, Amaze GO! 23.2M, Easybrain's Arrow Puzzle 16.4M).
- Genre revenue grew ~911% YoY ($15.4M → $156M). Hybrid-casual monetization (IAP + ads) is the standard.
- The base mechanic alone is NO LONGER a differentiator — a wave of near-identical clones from small publishers flooded the charts.

**What players complain about (our opening):**
1. **Tap sensitivity** — taps registering on the wrong arrow (most common Easybrain complaint).
2. **Glitches** — game freezing around level 600+ in Easybrain's title.
3. **Difficulty swings** — copy-pasted level design, too easy → artificially blocked.
4. **Forced ads after paying** — ads that persist after purchasing "remove ads."
5. **Repetitiveness** — no advanced mechanics in later stages (cited as the genre's retention risk).

**Our differentiation = fix all five + add a meta layer.**

---

## 2. Core game design

### 2.1 Core loop (familiar, refined)
- Grid of arrows pointing in 4 cardinal directions. Tap an arrow: if its path to the board edge is clear, it slides out. Goal: clear the whole board.
- **Improvements over reference:**
  - **Generous hitboxes + tap intent** — tap resolves to the nearest arrow within a comfortable radius, with a brief highlight-then-confirm feel (or drag-to-select). Fixes complaint #1.
  - **No lives/energy punishment for experimentation** — wrong tap = arrow shakes, no penalty; keep the "relaxing" promise. (Easybrain uses lives; reviewers dislike it. Alternatively: mistakes allowed count feeds a 3-star rating instead.)
  - **Undo button** (limited, rewarded ad refills) — genre rarely has it.
  - **Zero-glitch engineering target** — deterministic, offline-first logic; level data pre-verified (see §4).

### 2.2 New mechanics (introduced every ~10-15 levels, roller-coaster difficulty)
- **Ice arrows** — slide until they hit something (frictionless), can't stop mid-path.
- **Double arrows** — must be tapped twice (second tap after they land again).
- **Locked/gold arrows** — freed only after clearing N other arrows.
- **Portal pairs** — arrow exits through matching-colored portal elsewhere on the board.
- **Bomb arrow** — clears its row/column when tapped, but only if path clear (risk/reward).
- **Mirror arrows** — direction flips when an arrow passes adjacent to it.
- **Timed bonus levels** — optional, for streak/coin bonuses (never mandatory — keeps it relaxing).

### 2.3 Meta layer (this is what makes it publishable/marketable, not a rip)
- **Journey/World map**: themed worlds (Forest → Desert → Ice → Volcano → Sky → Space), 40-60 levels each, distinct art palettes and background music.
- **Meta collection**: cleared boards earn pieces to **build/restore a little world** (village → city → floating islands). Proven pattern (Woodle Screw, Woodoku-style metas) that lifts D30 retention from ~5% to 8-15%.
- **Daily challenges + streak calendar** (Amaze GO!'s fastest-growing LiveOps element — streak by level 4).
- **Events**: weekend themed level packs, collectible sets ("umbrella events" — fastest-growing live-ops format per Liftoff 2025).
- **Win streaks** with escalating rewards.

---

## 3. Tech stack

| Layer | Choice | Why |
|---|---|---|
| Engine | **Godot 4.x** | Native 2D, tiny builds (~30-50MB vs 150MB+ Easybrain), zero licensing fees, fast iteration. Unity only wins if we need its ad-SDK maturity; Godot has community AdMob/AppLovin plugins that work fine for casual titles. |
| Language | GDScript | Fast dev; C# not needed (no web export requirement). |
| Ads | AdMob (banner/interstitial/rewarded) + AppLovin MAX mediation | Standard hybrid-casual stack. |
| Analytics | Firebase Analytics + GameAnalytics | Funnel + retention tracking from day one. |
| IAP | Google Play Billing + RevenueCat (optional) | No-ads ($3.99), coin packs, hint bundles, battle pass. |
| Backend | None at MVP — levels bundled as compressed binary (see §4); remote config via Firebase for difficulty tuning + LiveOps flags | Serverless = cheap, offline-capable. |
| Platforms | Android first (biggest genre market, India #1), iOS at soft launch | Both from one Godot codebase. |

**Team (minimal):** 1 gameplay programmer, 1 artist (or curated asset pack + color grading), 1 part-time designer/level-gen engineer (can be same person), contractor for music/SFX. Realistic solo-dev possible with asset packs; 2-person ideal.

---

## 4. Level generation & QA (the moat)

The single biggest quality differentiator. Plan (based on proven published algorithms):

1. **Reverse/DAG generation**: build levels backwards — start from empty board, place arrows so each new arrow's exit path is blocked only by arrows placed after it in exit order. This guarantees 100% solvability (valid DAG, no cycles).
2. **Difficulty = measured, not guessed**: after generation, run a BFS solver over each candidate to compute optimal move count and branching factor; bucket levels into difficulty bands.
3. **Curated funnel**: generate thousands of candidates offline, auto-filter (solvability, difficulty band, near-duplicate detection), human-curate the top ones into the world progression. Roller-coaster curve: gradual rise, occasional spike, then an easy breather.
4. **Deterministic seeds** — every level pack reproducible from a seed in the commit history.
5. **Offline verifier** in CI: re-solve all levels on every build; fail the build if any level is unsolvable or below its difficulty band. (This is how we guarantee "zero glitch" — no level 600 freeze, no impossible boards.)
6. Ship **1000+ levels at launch** (500 generated + curated, ~50MB binary), new world packs monthly.

---

## 5. Monetization (hybrid-casual standard)

- **Ads (≈60-70% of revenue):**
  - Interstitial: every 3-5 levels, never mid-level, skippable, capped daily.
  - Rewarded video: hints, undos, level skips, streak recovery, daily bonus x2.
  - No banner at MVP (hurts UX; add later A/B tested).
- **IAP (≈30-40%):**
  - Remove ads $3.99 (REALLY removes all of them — fixes complaint #4).
  - Coin packs ($0.99-$9.99) for hints/undos.
  - Optional season pass ($4.99/mo) post-launch.
- **Target KPIs (from benchmarks):** D1 ≥ 40%, D7 ≥ 18%, D30 ≥ 8%, ARPDAU $0.15+, session 12+ min, CPI target < $0.60 (hyper-casual channels) / < $1.80 (casual US).

---

## 6. Publishing & marketing plan

**Store presence:**
- ASO: name with "Arrow"/"Puzzle"/"Tap Away" keywords ("Arrow Quest: Tap Away Puzzle"); localized listings (start: EN, HI, ID, BR-PT, ES, TR — genre's biggest markets).
- 30-sec gameplay video + 8 screenshots showing mechanic variety and meta world.

**UA strategy:**
- Playable ads + "fail-loop" video ads (show an almost-solved board, viewer taps) — genre-standard high-CTR creative.
- Channels: TikTok ($1.20 US CPI, cheapest), Unity Ads, AppLovin; Google UAC for scale.
- Start $10-20/day creative testing, 5-10 ad variants/week; kill anything above target CPI.

**Soft launch:** Philippines/Indonesia/Brazil (cheap CPI), 4-8 weeks, iterate on D1/D7. Kill/pivot criteria: D1 < 30% after 2 iterations = core loop problem; D7/D1 ratio < 0.30 = FTUE problem.

**Full launch:** once D1 ≥ 35% and D7 ≥ 15% in soft launch → global + push to press/reddit (r/puzzlevideogames, r/AndroidGaming "we built this" posts work well for indie puzzle launches).

**Live-ops cadence (post-launch):** new world monthly, daily puzzle, weekend event, seasonal skins for the meta world.

---

## 7. Roadmap (realistic, 2 devs)

| Phase | Weeks | Deliverables |
|---|---|---|
| P0 Prototype | 1-3 | Core tap-clear mechanic + generator v1 (500 levels), playable on device. Playtest fun. |
| P1 Vertical slice | 4-7 | Full game feel: juice (tweens, particles, sound), 3 worlds, stars, hints/undo, FTUE. |
| P2 Soft-launch build | 8-12 | Ads SDK, IAP, analytics, 500-1000 levels, meta world v1, daily challenge. Closed beta. |
| P3 Soft launch | 13-20 | 2 markets, iterate retention to targets, fix everything. |
| P4 Global launch | 21+ | ASO polish, UA creative testing, world #4-5 content pipeline. |

**Budget (bootstrapped):** ~$3-6k — Google Play ($25 one-time) + Apple ($99/yr), asset packs/art contractor $1-2k, music $300, UA test budget $2-3k. Zero engine licensing.

---

## 8. Key risks & mitigations

1. **Clone saturation** → differentiation through meta layer + mechanics variety + quality (fix the 5 complaints).
2. **Retention collapse after level ~50** (genre-known issue) → new mechanic every 10-15 levels, meta world, events.
3. **Godot ad SDK maturity** → prototype ad integration in P1, not P2; fallback = Unity (design is engine-agnostic).
4. **Easybrain marketing muscle** → we don't outspend; we out-quality niche (indie-friendly markets first, ASO long-tail keywords they ignore).
