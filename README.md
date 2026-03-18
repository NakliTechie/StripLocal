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

## Part of the NakliTechie browser-native tools series

StripLocal is the first in a series of single-file tools built around one question:

> *"Why are you uploading that to a server?"*

Every tool in the series runs entirely in the browser. No accounts. No cloud. No tracking. The target user isn't paranoid — they're just a professional who'd prefer their passport scans and medical notes didn't pass through a random startup's S3 bucket.

---

## Supported formats

JPEG · PNG · WebP — anything the browser's native image decoder can handle.

---

## License

MIT
