# Arrow Quest — Project Board (GitHub)

**Repo:** https://github.com/imraxy/arrow-quest
**Board equivalent:** Milestones M1–M4 + labels (phase/priority/size). All 26 issues assigned.
*Note: GitHub Projects v2 board needs a `read:project` token scope — add it later at https://github.com/settings/tokens if you want the kanban view; milestones + labels already give full tracking.*

## Milestones (= sprints)

### M1 — Generator v3 + 1,200 levels *(weeks 1-2)* — issues #1-6
- #1 Godot project structure + CI (P0)
- #2 Commit v2 game code (P0)
- #3 Generator mechanics: walls/double/locked/portals/rotators/ice/bombs/dark (P0, L)
- #4 Shape masks (P1)
- #5 Difficulty banding + 12 worlds (P0)
- #6 Daily seeding (P1)

### M2 — Core feel + FTUE *(weeks 3-4)* — issues #7-12
- #7 Long-press Guidance (P0)
- #8 Residue dots + combo audio (P1)
- #9 FTUE ladder L1-15 (P0)
- #10 Haptics + settings (P1)
- #11 Fit-to-screen + pan isolation (P0)
- #12 Win card + stars (P1)

### M3 — Meta + social *(weeks 5-6)* — issues #13-20
- #13 Home + world map (P0)
- #14 Hearts + return-to-origin fail flow (P0)
- #15 Streak + boosters (P0)
- #16 Daily screen + trophies (P1)
- #17 Achievements (P2)
- #18 Async duels (P1)
- #19 Daily percentile league (P1)
- #20 Share cards (P2)

### M4 — Monetization + soft launch *(weeks 7-8)* — issues #21-26
- #21 AdMob/MAX (P0)
- #22 Remove Ads $2.99 + coin shop (P0)
- #23 Analytics funnels (P0)
- #24 ASO + creatives (P0)
- #25 Playable ad build (P0)
- #26 Soft launch PH/ID (P0)

## Working agreements
- One issue = one branch = one PR; PR closes issue via "Closes #N"
- Every PR: E2E test suite green before merge
- APK artifacts per build; raxy playtests each M-gate on device
- Kill gates (from COMPETITIVE_PLAN.md §5) reviewed at M3 and M4
