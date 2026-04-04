# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```sh
npm run dev       # Dev server at localhost:4321
npm run build     # Build to ./dist/
npm run preview   # Preview production build
```

## Architecture

Single-page landing site for **Krunchy Studio** (food photography agency, Santa Cruz, Bolivia).

**Component tree:**
```
Layout.astro        → HTML shell, global CSS vars, Google Fonts (Montserrat + Hind Madurai)
  Header.astro      → Fixed floating navbar, hamburger menu for mobile
  Inicio.astro      → Entire landing page content (hero → footer)
    PaqueteCard.astro → Reusable card for pricing packages (accepts video, title, description[], price, categoria)
```

**`Inicio.astro`** is the main file — it contains all landing page sections in order:
- Hero (banner with video background)
- Servicios (diagonal clip-path background)
- Portafolio (manual carousel, 7 images `/public/p1.jpg`–`/public/p7.jpg`, fade transition via `.fading` class)
- Marquesina (logo scroll, 9 logos × 2 duplicated for seamless loop, logos in `/public/logo1.png`–`logo9.png`)
- Razones para Elegirnos (two-column: portrait image left / numbered list right)
- Paquetes (PaqueteCard grid with category filter tabs)
- Objetivo (video section `/public/objetivo.mp4`)
- Contacto (violet card, social links, founder image `/public/diego.png`)
- Footer (dark navy `#16172a`, 3-col grid)

## CSS Design System

All CSS custom properties are defined in `Layout.astro` as `:root` globals:

| Var | Value | Usage |
|-----|-------|-------|
| `--primary` | `#8198ca` | Brand blue, nav CTA bg |
| `--violet` | `#5b68c9` | Accent on cards, buttons |
| `--dark-violet` | `#2a2682` | Dark headings |
| `--accent` | `#85b4db` | Light blue accent |
| `--font-montserrat` | Montserrat | Primary font (all UI) |
| `--font-hind` | Hind Madurai | Body text alternative |

Responsive breakpoints used throughout `Inicio.astro`: `480px`, `576px`, `768px`, `900px`, `1024px`, `1200px`.

## Key Patterns

- **Scoped styles**: Each `.astro` file uses `<style>` (scoped) — styles don't leak between components.
- **Diagonal backgrounds**: `clip-path: polygon(...)` on section pseudo-elements (Servicios, Razones).
- **Carousel JS**: Inline `<script>` at bottom of `Inicio.astro`, IIFE pattern, touch swipe support (dx > 40px threshold).
- **WhatsApp links**: Format `https://wa.me/59162161541` — used in PaqueteCard and Contacto.
- **No framework JS**: All interactivity is vanilla JS in `<script>` tags inside `.astro` files.
