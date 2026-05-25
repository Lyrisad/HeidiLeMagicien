# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static marketing website for "Heidi Le Magicien" — a professional magician based in Île-de-France. The site is hosted at `heidilemagicien.fr`. All content is in French.

## Tech Stack

- **Pure HTML/CSS/JS** — no build tools, no bundler, no framework, no package manager.
- Single shared stylesheet: `styles.css`
- Fonts: Cinzel (titles) and Inter (body) via Google Fonts
- Contact form: EmailJS (loaded from CDN, configured via `data-emailjs-*` attributes on the form element)
- PWA manifest: `manifest.json`

## Development

Open any `.html` file directly in a browser, or serve with any static file server:
```
python -m http.server 8000
```
There are no build, lint, or test commands.

## Architecture

### Pages

- `index.html` — Landing page (hero, showreel video, prestations cards, social media, Google reviews, contact form)
- `presentation.html` — Biography / about page
- `anniversaire.html` — Birthday party service (with image carousel)
- `closeup.html` — Close-up magic service (with image carousel)
- `mariage.html` — Wedding magic service (with image carousel)
- `entreprise.html` — Corporate events service (with image carousel)
- `formations.html` — Online card magic course page (links to external platform)
- `faq.html` — FAQ with `<details>` accordion

### Styling

All pages share `styles.css`. The design uses a dark theme with gold (`--gold: #c6a15b`) and bordeaux (`--bordeaux: #7a1e2b`) accent colors. CSS custom properties are defined in `:root`. Responsive breakpoints are at 1024px and 760px. Playing-card suit symbols (spades, hearts, diamonds, clubs) are used throughout as decorative motifs.

### JavaScript

All JS is inline in `<script>` tags at the bottom of each HTML file (no external JS files). Key interactive features:
- **Hero particle canvas** — animated gold sparkles behind the hero title (`index.html`)
- **Phone particle canvas** — similar effect in the social media section (`index.html`)
- **Cursor trail canvas** — gold particles following the mouse (`index.html`)
- **Playing card flip** — 3D CSS flip on the prestations cards, toggled via `aria-pressed`
- **Image carousel** — with autoplay, progress bar, touch swipe, and lightbox zoom (prestation pages)
- **Review clamp** — "Lire plus / Lire moins" toggle for long review texts
- **Contact form** — progressive enhancement: tries EmailJS first, then fetch to `data-endpoint`, then falls back to default form submission
- **Mobile nav** — hamburger toggle at 760px breakpoint

### SEO

Each page has its own structured data (`<script type="application/ld+json">`), Open Graph / Twitter Card meta tags, and canonical URL. The site targets local SEO for Val d'Oise (95), Paris (75), Yvelines (78), Hauts-de-Seine (92), and Île-de-France.

### Images

All images are in `img/`. Prestation carousel images are in `img/prestations/Carroussel/{anniversaire,closeUp,mariage,entreprise}/`.

## Conventions

- Navigation and footer markup are duplicated across all pages (no shared template system). When modifying the nav or footer, update every HTML file.
- Prestation pages (`anniversaire`, `closeup`, `mariage`, `entreprise`) follow an identical structure: shared header, `.prestation-media` layout with text + carousel, shared footer, and identical carousel JS at the bottom.
- The `data-suit` attribute on `.section-title` elements controls the decorative card suit icon shown via CSS `::before`.
- Accessibility: `aria-*` attributes are used on interactive elements (card flips, nav toggle, carousels). `prefers-reduced-motion` is respected for animations.
