# Sunken Market — performance pass

This update keeps the same game, controls, five collectibles, journal, compass, and fallback models, but reduces the default rendering workload.

## What changed
- Disabled the full-screen bloom post-processing chain by default.
- Reduced the renderer pixel ratio (0.9 on touch devices, 1.25 maximum on desktop) and disabled MSAA.
- Reduced the sea-floor mesh from 130×130 segments to 76×76.
- Reduced marine-snow particles from 1,100 to 280 on desktop / 140 on touch devices.
- Reduced light-shaft count and cone geometry.
- Reduced coral and shell scatter and fish count.
- Reduced collectible point-light intensity/range.
- Reused camera vectors and avoided updating the camera projection matrix unless its FOV changes visibly.
- Capped touch-device rendering at approximately 30 FPS to avoid overheating and uneven frame pacing.

## Important
This is a source-level optimization pass. The live Vercel deployment has not been device-profiled from here, so test it on the target phone after deploying. If it still stutters, the next step is to profile the actual GLB files and convert repeated coral/shell meshes to instanced rendering.

## Files
- `index.html` — optimized game
- `README.md`, `ASSET_PROMPTS.md`, `LICENSE` — retained from the supplied project
