# StripLocal — EXIF Metadata Remover

**[Try it live →](https://naklitechie.github.io/StripLocal/)**

**Every photo you take is carrying a passenger.**

GPS coordinates. The exact timestamp. Your phone's model and serial number. Camera settings. Software you used to edit it. Sometimes a tiny embedded copy of the photo itself.

It's all sitting in the file, invisible, and it goes wherever the photo goes.

Most people find out about EXIF metadata right after they share something they didn't intend to share — a home address inferred from a photo's GPS tag, a device linked across accounts, a timestamp that contradicts a story.

And every online EXIF tool that offers to "fix" this? It receives your photo on a server first.

**StripLocal doesn't.** Drop your photos in. Get clean copies out. Nothing leaves the tab.

---

## What it strips

- 📍 GPS coordinates (location where photo was taken)
- 📅 Date & time taken
- 📱 Device model & serial number
- 📷 Camera settings (ISO, aperture, shutter speed, focal length)
- 👤 Author / copyright / artist fields
- 🔍 Software & editing history
- 🏷️ IPTC keywords & captions
- 📝 XMP / Adobe metadata
- 🌐 Embedded thumbnail preview

---

## How it works

No libraries. No WASM. No server.

The browser's native `Canvas` API is the entire engine. When you draw an image onto a canvas and re-export it as a blob, the canvas only captures pixel data — metadata has nowhere to go. It's discarded automatically.

One edge case handled: JPEG files often store rotation in EXIF rather than rotating the actual pixels. StripLocal reads the orientation tag before stripping, bakes the rotation into the canvas draw, then strips — so your photos come out upright.

```
File → FileReader → detect EXIF orientation → Canvas draw (with rotation baked in)
     → canvas.toBlob() → clean file (pixels only, no metadata) → download
```

---

## Use it

Open [`index.html`](index.html) directly in any modern browser, or serve it:

```bash
python3 -m http.server
```

No build step. No npm. No install. One file.

---

## Part of the NakliTechie series

| Tool | What it does |
|------|--------------|
| [**BabelLocal**](https://github.com/NakliTechie/BabelLocal) | Offline translation — 200 languages, NLLB model |
| **StripLocal** | EXIF metadata stripper — nothing leaves the browser |
| [**GambitLocal**](https://github.com/NakliTechie/GambitLocal) | Chess vs Stockfish — correspondence mode via URL |
| [**VoiceVault**](https://github.com/NakliTechie/VoiceVault) | Audio transcription — Whisper, offline-first |
| [**KingMe**](https://github.com/NakliTechie/KingMe) | English draughts — custom minimax AI, zero deps |
| [**SnipLocal**](https://github.com/NakliTechie/SnipLocal) | Background remover — RMBG-1.4, passport mode |
| [**Clacker**](https://github.com/NakliTechie/Clacker) | Split-flap display — browser-native, offline |
| [**Strait Command**](https://github.com/NakliTechie/strait-command) | Mine-clearing game in strategic waterways |
| [**Chokepoint**](https://github.com/NakliTechie/chokepoint) | Maritime tower defense — hold the strait |
| [**PredictionMarket**](https://github.com/NakliTechie/PredictionMarket) | Prediction market simulator — Parimutuel & LMSR |
| **PDFLOcal** | PDF editor — merge, split, rotate, annotate |
| **RangeLocal** | Missile range simulator — interactive globe & map |
| [**3D Tic-Tac-Toe**](https://github.com/NakliTechie/3d-tic-tac-toe) | 3D tic-tac-toe — 3×3×3 to 5×5×5, minimax AI |

---

**Built by [Chirag Patnaik](https://github.com/NakliTechie)**

## Supported formats

JPEG · PNG · WebP — anything the browser's native image decoder can handle.

---

## Launching a new tool in this series

Checklist to run through before and after the first push:

1. **Set git author** — `git config user.name "Chirag Patnaik"` before committing
2. **README live link** — add `**[Try it live →](https://naklitechie.github.io/<RepoName>/)**` right after the h1
3. **Footer attribution** — `index.html` footer should read "NakliTechie" and link to `https://github.com/NakliTechie/<RepoName>`
4. **Enable GitHub Pages** — after pushing, run:
   ```bash
   gh api repos/NakliTechie/<RepoName>/pages -X POST --field 'source[branch]=main' --field 'source[path]=/'
   ```

---

## License

MIT
