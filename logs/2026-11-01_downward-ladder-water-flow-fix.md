# Central ladder water flow — downward speed adjustment

Date: 2026-11-01

## Report
User tested the central hatch/ladder water transfer and confirmed it works, but downward transfer is too slow: water pools above an open hatch and trickles down, while upward transfer appears normal.

## Backup before change
The current HTML was unchanged since the earlier audit backup:
- `backups/2026-11-01_before-central-ladder-water-audit.html`
- https://github.com/Doffton7Naftalin4/-Barotrauma-Game/blob/recovery/restore-from-main-2026-10-31/backups/2026-11-01_before-central-ladder-water-audit.html

## Change
Updated `Barotrauma_Dugong_BreachRepair_PlayerSlowRegen.html`:
- Kept upward water-transfer rate at `0.70`.
- Increased downward transfer rate through the central ladder shaft to `3.5` (5x the previous rate).
- Kept the transfer based on a shared pre-transfer snapshot and applied equal-and-opposite deltas, so the water moved between the two rooms remains conserved by this connection.
- Did not change side-door flow, pumps, leaks, character movement, or breach placement.

## Verification status
- Patch applied to the existing project branch.
- Browser gameplay test has **not** been performed by the assistant. The user must verify the downflow visually and confirm that upward flow and overall flooding still behave as expected.
- If downward flow is still too slow or becomes too abrupt, tune the ladder-only rate rather than changing the general water-flow function.

## Build
- Current build: `Barotrauma_Dugong_BreachRepair_PlayerSlowRegen.html`
- Commit: `98f39f1dfbb159369e603f4c210cad502d542d2e`
- New blob: `88f3971729580a0ad747a217444c895171500b00`
