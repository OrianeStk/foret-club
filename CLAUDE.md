# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static landing page for **Forêt Club** — collective forest walks for dogs in Strasbourg ("votre chien retrouve ses copains en forêt"). The site is a single `index.html` plus an `images/` folder. All content is in French (`lang="fr"`).

There is no build system, package manager, linter, or test suite. To preview locally:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Architecture of index.html

- **Single-file design**: one inline `<style>` block, **no JavaScript at all**. Interactivity (smooth scroll, hover states) is pure CSS. Keep it that way unless explicitly asked to add scripts.
- **Images policy**: all images live in `images/` at the repo root and are referenced with relative paths (`<img src="images/foo.jpg">`). **Never embed images as base64 data URIs.** Name files descriptively in French, matching the existing convention (e.g. `groupe-chiens-foret.jpg`, `oriane-plage-chien.png`), and give every content image French alt text.
- The full-width `.photo-break` images use `loading="lazy"`, so they don't appear in naive full-page screenshots — scroll through the page first if capturing renders for visual comparison.
- **Design tokens** live in `:root` CSS variables at the top of the `<style>` block: `--fuchsia` (#FF0099, accent/CTA), `--mint`, `--neon` (badge), `--jungle` (dark text), `--ivory` (background), `--vert-pale`.
- **Typography**: Playfair Display (headings, italic accents) + Inter (body), loaded from Google Fonts — the only external stylesheet.
- **Signup funnel**: CTA buttons link to an external Tally form (`https://tally.so/r/J9YoJJ`). There is no form handling in the page itself.
- **Page structure** (in order): full-screen hero with background photo (no nav bar, no logo) → full-width photo breaks alternating with `.section` blocks: concept ("C'est quoi, le Forêt Club ?"), benefits, "pour qui", group formation, founder bio (Oriane, with a photo grid), pricing (`.tarif-bloc`), CTA, FAQ (7 CSS-only `.faq-item`s).
