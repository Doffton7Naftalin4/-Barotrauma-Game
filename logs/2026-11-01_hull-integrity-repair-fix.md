# 2026-11-01 — Restore hull integrity after breach repair

## Starting point and backup
- Source build: `Barotrauma_Dugong_BreachRepair_ImpactBreachFix.html`
- Source blob SHA: `eab1b3ef73a0ccbb43d61328d69ebcdb3c225651`
- Backup: `backups/2026-11-01_before-hull-repair-restore.html`
- Backup commit: `ef5d31b29546068cd49482d758f0d43fae3c14d3`
- Working branch: `recovery/restore-from-main-2026-10-31`

## Reported issue
Welding a breach removed the leak, but did not restore the submarine hull integrity bar.

## Changes
- `hurt(n)` now returns the actual integrity loss after hull-upgrade and submarine-armor reductions; existing damage behavior is preserved.
- A breach created by a collision records that actual hull damage.
- When welding fully closes that breach, its recorded damage is restored to hull integrity, capped at 100. Partial welding does not restore integrity early.
- The existing breach location, water-flow direction, fuel use, and welding effects are left unchanged.

## New build
- `Barotrauma_Dugong_BreachRepair_HullIntegrityRestore.html`
- Commit: `63a78c57f90103217cbd84ef628b9a2f01480bd0`

## Validation
- JavaScript syntax check using `new Function(script)`: PASS.
- Browser gameplay test: NOT RUN. Verify that hull integrity drops after a collision and returns by the same amount only after that breach is fully welded.
