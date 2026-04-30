# GLYPH — ASCII Portrait Generator

**Canvas-based ASCII glyph field generator for mixed media.**  
Drop any image. Watch it come alive as a field of cycling glyphs. Control everything. Record it. Export it.

**[→ Open in browser](https://glyph-gen.vercel.app)**

---

## What it does

GLYPH converts portraits and images into real-time ASCII/glyph particle simulations. Every character is a living particle — spring physics, multi-frequency oscillators, wandering rogue glyphs, cursor interaction. The result looks like data leaking out of a terminal that forgot how to stop.

Built for mixed media artists, creative coders, zine makers, and anyone who wants their visuals to feel like they were decoded from somewhere else.

---

## Features

- **12,000 glyph particles** — each with independent physics, character cycle, and color cycle
- **4 character sets** — ALL (86 glyphs), ALPHA, NUMS, SYMBOLS — switchable live
- **6-color palette** — chartreuse, phosphor green, cyan, sky cyan, seafoam, teal
- **Spring physics** — mass, damping, multi-frequency oscillators, idle twitches
- **Wanderer glyphs** — rogue characters orbit the image perimeter in accent colors
- **Cursor interaction** — magnetic force field disturbs the glyph field on hover
- **25+ live controls** — every parameter tweakable in real time via side panel
- **MP4 / WebM export** — record direct from canvas with 3-second pre-roll countdown
- **Frame export** — PNG snapshot at any moment
- **Hue shift** — rotate the palette across the full spectrum
- **Works on any image** — JPG, PNG, WEBP — drag, click, or paste

---

## Use it

### Online
[glyph-gen.vercel.app](https://glyph-gen.vercel.app) — no install, no account, runs in browser

### Local
```bash
git clone https://github.com/ripfarhan/asciigenerator.git
cd asciigenerator
python -m http.server 3000
# open http://localhost:3000
```

No dependencies. No build step. One HTML file.

---

## Controls

Open the **▶ CONTROLS** panel on the right edge.

| Section | Controls |
|---|---|
| **Render** | Trail Fade, Glyph Size, Glow Blur |
| **Glyphs** | Char Speed (cycle rate), Color Speed |
| **Motion** | Amplitude, Breathe Speed, Twitch Rate, Twitch Strength |
| **Cursor** | Force Radius, Force Strength |
| **Wanderers** | Speed Multiplier, Impulse |
| **Display** | Scanlines, Vignette, Flicker, Hue Shift |
| **Toggles** | Reactive mode, Polarity (invert image) |
| **Charset** | ALL / ALPHA / NUMS / SYM |
| **Density** | HIGH / MED / LOW particle density |
| **Actions** | New Image, Export Frame, Rec MP4, Reset Defaults |

---

## Recording

1. Set duration with the **REC DURATION** slider (3–30 seconds)
2. Hit **[ ● REC MP4 ]**
3. Yellow **3 → 2 → 1** countdown — get your cursor in position
4. Red countdown runs — captures live from canvas
5. File auto-downloads as `.mp4` (Chrome) or `.webm` (Firefox/others)

---

## Modify it

Everything is in `index.html`. The architecture:

```
Canvas 2D renderer
  ├── Batched fillText() per color bucket (minimises fillStyle changes)
  ├── shadowBlur per-glyph glow
  └── rgba fade quad for motion trails

CPU Physics (Float32Arrays)
  ├── Spring forces + damping per particle
  ├── Multi-frequency oscillators (freqA/B/C + phaseA/B/C)
  ├── Per-particle char cycling (charAge / charPeriod)
  ├── Per-particle color cycling (colorAge / colorPeriod)
  └── Wanderer orbit system

cfg object
  └── All live parameters — modify defaults here or wire new sliders
```

To add a new control: add a slider to the panel HTML → `bindSlider('id', 'val-id', 'cfg-key', formatter)` → use `cfg.yourKey` in the render loop.

---

## Related

- **[CRT GEN](https://github.com/ripfarhan/crtgenerator)** — WebGL GPU phosphor particle version of the same concept

---

## Tech

- Pure Canvas 2D (no libraries)
- `canvas.captureStream()` + `MediaRecorder` for video export
- `Float32Array` typed arrays for all physics state
- Bayer 4×4 ordered dithering for image sampling
- Color-bucketed render pass to minimize fillStyle switches

---

## License

MIT — do whatever you want with it.

---

*Made with a terminal and too much time.*
