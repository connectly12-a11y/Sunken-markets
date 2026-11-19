# Sunken Market

A dreamy, browser-based 3D swimming exploration game. A drowned bazaar still glows beneath the tide, and five lost treasures once traded here. Swim the ruins, follow your journal, and bring them home.

Built for the **Manycore Aholo Global 3D AI Hackathon** ("Play in 3D, Create with Aholo"). Every major 3D model in the game (coral, shells, statues, archways, platforms, the five treasures and the player character) is generated with **Aholo Lux3D**.

**Play it:** https://bencoy09.github.io/sunken-market/ (desktop or phone, no install)

## Gameplay

- Swim a single glowing underwater market and find **5 treasures**: Golden Conch, Moon Pearl, Brass Compass, Sunken Bell, Glass Lantern.
- Gentle guidance only: a journal with a riddle-style hint per treasure, a compass arrow toward the nearest uncollected one, and faint light beams you can spot through the fog.
- Collect all five to wake the market.

## Controls

| Input | Desktop | Mobile |
|---|---|---|
| Swim | W A S D | Left virtual stick |
| Look | Mouse | Drag anywhere else |
| Rise / sink | Space / Shift | ▲ / ▼ buttons |
| Journal / mute | J / M | n/a |

Swimming is momentum-based: you ease into speed and glide to a stop. Forward follows where the camera looks, so look up and swim up.

## How Aholo Lux3D is used

All hero assets are generated from text prompts with Lux3D (https://lux3d.aholo3d.com), exported as GLB, and dropped into `models/`. The exact prompts are in [`ASSET_PROMPTS.md`](ASSET_PROMPTS.md), sharing one style block so the set looks cohesive.

The game loads each GLB, then **auto-scales it to a target size and re-pivots it**, so whatever scale the generator exports at works without hand-tuning. If a GLB is missing, a simple procedural stand-in is used so the game always runs.

| Asset | File |
|---|---|
| Branching, brain and fan coral | `coral_branch.glb`, `coral_brain.glb`, `coral_fan.glb` |
| Shell | `shell.glb` |
| Statue, archway, platform | `statue.glb`, `archway.glb`, `platform.glb` |
| Player character | `player.glb` |
| Treasures | `item_conch.glb`, `item_pearl.glb`, `item_compass.glb`, `item_bell.glb`, `item_lantern.glb` |

The start screen reports how many custom GLB models loaded.

## Run locally

Browsers block GLB loading from `file://`, so use any static server:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

No build step. Three.js (r160) loads from a CDN, so an internet connection is required.

## Project structure

```
index.html          the whole game (Three.js, no build step)
models/             Lux3D-generated .glb files
ASSET_PROMPTS.md    prompts used to generate each model
```

Tuning knobs (swim feel, bloom, scatter density) are in the `CONFIG` block at the top of the script; item positions and hints are in `ITEMS`.

## Tech

Three.js, GLTFLoader, UnrealBloomPass, procedural caustics and light shafts, WebAudio ambience. Single HTML file.

## License

MIT, see [LICENSE](LICENSE). Generated 3D assets are subject to Aholo's terms of use.
