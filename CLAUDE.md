# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Reality

Static React prototype — no `package.json`, bundler, CI, or test/lint config. All React and Babel run in-browser via CDN.

- Primary app: `Les Coiffeurs v2.html` (single-page, ~1500 lines, inline JSX via Babel)
- Shared helper: `tweaks-panel.jsx` (edit-mode UI kit loaded directly from HTML)

## Running Locally

```bash
python3 -m http.server 8000
# Open: http://localhost:8000/Les%20Coiffeurs%20v2.html
```

Do not introduce bundler or build-tool assumptions unless explicitly asked.

## Architecture

### Single HTML entry point

All CSS, components, and content live inline in `Les Coiffeurs v2.html`. Follow that pattern unless asked to restructure.

**Script load order is locked — do not reorder:**
```
React → ReactDOM → Babel → tweaks-panel.jsx → <script type="text/babel"> (inline app)
```

### tweaks-panel.jsx

Exposes globals on `window`: `useTweaks`, `TweaksPanel`, `TweakSlider`, `TweakRadio`, `TweakColor`, `TweakToggle`, `TweakSection`. The HTML app consumes these directly.

Edit-mode protocol: listens for `__activate_edit_mode` / `__deactivate_edit_mode` window messages, posts status events back.

### EDITMODE block

Inside `Les Coiffeurs v2.html`, a `/*EDITMODE-BEGIN*/ ... /*EDITMODE-END*/` JSON block configures live-edit tweaks (`TWEAK_DEFAULTS`). Keep it valid JSON and leave the markers unchanged — they are host-managed.

### Bilingual content

Content strings live in a `T` object with `T.fr` and `T.en` keys. When changing copy or data, keep both locales in sync unless the task explicitly says otherwise.

### Images

`IMGS` object maps logical names to file paths under `uploads/`.
