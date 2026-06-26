# The Composable Codex — archival recreation

A self-contained, offline-viewable recreation of **The Composable Codex** by
[Voltron Data](https://voltrondata.com), which went offline in 2025. This copy
was reconstructed from the Internet Archive's Wayback Machine snapshot taken on
**2024-09-26** (`https://web.archive.org/web/20240926150551/https://voltrondata.com/codex/`).

This is an unofficial preservation copy. All content, text, and imagery are the
work and property of Voltron Data; this repository only re-hosts the publicly
archived material so it can be read again.

## Viewing it

It's a static site — open it in any browser. Because pages reference assets with
relative paths, serve the folder rather than opening the files directly:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/
```

Opening `index.html` straight off disk (`file://`) mostly works too, but a local
server is more reliable for the CSS/JS.

## Contents

| File | Chapter |
|------|---------|
| `index.html` | Landing page / table of contents |
| `a-new-frontier.html` | Chapter 00 — A new frontier |
| `open-standards.html` | Chapter 01 — Open standards over silos |
| `language-interoperability.html` | Chapter 02 — Bridging divides: Language interoperability |
| `data-connectivity.html` | Chapter 03 — From data sprawl to data connectivity |
| `accelerated-hardware.html` | Chapter 04 — The Wall & The Machine: Accelerated hardware |

- `assets/` — CSS, JS, fonts, and images (logos, diagrams, comics).
- `output.css`, `favicon.ico` — site stylesheet (Tailwind build) and icon.
- `_raw_original/` — the unmodified HTML exactly as pulled from the Wayback
  Machine, kept for provenance before any link rewriting.

All prose is captured in full. Every chapter, section, and heading anchor is
present and cross-links between chapters work locally.

## How it was rebuilt

1. Pulled the six raw HTML pages from the Wayback Machine using the `id_` raw
   modifier (strips the Wayback toolbar/wrapper).
2. Downloaded every local asset referenced by the pages.
3. Rewrote absolute paths to relative ones: `/codex/<chapter>` → `<chapter>.html`,
   `/assets/...` → `assets/...`, protocol-relative CDN URLs → `https://`.
   Non-Codex site links (e.g. `/about`, `/blog`) point back at the Wayback Machine.
4. External CDN libraries (jQuery, Flowbite, highlight.js, Lottie, fonts) are
   left as live `https://` references and load when you're online.

## Recovered vs. missing diagrams

Many diagrams (~37) were **not** captured in the Wayback snapshot, but Voltron
Data's Cloudinary CDN (`res.cloudinary.com/dm6arzeue`) is still live and served
the same images. Those were downloaded as PNGs and the pages rewritten to use
them, so the book renders with its diagrams intact.

The xkcd comic in Chapter 03 (#2054, "Data Pipeline") was re-fetched from
`xkcd.com`.

The following **11 assets could not be recovered** — they were never archived by
the Wayback Machine and have no Cloudinary equivalent. In their place the pages
show a styled placeholder containing the original `alt` description:

- The animated **MICE** badges (Modular / Interoperable / Customizable /
  Extensible) — Lottie `.json` animations reused across Chapters 01–04.
- Chapter 01's two "interoperable implementation" key/stack Lottie diagrams.
- Chapter 03's "it-depends" O'Reilly-parody cover image.

The placeholder styling lives in `assets/css/archive-fallback.css` and is the
only addition not present in the original site.
