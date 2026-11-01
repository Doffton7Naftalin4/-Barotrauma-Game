# 2026-11-01 — Slow passive player health regeneration

## Backup
- Source build: `Barotrauma_Dugong_BreachRepair_HullIntegrityRestore.html`
- Backup: `backups/2026-11-01_before-player-slow-regeneration.html`
- Backup commit: `ff490beac43933d6033feb2f11991db921657b7d`

## Change
User clarified that "health" means the diver/player, not submarine hull integrity.
- Reduced passive player health regeneration from 1.5 health/second to 0.05 health/second (30 times slower).
- Passive regeneration still requires oxygen above 30 and remains disabled while infection or poisoning is active.
- Medical items and explicit healing amounts were not changed.

## New build
- `Barotrauma_Dugong_BreachRepair_PlayerSlowRegen.html`
- Commit: `bba9e70afae1305ae725486bff7a42e2bb18d1e0`

## Validation
- JavaScript syntax check with `new Function(script)`: PASS.
- Browser gameplay test: NOT RUN.
