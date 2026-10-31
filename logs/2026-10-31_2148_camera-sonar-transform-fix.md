# Camera / sonar coordinate fix — 2026-10-31 21:48 (+03:00)

## Safety checkpoint
- Before-edit backup created: `backups/2026-10-31_2148_before-camera-distortion-fix.html`
- Backup commit: `9c62f6598af804df209282d9540d02d9737403f2`
- Source file SHA before edit: `28ea6b2a57b0c32e3c39057a42403ddf206b8b02`
- Work branch: `recovery/restore-from-main-2026-10-31`
- `main` was not modified.

## User-observed issue
At 64% zoom, objects and cave geometry appeared increasingly displaced relative to one another with distance from the diver/player. The issue was reported both while walking and while using the helm; the submarine had not moved between the screenshots.

## Code inspection
- The main world render applies a centered `viewZoom` transform and then the camera translation.
- `drawDark()` applies the matching zoom and camera transform.
- `drawBeaconCover()` also applies the matching zoom and camera transform.
- `drawSonar()` was the exception: it restored the main world context and then applied only `translate(-camX, -camY)`, omitting the centered `viewZoom` scale. Its low-resolution sonar triangles and echoes could therefore drift relative to zoomed cave geometry, with the displacement growing away from the screen center.

## Change made
Created a separate candidate build, without overwriting the existing working file:
- `Barotrauma_Dugong_World_Repair_camera-fix.html`
- Commit: `fb34ff4e5f01a040bced1618525e032d483e8f03`
- New blob SHA after fetch verification: `b44cea9354813b63523097b49b00c4a8b18b4096`

In `drawSonar()`, replaced the camera-only translation with the same transform order used by the world and the other overlays:
1. translate to screen center;
2. scale by `viewZoom` (or 1 outside play);
3. translate back from screen center;
4. apply camera offset and shake.

## Verification performed
- Created and fetched the candidate file again from the recovery branch.
- Confirmed the new transform is present and the old camera-only transform is absent.
- Inspected `drawBeaconCover()`; it already uses the correct centered zoom transform.
- No browser gameplay test or JavaScript parser/syntax test was available in this run. Therefore this is a targeted code-level fix candidate, not a confirmed in-game resolution.

## Next test
On the phone, open the candidate build, start a level, set zoom to 64%, and compare the alignment of cave walls and sonar echoes near the center and far from the center. Repeat while walking and while seated at the helm. If the same displacement remains when sonar is not active, continue tracing the world/camera transform and coordinate input separately; do not assume this sonar fix resolves every camera issue.

## Scope kept separate
Camera centering on the submarine while using helm/guns remains a separate task and was not changed here.
