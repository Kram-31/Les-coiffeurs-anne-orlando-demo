# AGENTS.md

## Repo Reality
- This is a static prototype, not a Node/monorepo project: no `package.json`, lockfile, CI workflow, or test/lint config exists.
- Primary app file is `Les Coiffeurs v2.html` (single-page React app via in-browser Babel).
- Shared edit-mode helper is `tweaks-panel.jsx` and is loaded directly from the HTML.

## Run / Preview
- Serve the repo root with `python3 -m http.server 8000` and open `http://localhost:8000/Les%20Coiffeurs%20v2.html`.
- Do not introduce bundler/build-tool assumptions unless explicitly requested.

## Non-Obvious Wiring
- Keep script order in `Les Coiffeurs v2.html`: React -> ReactDOM -> Babel -> `tweaks-panel.jsx` -> inline `text/babel` app script.
- `tweaks-panel.jsx` exposes globals on `window` (`useTweaks`, `TweaksPanel`, `Tweak*` controls); the HTML app consumes those directly.
- The `/*EDITMODE-BEGIN*/ ... /*EDITMODE-END*/` block in `Les Coiffeurs v2.html` is host-managed; keep it valid JSON and keep the markers unchanged.

## Editing Conventions In This Repo
- This prototype keeps CSS + React components inline in `Les Coiffeurs v2.html`; follow that pattern unless asked to restructure.
- Content is bilingual via `T.fr` and `T.en`; when changing copy or data, keep both locales in sync unless the task says otherwise.
