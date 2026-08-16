# Free Toolkit

Small, single-file web tools that run entirely in your browser. No ads, no sign-up, no
upload. Open one in a tab, or download the file and run it offline forever.

**Live:** https://msubham06.github.io/Free-Toolkit/

---

## 1. Tools in the toolkit

| Tool | Link | What it does |
|---|---|---|
| **QR Forge** | [Open](https://msubham06.github.io/Free-Toolkit/tools/qr-forge.html) · [File](tools/qr-forge.html) | Turns any link or text into a QR code. **Basic** mode gives a clean, maximally scannable code in one step. **Custom** mode opens up solid/linear/radial fills, four module shapes, four eye-frame and four eye-centre styles, separate eye colours, quiet zone, error correction, and a transparent logo with live scan-safety checking. Exports PNG, SVG, or straight to clipboard. |
| **Frame Grab** | [Open](https://msubham06.github.io/Free-Toolkit/tools/frame-grab.html) · [File](tools/frame-grab.html) | Pulls stills out of video files. Frame-by-frame scrubbing at the video's real detected frame rate, sharpest-frame detection, crop ratio presets, brightness/contrast/saturation with live preview, and a capture tray. Exports as JPG/PNG/WebP — one at a time, as separate files, as a ZIP, or as a single contact sheet. |

---

## 2. Tools to add

Ordered by how commonly people need them — most-used at the top, niche at the bottom.
Tick them off as they ship.

| # | Tool | What it does | Notes |
|---|---|---|---|
| 1 | **Image Compressor** | Drop images, pick a quality level, get smaller files. Shows before/after size and a side-by-side preview so you can see what the compression cost you. Batch mode with ZIP export. | Canvas re-encode. Engine already exists in Frame Grab. |
| 2 | **Image to PDF** | Combine one or many images into a single PDF. Page size, orientation, margin, and drag-to-reorder. | JPEG bytes embed directly into a PDF with no re-encoding. ~150 lines. |
| 3 | **PDF to Image** | Turn each page of a PDF into a PNG or JPG at a chosen resolution. Select pages or export all as a ZIP. | Needs a PDF rendering engine — the one item here that requires bundling `pdf.js` locally in `lib/`. |
| 4 | **Image Converter** | Convert between JPG, PNG and WebP, with an optional resize. Batch in, ZIP out. | Same canvas pipeline as the compressor — could be one tool with tabs. |
| 5 | **PDF Merge & Split** | Combine several PDFs into one, pull specific pages out, delete pages, rotate, and reorder by dragging. | Rearranging PDF structure works without rendering it. |
| 6 | **Image Resizer & Cropper** | Resize to exact pixels, a percentage, or a preset (Instagram, YouTube thumbnail, A4). Crop with ratio locking. | Crop maths already written in Frame Grab. |
| 7 | **PDF Compressor** | Shrink PDF file size by re-encoding embedded images and stripping unused objects. | Needs the same engine as #3 — bundle `pdf.js` / `pdf-lib` in `lib/`. |
| 8 | **Word to PDF** | Convert a `.docx` into a PDF, keeping headings, lists and basic formatting. | `.docx` is a ZIP of XML. Needs a bundled converter — the heaviest item on this list. |
| 9 | **PPT to PDF** | Convert a `.pptx` deck into a PDF, one slide per page. | Same bundled-library approach as #8. |
| 10 | **QR Reader** | Scan a QR code from an uploaded image or the live camera and get the text or link back, with a copy button and history. | The Reed–Solomon maths in QR Forge is reusable. |
| 11 | **Video Compressor / Trimmer** | Trim a clip to a range and re-encode it smaller. Set target size or quality. | `MediaRecorder` on a canvas gives WebM cheaply; MP4 needs a bundled encoder. |
| 12 | **Video to GIF** | Turn a section of video into a GIF. Frame rate, size and loop controls, with a live preview. | Needs a hand-written GIF encoder, or ship WebM output first. |
| 13 | **Background Remover** | Cut the background out of a photo and export a transparent PNG. | Needs an ML model file (5–30 MB) in `lib/`. |
| 14 | **Audio Converter & Trimmer** | Trim audio to a range and export it. Fade in/out and volume normalise. | Web Audio decode + WAV export is straightforward; MP3 needs a bundled encoder. |
| 15 | **Favicon Generator** | One image in, every favicon size out — 16 to 512, plus `.ico` and the exact HTML snippet to paste into your `<head>`. | Pure canvas. `.ico` is a simple container format. |
| 16 | **Colour Picker & Palette** | Pull the dominant colours out of an image, or build a palette by hand. Copies as hex, RGB, HSL, Tailwind config, or CSS variables. | |
| 17 | **JSON Formatter** | Pretty-print, minify and validate JSON, with a collapsible tree view and error line numbers. | |
| 18 | **CSV to JSON** | Convert CSV or TSV to JSON and back, with a table preview and delimiter detection. | |
| 19 | **Base64 Studio** | Text to base64 and back, plus file to data URI — handy for embedding an image directly into a single-file tool. | |
| 20 | **Text Toolbox** | Case conversion, slug maker, line sorting and dedupe, find and replace, whitespace cleanup, word and character count. | One tool, several tabs. |
| 21 | **Password Generator** | Generate strong passwords or passphrases with length and character-set controls and a live strength meter. | `crypto.getRandomValues`. |
| 22 | **Markdown Editor** | Write markdown with live preview, then export as HTML or print to PDF. | |
| 23 | **Image to Text (OCR)** | Read text out of a screenshot or photo and copy it. | Needs a bundled OCR engine in `lib/`. |
| 24 | **Screen & Webcam Recorder** | Record your screen, a window, or your webcam and download the clip. | `MediaRecorder` + `getDisplayMedia`. Fewer lines than it sounds. |
| 25 | **EXIF Viewer & Stripper** | Show the hidden metadata in a photo — camera, date, and GPS location — then re-save it clean. | Fits the privacy angle of the site better than anything else here. |
| 26 | **Meta Tag Generator** | Build Open Graph and Twitter card tags with an accurate preview of how the link will look when shared. | |
| 27 | **CSS Playground** | Visual builders for gradients, box shadows, border radius and glassmorphism, with the CSS ready to copy. | |
| 28 | **Invoice Generator** | Fill in line items and client details, get a clean PDF invoice. Saves the layout, not the data. | Builds on #2 plus text drawing. |
| 29 | **Unit & Ratio Calculator** | px ↔ rem ↔ em, aspect ratio solving, and a breakpoint helper. | |
| 30 | **UUID & Hash Generator** | Generate UUIDs in bulk, and hash text with SHA-1/256/512. | `crypto.subtle`. |
| 31 | **Lorem Ipsum & Placeholder** | Generate filler text by words, sentences or paragraphs, and placeholder images at any size. | |

---

## 3. How this site is built

*This section exists so the design can be picked up again later without re-deciding
anything. If you are handing this repo to someone — or to an AI in a fresh conversation —
point them here.*

### Structure

```
Free-Toolkit/
├── index.html          the landing page; tool cards are generated from a TOOLS array
├── favicon.svg         yellow lightning bolt, transparent background
├── developer.png       photo used in the Developer panel
├── README.md
└── tools/
    ├── qr-forge.html
    └── frame-grab.html
```

Every tool is one self-contained HTML file — markup, CSS and JS inline, no build step, no
framework, no external requests. A tool must work when downloaded and opened from disk
with the internet off. If a tool ever needs a heavy library, bundle it locally in `lib/`
rather than loading it from a CDN — the "nothing leaves your device" promise is the point
of the project.

### Colour

Every page shares one dark base, and each tool owns one accent colour used for its card on
the index, its wordmark, its buttons and its scrollbar.

```css
--bg:          #0b0d12    /* page */
--surface:     #12151d    /* cards, panels */
--surface-2:   #181c26    /* inputs, secondary buttons */
--line:        rgba(255,255,255,0.08)
--line-bright: rgba(255,255,255,0.16)
--text:        #e8ecf3
--dim:         rgba(232,236,243,0.52)
--faint:       rgba(232,236,243,0.30)

--volt: #ffe94d   /* toolkit identity — bolt, index highlights, hover borders */
--live: #f87171   /* status LED, heart, destructive */
--good: #34d399   /* success states */
```

Tool accents, set per file as `--tint` / `--tint-deep`:

| Tool | Accent |
|---|---|
| QR Forge | `#38bdf8` → `#0284c7` (sky) |
| Frame Grab | `#a78bfa` → `#7c3aed` (violet) |

New tools pick an unused hue. Set `--tint` in the tool file and the matching `tint` /
`tintDeep` in the index `TOOLS` array so the card and the page agree.

### Type

No web fonts. Nothing is requested from anywhere, so system stacks only.

```css
--display: ui-sans-serif, system-ui, -apple-system, "Segoe UI Variable Display", …
--body:    ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, sans-serif
--mono:    ui-monospace, SFMono-Regular, "Cascadia Mono", Menlo, Consolas, monospace
```

- **Index wordmark** — heavy sans, uppercase, `FREE` outlined via `-webkit-text-stroke`
  cycling through the tool accents, `TOOLKIT` solid.
- **Tool wordmarks** — monospace, weight 800, uppercase, tracking `-0.05em`. First word in
  white, second in the tool's accent. (`QR`+`FORGE`, `FRAME`+`GRAB`.)
- **Labels, eyebrows, metadata, hints** — mono, ~0.63–0.7rem, uppercase, wide tracking
  (0.1–0.24em), colour `--faint`.
- **Body copy on tool pages** — mono, 0.78rem, line-height 1.75.
- **Body copy on the index** — sans, 1.02rem.

### Layout

- `--wrap: 1400px` on tool pages. Every region — hero, workspace, footer — uses
  `max-width: var(--wrap)` so all left and right edges line up. Do not hardcode a width.
- The index runs full width by design.
- Page padding: `clamp(18px, 3.5vw, 56px)`.
- Hero top padding: `clamp(76px, 12vh, 150px)`.
- Tool pages use a two-column hero: copy on the left, the primary action on the right
  (mode selector for QR Forge, drop zone for Frame Grab).
- Panels: `border-radius: 18px`, `1px solid var(--line)`, `background: var(--surface)`.
- Breakpoints: 1100px (side panels drop below), 900px (hero stacks), 720px / 640px
  (single column; feature cards hide on phones).

### Motion

- Ambient background on every page: three slow-floating blurred blobs in the tool's accent
  plus `--volt`, and ~12 drifting specks. No grid overlay — it lit up behind the headline.
- Page load: staggered `.reveal` with `.d1`–`.d5` delay classes.
- Cards: lift on hover, animated top rule, a light sweep across, icon tilt.
- Everything is wrapped in `@media (prefers-reduced-motion: reduce)`.

### Components

Consistent across all three files: pill eyebrow with a pulsing dot and fading rule,
segmented button groups (`.seg`, max 150px per button so they don't stretch), sliders with
a live value on the right of the label, `.btn primary` / `.btn ghost`, mono hint lines, a
themed scrollbar, and a footer with `← Free Toolkit` on the left and *Built with ♥ by
Subham* on the right.

### Writing style

Plain and specific. No marketing voice, no exclamation marks. Tell the user what the tool
does and what the trade-off is. When something might not work — a logo too large to scan,
a browser that can't encode WebP — say so in the interface, not in a disclaimer.

---

## Adding a tool

1. Build it as one HTML file in `tools/`.
2. Copy the shell from an existing tool — tokens, ambient layer, hero, footer, scrollbar —
   and give it a new `--tint`.
3. Add one object to the `TOOLS` array in `index.html`:
   ```js
   {
     name: "Tool Name",
     file: "tools/tool-name.html",
     size: "NN KB",              // check the real file size, this goes stale
     kind: "Converter",
     tint: "#hex", tintDeep: "#hex",
     desc: "Two or three lines on what it actually does.",
     icon: '<svg …>'
   }
   ```
4. Add a row to the table in section 1 and tick it off in section 2.
5. Test it offline: download it, turn off Wi-Fi, open it.
6. Test it on a phone.

---

Built with ♥ by [Subham](https://github.com/MSubham06)