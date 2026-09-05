# QR Forge

A single-file, offline-first QR code generator that runs entirely in the
browser — no build step, no server, no dependencies. Open the HTML file and
it works.

It supports styled QR codes (custom pixel/eye/frame shapes, gradients, logo
overlays) similar to the QR tool in [ImageToolbox](https://github.com/T8RIN/ImageToolbox),
an open-source Android image editor. The QR-code encoding engine (Reed–Solomon
error correction, mask-pattern selection, module placement) was ported to
JavaScript from the algorithm used by ImageToolbox's `qrose` Kotlin library —
see [Credits & attribution](#credits--attribution) below.

## Features

- **Content types**: plain text, URL, Wi-Fi, email, phone, SMS, contact
  (vCard), and geolocation (`geo:` URI)
- **Error correction levels**: L / M / Q / H, selectable per code
- **Styling**: pixel shape (square, circle, rounded, diamond, dot), finder
  "eye" shape, finder frame shape, solid or gradient coloring, adjustable
  corner rounding
- **Logo overlay**: upload an image to embed in the center; error correction
  automatically switches to H to keep the code scannable
- **Export**: download as PNG or SVG
- **Fully client-side**: nothing you type is sent anywhere — there is no
  backend, no analytics, no network calls at all

## Requirements

None, beyond a modern web browser (Chrome, Firefox, Safari, Edge — anything
with reasonably current Canvas/ES6 support). There is nothing to install,
no `npm install`, and no build/bundle step.

## Usage

### Locally
Download `qr-forge.html` and open it directly in a browser (double-click
it, or `open qr-forge.html` / drag it into a browser window).

### Via GitHub Pages
1. Push this repo to GitHub.
2. In **Settings → Pages**, set the source to the branch/folder containing
   `qr-forge.html` (root of `main`, for example).
3. Rename the file to `index.html` if you want it served at the root of your
   Pages URL, or link to `qr-forge.html` directly.

## Project structure

```
.
├── qr-forge.html   # the entire app: markup, styles, QR engine, and UI logic
├── README.md           # this file
├── LICENSE             # MIT license for this project's original code
└── NOTICE              # required attribution for ported Apache-2.0 code
```

## How it works

- The `<script>` block in `qr-forge.html` is split into two parts:
  1. **QR engine** — a from-scratch JS re-implementation of standard QR
     encoding (byte-mode encoding, Reed–Solomon error-correction codewords,
     all 8 mask patterns scored and the best one selected, finder/timing/
     alignment pattern placement). This follows the same algorithm as the
     `qrose` library used by ImageToolbox.
  2. **UI/app logic** — content-type forms, style pickers, canvas rendering
     of the matrix with the chosen shapes/colors/logo, and PNG/SVG export.
- Output has been checked against OpenCV's QR decoders across multiple
  content types, lengths, and error-correction levels to confirm generated
  codes actually scan correctly.

## Credits & attribution

- QR-encoding algorithm ported from **[ImageToolbox](https://github.com/T8RIN/ImageToolbox)**'s
  `qrose` library (Copyright © 2026 T8RIN / Malik Mukhametzyanov; original
  `qrose` package by alexzhirkevich), licensed under the
  **Apache License, Version 2.0**. See [`NOTICE`](./NOTICE) for the full
  attribution notice and license text, as required by that license.
- Styling concepts (pixel/eye/frame shape options, gradients, logo overlay)
  are inspired by the same library's QR customization options.
- No original ImageToolbox/qrose source files are redistributed here — the
  encoding logic was independently re-implemented in JavaScript and verified
  for correctness, then relicensed for this repo's original code under MIT,
  with the Apache-2.0 attribution preserved in `NOTICE` as required.

## License

This project's original code (UI, app logic, payload builders, styling) is
licensed under the **MIT License** — see [`LICENSE`](./LICENSE).

The ported QR-encoding engine remains subject to the attribution
requirements of the **Apache License, Version 2.0** — see [`NOTICE`](./NOTICE).

This isn't legal advice — if you plan to redistribute or relicense this
further, it's worth having your own read of the Apache-2.0 terms (or a
lawyer's) to confirm your use case is covered.
