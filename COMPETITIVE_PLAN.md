# Arrow Quest v3 — Competitive Redesign Plan
*Based on teardown of Arrows–Puzzle Escape (Lessmore), Amaze GO! (Oakever), Color Block Jam (Rollic) + their store-review complaints*

---

## 1. Strategic read (why clones die, winners win)

- The mechanic is commoditized. 10+ clones, none scaled. The winners own the **wrapper**: FTUE, feel, economy, fairness.
- Amaze GO (100M DL) wins on core feel (ASMR whoosh, calm) but bleeds users on: ads after EVERY level (top complaint, no IAP to remove them), fake "99% fail" stats, tap misregistration, boards bigger than screen with pan-tap conflicts, pointless points with no leaderboard.
- Arrows Escape wins on purity but is shallow: repetitive later, no advanced variation, greedy ads ($10 remove).
- Color Block Jam proves the retention stack: pre-level boosters + win-streak + meta = D7/D30 in a different genre. That stack is portable.

**Our thesis: same proven core + every competitor's best feature + none of their top-10 complaints.** We don't out-engineer them; we out-fair them.

---

## 2. Feature spec (competitive parity +)

### 2.1 Core feel (match Amaze GO quality bar)
- ASMR-style layered exit sound (whoosh + pop, pitch rises with combo) ✓ (v2 base exists)
- Wave-dot residue where a piece exited (visual progress memory — Arrows Escape's best detail)
- Long-press = **Guidance**: highlights the tapped piece's full path on the board before commit (Amaze GO's most-praised feature)
- Perfect-run tracking: hearts kept → "Perfect!" + bonus coins
- Combo pitch escalation on consecutive quick exits

### 2.2 Progressive FTUE (Arrows Escape's playbook)
- L1-2: board only, no buttons at all
- L3: undo appears · L5: hint appears · L8: hearts system explained
- L10: first special mechanic (wall) · every ~15 levels after: one new mechanic
- 0-tap tutorial: the board IS the tutorial (first level auto-solves one piece with a ghost-hand hint)

### 2.3 Mechanics ladder (the "additive features")
| Mechanic | Level | Rule |
|---|---|---|
| Walls/blocks | 10 | impassable cells |
| Double-tap pieces | 25 | 2 exits needed |
| Locked pieces | 40 | unlock after N clears |
| Portals | 55 | enter→warp→exit other side |
| Rotator cells | 70 | piece direction changes passing through |
| Ice pieces | 90 | slide until wall (frictionless) |
| Bomb pieces | 110 | clears a 3×3 area once |
| Dark zones | 130 | fog over unrouted area |
(All generator-supported: extend reverse-placement with per-type validation + BFS verify.)

### 2.4 Structure & retention
- **Difficulty badges**: Simple / Hard / Super Hard shown pre-level (self-selection, Amaze GO)
- **Shape boards**: pieces arranged as hearts/cats/stars/etc via silhouette masks (Amaze GO's caterpillar mode is loved)
- **3 hearts per level**; fail = piece RETURNS to origin (Arrows Escape rule — never deadlocks), not stuck
- **Fit-to-screen always** (Amaze GO's #1 UI complaint fixed; pan never misfires as tap — dedicated pan gesture threshold)
- **Daily Challenge**: seeded level/day + monthly trophy calendar
- **Win streak (5 steps)**: each win → progress → at 3/5 grant random pre-level booster, at 5/5 grant both (Color Block Jam's proven loop)
- **Boosters**: Undo+1, Magnet (auto-clears one piece), Shuffle — pre-level select or earn via streak
- **Achievements**: 30 milestones (clears, perfects, streaks, mechanics mastered)
- **Progress map**: 12 worlds × 40 levels, themed palettes, world completion stars
- NO league/demotion (Amaze GO's most-hated addition) — relaxation is the brand

### 2.5 Economy & monetization (fair by design — this is the moat)
- Interstitial: every 3rd level, capped 8/day, NEVER after a fail, never mid-flow
- Rewarded video: only player-initiated (hints, booster top-ups, streak repair)
- **Remove ads: $2.99** (actually removes all; the anti-greed play — every competitor fails here)
- Coin shop: hints/booster packs; earnable at ~30/level
- No energy system. No fake stats. Real fail-rate stats with a settings toggle.
- Optional season pass LATER (post-soft-launch data), not at launch

### 2.6 Accessibility (free wins nobody does)
- Colorblind-safe: path-highlight uses dash pattern, not just color
- Settings: music/SFX sliders (not 3 toggles), haptics toggle, stats toggle
- One-thumb portrait; nothing important in top 8% (notch) or bottom 10% (gesture bar)

---

## 3. Architecture (build on what exists)

- Godot 4.7 project (working) + generator v2 (110 verified levels) → extend to:
  - **Generator v3**: shape masks, mechanic placement constraints, BFS solver with per-mechanic move model, difficulty banding by avgFree score, near-dup filter → emit 1,200 levels in 12 worlds
  - Verification in CI: all levels re-solved per build (already the pattern)
- Scenes: Home (map) · Level (board) · Daily · Settings · Shop-lite · Win card
- Save: local JSON (working) + optional Play Games cloud later
- Ad SDK: AdMob + AppLovin MAX mediation (P2 phase)
- Analytics: Firebase + GameAnalytics funnels from day 1

## 4. Roadmap (8 weeks to soft launch)
| Wk | Deliverable |
|---|---|
| 1-2 | Generator v3 (mechanics + shapes + bands), 1,200 levels, verifier |
| 3 | Core feel upgrade: Guidance long-press, residue dots, combo audio, FTUE ladder |
| 4 | Screens: Home/map, win card, daily, settings, achievements; streak+boosters |
| 5 | Polish pass (game-feel audit), hearts economy, difficulty badges, haptics |
| 6 | AdMob/MAX + IAP ($2.99) + analytics integration |
| 7 | Closed beta (10-20 testers), fix top 10 issues |
| 8 | Soft launch build: PH/ID stores, ASO listing, creatives |

Budget: ~$3-5k (store fees, ad test budget, contractor SFX/music polish).

## 5. Kill/pivot gates
- Soft-launch D1 < 35% after 2 iterations → core loop problem → pivot mechanics
- D7/D1 < 0.45 → meta/FTUE problem → fix before scaling
- CPI > $0.60 on TikTok IN after 20 creatives → creative problem, not game

## 6. New-game alternative (if we don't clone-adjacent)
Option B: "Untangle Rush" — same arrow DNA + real-time lane pressure (timed lane closures, puzzle-arcade hybrid, instant session 60-90s). Higher novelty, higher risk, worse for calm-brand ads. **Recommend Option A** — mechanic is proven at 100M+ DL scale, our edge is the wrapper + fairness.
