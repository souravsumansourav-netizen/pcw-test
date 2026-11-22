# Signature Couture Edit — Tanishq × Rahul Mishra (Salesforce fragment, build 165d)

The page names every image, film, link and text; the script names none of them.

    index.html          the markup to paste where the page's content goes: one <link>, the root <div id="pcwv6-pcw">, one deferred <script>
    assets/css/pcw-v6-165d.css  all styles, one file; every url() absolute on the CDN
    assets/js/pcw-v6-165d.js    all script, one file (our code and three.js, minified); no file names inside
    assets/images/<section>/…   the images (opening, three-worlds, metamorphosis, trellis, bridge, moodboard, invitation, film, shared)
    assets/videos/              the master film and the four Moments films
    assets/fonts/               three woff2 files

The layout is the Adhyantara one: css, js, images, videos, fonts under `assets/`, to upload under `https://staticimg.tanishq.co.in/microsite/couture/assets/` with the same folder layout.

## Putting it on the page
1. Upload `assets/` so that each file sits at `https://staticimg.tanishq.co.in/microsite/couture/assets/<same path>`. If the folder differs, search/replace that prefix in `index.html` and the css; the script carries no paths.
2. Paste the three parts of `index.html` where the page's content goes (the `<link>` may go in the head, the `<script defer>` at the end of the body).
3. Images the 3D scene draws are listed in `<template id="pcwv6-pcw-assets">`, one `<img data-asset="…" src="…">` per texture; the master film and its poster are there too. To replace an image, change the URL there. Product names and links are the `<a data-link="product-…">` entries and the `data-piece` labels; all copy is in `<div id="pcwv6-pcw-copy">`.
4. The host's fixed header is measured by the script (any fixed or sticky bar across the top of the page, outside our root) and the stage sits under it (`--pcw-head`).

## Names
Every id, class, keyframe and CSS variable the page adds starts with `pcwv6-`; every CSS rule starts with `#pcwv6-pcw`; no `<main>`, `<header>`, `<footer>`, `<nav>` or `<dialog>` elements. Inside the root, bare elements (img, video, section, div, ul, figure, h1–h4, p, a, button, input) are reset first so the host's global rules do not reach them. The build tag is in the css/js file names: rename on every change, never overwrite a file on the CDN.

## Scroll, touch, state
Wheel, touch and keys are handled on our root only, and only while the journey owns the scroll; after the moodboard the page scrolls natively. The window carries a passive `scroll`, `resize`, `pageshow` and `visibilitychange` only. On touch screens the stage sets `touch-action: pinch-zoom`. No history writes, no hash, no storage, no cookies, no globals.

## CDN requirements
- `Access-Control-Allow-Origin: *` on every image and on the three `.woff2` files (textures are fetched with `crossOrigin="anonymous"`; fonts are always cross-origin).
- HTTP `Range` on `.mp4` (iOS Safari).
- gzip or brotli on `.js` and `.css` (the script is 525 KB raw, 143 KB gzipped).

## Films
`assets/master-film/master-film.mp4` (26.6 MB, 1280×666, 172 s) is loaded only when played; the four Moments films (about 1.1–1.8 MB each) load only when their card is near. No phone rendition exists yet.

## Appointment form
The form validates and thanks the visitor; it posts nowhere. Wire it to the lead endpoint before publishing, or remove it.

## Checked
Host replica (fixed 86 px / 130 px bar, `overflow:hidden` wrapper, global rules on img, button, a, h1–h3, p, ul, section), desktop 1440×900 and phone 375×812: opening, film, the three collections, moodboard, invitation, host footer; zero console errors, zero 404s. Not checked: real iPhone/Android, Windows wheel, the live Tanishq CSS, CDN headers.

## This repo (build 165d)
- Repo root is the deployable test site (Render: Docker via `Dockerfile`, or Static Site with publish dir `.`). Asset paths are local `/assets/...`.
- `salesforce/index.html` is the Salesforce/CDN version (assets on `staticimg.tanishq.co.in`); upload `assets/` to the CDN with the same layout.
