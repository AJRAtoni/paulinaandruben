# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A static HTML/CSS/JavaScript destination wedding website for Paulina & Ruben's wedding in Tangier, Morocco (June 6, 2026). No build system, no npm, no framework — pure vanilla web.

**Live site:** https://paulinaandruben.com (deployed via GitHub Pages from `main` branch — every push to `main` auto-deploys)

## Development

No build or install steps. Open `index.html` directly in a browser, or use any static file server:

```bash
python3 -m http.server 8080
```

## Architecture

Two pages share one stylesheet:

- **`index.html`** — Full single-page site with all sections (Home/hero, Itinerary, Accommodations, FAQs, Footer). Contains embedded `<style>` in `<head>` in addition to the external `styles.css` link.
- **`rsvp.html`** — Standalone RSVP form; submits via `fetch` (no-cors) to a Google Apps Script endpoint that writes to Google Sheets.
- **`styles.css`** — Shared stylesheet used by both pages.

### JavaScript (inline in HTML files)

`index.html` contains:
- `updateCountdown()` — live countdown timer to wedding date
- `downloadICS()` — generates and downloads `.ics` calendar files for each event
- `toggleFaq()` — accordion open/close for the FAQ section
- Scroll listener for sticky header shadow and active nav link tracking
- Mobile hamburger menu toggle

`rsvp.html` contains only the mobile menu toggle and form submission logic.

### Styling Notes

- Color scheme: background `rgb(245, 239, 232)` (warm cream), primary `rgb(92, 23, 69)` (deep burgundy)
- Fonts: "Lovers in New York" (custom TTF in repo root) for display headings; "Cormorant Garamond" (Google Fonts) for body
- Responsive breakpoints handle mobile nav and layout adjustments
- Safari-specific fixes applied: `-webkit-font-smoothing`, `translateZ(0)` on key elements

### External Integrations

- **Google Sheets (RSVP):** Form posts to a Google Apps Script URL via `fetch` with `mode: 'no-cors'`
- **Calendar export:** `.ics` files generated client-side via `downloadICS()`
- **Google Fonts:** Loaded via `<link>` in `<head>`
- **Open Graph / Twitter Card:** Meta tags set for social sharing using `socialsharing.png`
