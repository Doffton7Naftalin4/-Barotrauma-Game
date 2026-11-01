# 2026-11-01 — submarine bulkhead visibility fix

- Before editing, saved the current HTML build to `backups/2026-11-01_before-submarine-wall-visibility.html`.
- Updated `Barotrauma_Dugong_BreachRepair_PlayerSlowRegen.html` on branch `recovery/restore-from-main-2026-10-31`; `main` was not changed.
- Added a final opaque overlay for internal vertical bulkheads so sprites behind a wall are hidden. Existing doorway openings remain open; closed doors and ballast-room partitions remain opaque.
- Scope intentionally limited to rendering. Physics, flooding, breach logic, and movement were not edited.
- Static checks: patch anchors matched exactly once; updated source includes the occlusion function and its render call.
- Browser gameplay test: **pending user verification**. Please check visibility across a closed bulkhead and through an open doorway.
- Backup commit: c0a5a518c3f2d0a7c3e2f3a406b04e8b9f591f71
- Build update commit: 28c0f7af37a4081a3b78c3ea7652325a00d53f45
- New build blob SHA: df87ad8b2fe4290de57a1793c36e1f89dc94cb38
