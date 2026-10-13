# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Professional portfolio for Renato Deyvson as a software developer. Sister site of the music EPK `minirenatinho.github.io` (Mini Renatinho, on `minirenatinho.com.br`); each site links to the other only discreetly (footer / about text).

Deployed via GitHub Pages from `minirenatinho/renatodeyvson.github.io` — a regular project repo under the `minirenatinho` account (despite the `.github.io` name) — on the custom domain `renatodeyvson.com.br` (set by the `CNAME` file). Public URLs in metadata (`canonical`, `hreflang`, `og:url`, `sitemap.xml`) use the custom domain.

## Stack

Vanilla HTML and CSS — no JavaScript, no build system, no package manager. The site is served exactly as-is. Preview with any static server:

```
npx serve .
```

## Bilingual Pages

- `index.html` — Portuguese (pt-BR), the default and `x-default`
- `en/index.html` — English copy; uses `../` for every local asset

Both pages must stay in sync: any content change goes into both files. Each page carries `hreflang` alternates, and `sitemap.xml` lists both URLs with `xhtml:link` alternates.

## Résumé

- `pdf/curriculo-renato-deyvson.pdf` (pt-BR, linked from `index.html`) and `pdf/resume-renato-deyvson.pdf` (en, linked from `en/index.html`)
- Source: `_curriculo/curriculo.html` (pt-BR) and `_curriculo/resume.html` (en), sharing `_curriculo/style.css` (A4, Arial, navy `--heading`, blue `--link`). GitHub Pages' Jekyll skips `_`-prefixed folders, so the source is versioned but not published. Like the site pages, both files must stay in sync.
- Regenerate each PDF with headless Chrome. Both paths must be absolute, because a relative page path is read as a hostname. Each résumé should stay at two A4 pages.

  ```
  chrome --headless --no-pdf-header-footer --print-to-pdf="<repo>/pdf/curriculo-renato-deyvson.pdf" "file:///<repo>/_curriculo/curriculo.html"
  ```

- The public PDFs leave out the phone number. Renato also keeps Google Docs versions (with the phone) to send directly to recruiters; those are edited by hand and may lag behind `_curriculo/`.
- Keep the experience section of the site consistent with the résumé (titles, month/year periods, clients described by sector only — no client names).

## Architecture

Single page per language with a fixed nav linking to in-page sections: Experiência/Experience, Projetos/Projects, Stack, Sobre/About, Contato/Contact.

- **`main.css`** — all styling. Light and dark themes via `prefers-color-scheme` tokens on `:root`; navy accent (`--accent`) and a brighter blue for links (`--link`), matching the résumé; no green apart from the "available" status dot; Inter for text, JetBrains Mono for labels, tags and periods. Components: `.card`, `.tags`, `.timeline`/`.roles` (experience), `.projects` (featured cards with a 16:9 image), `.more` (compact list of other projects), `.stack`, `.facts`.
- **`404.html`** — bilingual not-found page; uses absolute paths (`/main.css`) because GitHub Pages serves it at any URL
- **`favicon.svg`**, **`images/favicon.png`**, **`images/apple-touch-icon.png`** — "RD" monogram icons (navy `#1e3a5f`)
- **`images/og-pt.jpg` / `images/og-en.jpg`** — 1200×630 social preview cards (photo + name + stack)
- **`images/renato.jpg`** — 480×480 avatar used in the hero
- **`pdf/`** — résumé PDFs; **`_curriculo/`** — their HTML/CSS source, not published (see Résumé above)
- **`metronomo/`**, **`bruxinha-nautica/`** — downloadable builds (APK / zip) linked from the projects section
- **`robots.txt` / `sitemap.xml`** — SEO; update `lastmod` on significant content changes

Mixer de Vibe is hosted by its own repo at `minirenatinho.com.br/mixer-de-vibe/`; this site only links to it.

## Adding Projects

Strong, recent projects go in `.projects` as a featured card (image in `images/`, 16:9, compressed for web). Older or smaller ones go in the `.more` list without an image. Downloadable builds get their own folder (like `metronomo/`).

## Planned Work

`BACKLOG.md` tracks planned improvements — check it before adding new features.
