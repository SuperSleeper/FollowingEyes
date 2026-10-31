# Following Eyes

Halloween eyes that watch you. Open the page on a phone or laptop, prop it in a window or a decoration, and the eyes follow whoever moves in front of the camera.

**Live page:** https://supersleeper.github.io/FollowingEyes/

## Styles

| Style | Look |
|---|---|
| Eyes | A pair of bloodshot eyes with glowing orange irises |
| Pumpkin | A jack-o'-lantern whose eyes follow you |
| Cyclops | One huge green eye |
| Inferno | A burning eye with flames pouring off the iris, storm clouds rolling toward you, lightning, and a roaring fire sound |

## How to use

1. Open the live page in Chrome (Android or desktop).
2. Tap **Allow** when the browser asks for the camera.
3. Pick a style and tap **Start**. The page goes fullscreen and keeps the screen awake.
4. Tap the screen anytime to bring the settings back.

## Settings

| Control | What it does |
|---|---|
| Sensitivity | How much movement it takes to catch the eyes' attention |
| Flip left/right | Use this if the eyes look away from you instead of at you |
| Flip top/bottom | Use this if the eyes look up when you crouch, or the phone is mounted upside down |
| Camera view | Shows a small motion preview for tuning |
| Switch camera | Cycles through cameras (useful on foldables like the Galaxy Z Fold with two front cameras) |
| Fire sound / Volume | Inferno's roar. Sound starts after you tap, as browsers require. |

## How it works

- The front camera is sampled at 64×48 pixels. Each frame is compared to the previous one, and the center of the changed pixels is where the eyes look.
- It tracks **motion**, not faces. That makes it work at porch distance, but someone standing perfectly still is "lost" until they move again.
- The fire sound is generated live with the Web Audio API: low-passed brown noise for the roar, filtered noise for the hiss, and random noise bursts for crackles. No audio files.
- Everything runs in one HTML file with no libraries.

## Code layout

Everything lives in `index.html`. The script is split into numbered sections, with each style's code kept together:

| Section | What it holds |
|---|---|
| 1. Setup | Canvas, page elements, shared settings |
| 2. Settings panel | Buttons and sliders |
| 3. Camera | Opening and switching cameras, error messages |
| 4. Motion tracker | Finds where movement is in the camera image |
| 5. Gaze & blink | Where the eyes look, pupil size, blinking |
| 6. Eyes | `classicEye()` (shared eyeball) and the two-eye style |
| 7. Pumpkin | Jack-o'-lantern body, grin, and eyes |
| 8. Cyclops | One large eye |
| 9. Inferno | 9a fire particles, 9b storm sky, 9c fire sound, 9d the eye |
| 10. Main loop | Style registry (`STYLES`) and the per-frame update |

**To add a style:** add a button with `data-s="name"` to the panel, then add an entry to `STYLES` with a `draw(scene)` function. `activate()` and `deactivate()` are optional.

## Privacy

Nothing is recorded, stored, or sent anywhere. Camera frames are processed in the browser and discarded.

## Tips

- Give visitors some light. A porch light is enough.
- Aim away from wind-blown decorations and moving trees, or the eyes will watch those instead.
- Phone speakers lose the low roar. A Bluetooth speaker makes Inferno much louder.

## Troubleshooting

| Problem | Fix |
|---|---|
| No camera prompt | The page must be opened from its `https://` address. Opening the downloaded file from My Files or Downloads will not work. |
| "Camera is blocked" | Tap the icon left of the address bar → Permissions → Camera → Allow, then reload. |
| Eyes don't react | Tap **Switch camera**, raise Sensitivity, and check Camera view for movement. |

## Run your own copy

Fork this repo, then enable **Settings → Pages → Deploy from a branch → main / (root)**. Your copy will be at `https://<your-username>.github.io/FollowingEyes/`.
