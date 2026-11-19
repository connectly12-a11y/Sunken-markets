# Sunken Market: Asset Prompts

I'm not familiar with Lux3D's exact interface or prompt syntax, so these are written as plain text-to-3D prompts. Adapt the wording to whatever fields it exposes (style, negative prompt, image-to-3D, etc.).

## How to drop files in

1. Generate each model and export as **.glb**.
2. Put the files in a `models/` folder next to `index.html` using the exact filenames below.
3. Serve the folder over HTTP (browsers block GLB loading from `file://`):
   `python3 -m http.server 8000` then open http://localhost:8000
4. The start screen reports how many custom models loaded. Missing files fall back to built-in placeholders, so you can add them one at a time.

**You don't need to match scale or pivot.** The loader auto-resizes each model so its largest dimension hits the `size` in the `ASSETS` manifest, and re-centers it (bottom-center for props, center for items). Only requirements: **Y-up**, and for the player, **front facing +Z**. To tune size, edit `size` in `ASSETS` at the top of the script.

## Shared style block (prepend to every prompt)

> Stylized dreamy underwater game asset, soft rounded shapes, hand-painted pastel textures, gentle bioluminescent glow accents in teal, pink and violet, slightly chunky proportions, single object, centered, neutral pose, clean low-to-mid poly topology, game-ready, no background, no base plate, no text.

Keep the same style block and, if Lux3D supports it, the same seed or style reference for every asset so they look like one set.

## Environment

| File | Prompt | Notes |
|---|---|---|
| `coral_branch.glb` | Branching staghorn coral cluster, pink coral with pale glowing tips, five to seven curved branches rising from a small rocky base | Used ~40x at varied scale |
| `coral_brain.glb` | Rounded brain coral dome in mint green with winding ridged grooves, soft teal glow in the grooves | Low and wide |
| `coral_fan.glb` | Large sea fan coral, violet lattice fan on a thin stem, delicate translucent edges, soft purple glow | Flat shape is fine |
| `shell.glb` | Small pearly spiral seashell, pale pink and cream with iridescent sheen, lying on its side | Scattered ~60x on the floor; keep it simple |
| `statue.glb` | Ancient weathered stone merchant statue, robed figure with one arm raised holding out a bowl, green moss and tiny barnacles, worn smooth by the sea | Standing, arms away from body |
| `archway.glb` | Ruined stone archway market gate, two thick pillars joined by a rounded arch, carved wave patterns, coral growth and moss, a glowing teal gem set in the keystone | Walk-through: open space under the arch |
| `platform.glb` | Circular stone market stall platform, low wide pedestal with carved rim, faint glowing teal rune ring around the top edge, small cracks and algae | Flat top; the game treats the top as ground you glide over |

## Player

| File | Prompt | Notes |
|---|---|---|
| `player.glb` | Small friendly underwater explorer, rounded diver suit in ocean blue with gold trim, glowing teal visor, little swim fins, arms slightly back as if gliding, stylized game character | **Front must face +Z.** If it includes a swim or idle animation, the first clip plays automatically |

## Collectibles (the five treasures)

| File | Prompt | Notes |
|---|---|---|
| `item_conch.glb` | Golden conch shell, polished gold spiral with warm amber glow inside the opening, ornate ridges | Journal name: Golden Conch |
| `item_pearl.glb` | Giant luminous moon pearl, smooth pearlescent sphere with soft blue-white inner glow, tiny silver cradle ring | Journal name: Moon Pearl |
| `item_compass.glb` | Antique brass nautical compass with open lid, cracked glass, a glowing red needle, teal engraved markings | Journal name: Brass Compass |
| `item_bell.glb` | Small sunken ship bell in tarnished gold bronze, rounded bell shape, barnacles around the rim, warm glow from inside | Journal name: Sunken Bell |
| `item_lantern.glb` | Glass lantern with a bright cyan flame floating inside, slim iron frame and cap, soft light bleeding through the glass | Journal name: Glass Lantern |

Make the collectibles a bit brighter and more saturated than the environment; they're what the player is hunting for, and the code adds a halo, point light and beam around them.

## Tips

- Generate the three corals and the shell first; they're the most visible and repeated.
- Avoid very high poly counts (aim under ~20k tris per environment piece, under ~10k for items). There are 100+ scatter instances.
- If a model's materials look too dark underwater, give it an emissive map or ask for "soft glow accents"; the scene lighting is cool and moody by design.
- To change what an item is called or where it sits, edit the `ITEMS` array in `index.html`.
