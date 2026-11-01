# 2026-11-01 — revert of failed bulkhead visibility overlay

- User tested the prior visibility change and reported that it changed bulkhead/wall color from grey to black but did not prevent seeing through walls.
- Before reverting, backed up the current build to `backups/2026-11-01_before-reverting-failed-visibility-overlay.html`.
- Removed the ineffective `drawBulkheadOcclusion` overlay and its render call, restoring the prior wall/partition rendering colors.
- No claim that wall-based visibility is fixed; the correct solution needs actual render clipping/occlusion tied to the character's compartment and open/closed passages.
- Browser verification of this revert and further visibility work remains pending.
- Revert commit: 334078cb88a993673ede2bf9db21bd1a2ebda286
