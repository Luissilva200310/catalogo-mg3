# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file HTML catalog viewer for a carpentry business (marcenaria). No build system, no dependencies, no package manager — just open `catalogo-marcenaria.html` in any browser.

## Running

Open `catalogo-marcenaria.html` directly in a browser. All assets (Google Fonts) are loaded from CDN; images must reside in the `imagens/` folder alongside the HTML file.

## Architecture

Everything lives in `catalogo-marcenaria.html` — styles, markup, and scripts are all inline.

**Configuration block** (top `<script>`, clearly marked "ÁREA DE CONFIGURAÇÃO"):

- `CATALOGO` — array of slide objects `{ title, category, desc, src }`. `src` is the image filename relative to the HTML file. Empty `src` renders a placeholder.
- `CONFIG` — `{ nomeMarcenaria, tagline }` sets the header brand name and subtitle.

**Runtime logic** (bottom `<script>`):

- `init()` — reads `CONFIG`, builds category filter buttons from unique `category` values in `CATALOGO`, then calls `setCategory("Todos")`.
- `setCategory(cat)` — filters `CATALOGO` into `filtered[]`, resets `current = 0`, calls `renderAll()`.
- `renderAll()` — destroys and rebuilds all `.slide` elements in `#imageStage` and `.thumb` elements in `#thumbStrip`.
- `goTo(index)` / `navigate(dir)` — update `current`, toggle `.active` classes on slides and thumbnails, scroll thumbnail into view.
- Keyboard: `←` / `→` navigate; `F` toggles fullscreen. Touch swipe (>50px delta) also navigates.

**CSS custom properties** (`:root`): `--wood-dark`, `--wood-mid`, `--wood-light`, `--cream`, `--cream-dark`, `--gold`, `--text`, `--muted`. All color changes should go through these variables.

## Adding Images

1. Copy the image file into the `imagens/` folder.
2. Add an entry to the `CATALOGO` array:
   ```js
   { title: "Nome", category: "Categoria", desc: "Descrição opcional", src: "imagens/nome-arquivo.jpg" }
   ```
3. Category filter buttons are auto-generated — no extra step needed.
