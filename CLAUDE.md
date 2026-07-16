# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static landing page for **Forêt Club** — guided group forest walks in Strasbourg. The entire site is a single self-contained file: `index.html`. All content is in French (`lang="fr"`).

There is no build system, package manager, linter, or test suite. To preview locally:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Architecture of index.html

- **Single-file design**: one inline `<style>` block, **no JavaScript at all**. Interactivity (smooth scroll, hover states) is pure CSS. Keep it that way unless explicitly asked to add scripts.
- **Images are embedded as base64 data URIs** (10 JPEG + 1 PNG), which makes the file ~1.8 MB despite being only ~460 lines. **Never read the whole file** — target sections with Grep or offset/limit reads to avoid pulling megabytes of base64 into context. Editing text/CSS is safe with exact-string edits.
- **Design tokens** live in `:root` CSS variables at the top of the `<style>` block: `--fuchsia` (#FF0099, accent/CTA), `--mint`, `--neon` (badge), `--jungle` (dark text), `--ivory` (background), `--vert-pale`.
- **Typography**: Playfair Display (headings, italic accents) + Inter (body), loaded from Google Fonts — the only external stylesheet.
- **Signup funnel**: CTA buttons link to an external Tally form (`https://tally.so/r/J9YoJJ`). There is no form handling in the page itself.
- **Page structure** (in order): fixed nav → hero with logo → full-width photo breaks alternating with `.section` blocks: concept ("C'est quoi, le Forêt Club ?"), benefits, "pour qui", group formation, presenter bio (Oriane), pricing (`.tarif-bloc`), CTA, FAQ (7 CSS-only `.faq-item`s) → footer.
