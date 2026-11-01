# Bombies

A zombie survival shooter that runs in the browser. Open `index.html` through any web host, or publish it free with GitHub Pages.

## Put it on GitHub Pages
1. Sign in at github.com and create a new **public** repository named `bombies`.
2. Click **uploading an existing file**, drag in everything from this folder (`index.html`, `manifest.json`, the icons, `.nojekyll`), and click **Commit changes**.
3. Go to **Settings > Pages**. Under **Build and deployment**, set Source to **Deploy from a branch**, pick **main** and **/(root)**, and click **Save**.
4. Wait a minute or two. Your game will be at `https://YOUR-USERNAME.github.io/bombies/`.

## Play on iPad or iPhone
1. Open that address in **Safari**.
2. Tap **Share** (square with an arrow) > **Add to Home Screen** > **Add**.
3. Start Bombies from the new icon. It opens full screen, like an app.

Tap the screen once at the start so sound can play. Scores and settings save on each device.

## Updating
Upload a new `index.html` to the same repository (it replaces the old one). Changes show up a minute or two later; pull down to refresh, or remove and re-add the home-screen icon if it looks stale.

## Photoreal conversion (visuals + sound only — gameplay, menus, settings, loadout, waves, and controls are unchanged)

### Photographic textures (`textures/`)
- Zombie and hero faces: photographic face plates (`bombie-face.jpg`, `hero-face.jpg` — crops of the Dead Zone portraits), bent to the head shape with a feathered rim so the photo fades into the head instead of ending in a hard edge. One continuous photo per face, no tiled patches. The procedural mouth is hidden on plated faces.
- Cars: drivable cars keep their clean finish; parked and wreck cars use the rusted-panel photo (`rust.jpg`).
- Buildings: weathered brick facade photo (`facade.jpg`).
- Ground and roads: cracked asphalt photo (`asphalt.jpg`); garage floor and alley sidewalk use stained concrete (`concrete.jpg`).
- Sky: park map uses a blue sky with cumulus clouds (`day-sky.jpg`); the dusk city/garage map uses a storm-cloud panorama (`storm-sky.jpg`).
- Guns: the rifle, shotgun, and magnum viewmodels and held guns use worn gunmetal (`gunmetal.jpg`).
- Icons: `icon-180/192/512.png` are a photographic Bombie portrait crop (reads at small sizes, no text).

### Reflections (the RTX-on look, not literal path tracing)
True ray-traced path tracing is not available in a Three.js web game, so reflections use what Three.js can do: the garage floor and park lake keep the game's true planar mirror reflection; city roads are low-roughness glossy surfaces lit by a sky environment map; four reflective puddles sit on the asphalt outside the garage; car paint and gunmetal are glossy materials lit by the same sky environment map, so paint and metal pick up the sky. Puddles reflect the sky via the environment map, not the scene.

### Sounds (`sounds/`) — cut from Danny's own recordings
The gun sounds are real recorded gunshots cut from Danny's two voice-note recordings (`Voice_261028_161724_51_ub91.m4a`, `Voice_261028_161925_52_djy9.m4a`), not from any sound library and not from the earlier video:
- `rifle.mp3` (1.59 s): voice note 2, 2.81–4.40 s — rifle crack with echo tail.
- `shotgun.mp3` (1.85 s): voice note 2, 17.25–19.10 s — loudest, bassiest shot, used as-is.
- `magnum.mp3` (0.89 s): voice note 2, 33.71–34.60 s — short dry pistol crack.
- `boom.mp3` (1.83 s): voice note 1, 18.59–19.70 s, pitched to 0.6× and lowpassed at 500 Hz for explosion weight.
All four are peak-normalised and wired into the existing sound triggers with procedural fallback if a sample fails to load. Reload clicks and shotgun pump sounds stay procedural: neither the voice notes nor the video contain clean reload/pump segments.

### Honest limits
- Textures make surfaces photographic; they do not change geometry. Bodies, garments, and cars keep their modelled shapes underneath (box/cylinder forms stay boxy where the original modelled them so).
- Bodies and garments have no UVs, so they keep their detailed procedural painting; ears stay procedural skin.
- Trees keep procedural canopies (no UVs for a foliage photo; rebuilding them risks the park layout and colliders).
- There are no standalone debris or scrap piles in this game; the scrap standard lands on the rust-textured wreck cars.
- The park lake has planar reflection plus animated ripples and sparkle, but no droplet splash particle system.
- There is no SMG in this game (rifle, shotgun, magnum only), so SMG items in the weapon/sound briefs have no landing point here.
- At alley-card size and dusk lighting, faces read as game faces rather than photographs; the photographic read at close range is not decisively demonstrated by screenshots, though the plate system (photo loads, attaches to zombies and hero, feathered rim, mouth hidden on plated faces) is in place.
- In headless verification, the magnum and shotgun voice-note samples were proven playing live; the rifle and boom samples are verified loading and decoding with identical wiring, but their live playback was not captured (the rifle never fired via touch holds in those runs, and grenade explosions produced no sound in the fingerprint window — mechanism not established). Reload and pump sounds are procedural by design.
