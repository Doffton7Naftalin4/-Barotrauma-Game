# 2026-11-01 — Diver inertia, tool alignment, and breach flow

## Starting point and rollback
- Source: `Barotrauma_Dugong_BreachRepair_SwimTurnFix.html`
- Source blob SHA: `39d281ca789dcc35cfaf5453d7002770710207dd`
- Exact pre-change backup: `backups/2026-11-01_before-inertia-tool-leakflow-fix.html`
- Backup commit: `d13baa2658a45dcc930ecf5869e9d3dafa95977b`
- The previous build was not overwritten; this change is a separate HTML build.

## Changes
1. Movement retains momentum more naturally: lower drag, moderated acceleration, and exponentially smoothed body turning. Direction changes therefore take time and velocity carries through the turn.
2. Harpoon model and flashlight cone now use the same smoothed body angle, so they rotate with the diver instead of independently snapping to the movement input.
3. Breach particles use a directional flow vector. Ceiling openings spray into the room downward, floor openings upward, and side-wall openings horizontally inward; the flow is no longer hard-coded to an upward-only animation.

## Checks and limits
- Inline JavaScript parsed with `new Function`: PASS.
- String-level checks confirm all intended replacements were applied: body angle target follows movement, momentum and smoother turning, breach flow vector based on opening surface, particle stream follows leak direction, rotating flashlight cone, harpoon model rotates with diver.
- No real browser/gameplay test was available in this step. Movement feel, light visibility, harpoon alignment, and breach directions still need in-game verification.


## 2026-11-01 follow-up — impact-localized breach placement
- Reported issue: hitting the submarine side while aligned with a ballast compartment could create a breach in the engine room; hitting the bottom of the ballast could place a breach at the wrong vertical location.
- Created a fresh exact backup before editing: `backups/2026-11-01_before-impact-compartment-breach-fix.html` (source blob `e15935e2f0182edaea5fc9edcc33a0ab7c16df46`, backup commit `ba01ac09f9953742501e8c2ace0164f455301d2f`).
- Added `subHitPoint(x,y)`, which estimates the local contact point from terrain cells overlapping the submarine hull.
- Horizontal collisions now pass the detected local X/Y contact point to breach creation instead of using a fixed X, Y=0, and a random top/bottom choice. This lets the existing compartment resolver select the deck/room near the actual contact.
- Preserved the previous build unchanged as `Barotrauma_Dugong_BreachRepair_InertiaToolsLeakFlow.html`; the candidate fix is a separate file: `Barotrauma_Dugong_BreachRepair_ImpactBreachFix.html`.
- JavaScript syntax check using `new Function`: PASS (1 inline script).
- No browser/gameplay collision test was available. The placement fix is a candidate and still needs user testing, especially side impacts beside both ballast rooms and bottom impacts.
