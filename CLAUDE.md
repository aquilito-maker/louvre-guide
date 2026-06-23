# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is a single-file static HTML app: `louvre_full_guide_v2.html`. No build step, no dependencies, no server required — open directly in a browser.

The `louvre-guide/` directory is currently empty and appears to be a planned future location for project files.

## Architecture

All code lives in one file with three sections:

1. **`<style>`** — Inline CSS using CSS custom properties (`--color-*`, `--border-radius-*`, `--font-sans`) that must be provided by a host environment (e.g., a Claude artifact viewer). The component does not define fallback values, so it only renders correctly inside that host.

2. **`PIECES` array** — The data layer. Each entry has: `id`, `num`, `title`, `bonus`, `loc`, `img` (Wikipedia URL), `lookFor`, `history`, `lenses` (array of `{type, lbl, txt}`), `controversy`, and `tags` (subset of `["eng","anth","arch","pol"]`).

3. **Rendering logic** — Three functions (`buildNav`, `buildFilters`, `buildCards`) regenerate the DOM on each interaction. State is two variables: `activeNav` (artifact id or `"all"`) and `activeFilter` (tag key or `null`). `refresh()` calls all three builders and is the only update path.

## Adding content

To add a new artifact, append an object to `PIECES` following the existing schema. The `lenses` array should have 2–3 entries; `tags` must be a subset of `["eng","anth","arch","pol"]`. The nav and filter UI rebuild automatically from the data.

## Viewing

Open the file in a browser or paste into a Claude artifact window. The CSS variables are only defined in the Claude artifact environment — raw browser rendering will show unstyled layout.
