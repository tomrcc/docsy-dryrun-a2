# Build and test — Docsy starter

## Checks run locally (agent)

| Check | Result |
| --- | --- |
| Clean install + build: `rm -rf node_modules public resources && npm ci && npm run build` (Hugo 0.166.0 extended) | 57 pages, no errors; only warning is the no-commits `enableGitInfo` notice |
| Config | `npx @cloudcannon/cli validate` — 7 files valid |
| Renderer | `public/_cloudcannon/` has `hugo_renderer.wasm.*.gz`, `hugo-worker.*.js`, `live-editing.*.js` |
| Editor bundle | `hugo.yaml`, `i18n/en.yaml` and all 12 project partials are bundled keys |
| Editor renderer | The editor's Hugo 0.164 WASM (`public/_cloudcannon/hugo_renderer.wasm.*.gz`), run in Node on the bundle: config loads, and every block on home, About and Community renders with the same text and links as the built page |
| Regions in output | `array` 91, `array-item` 263, `text` 147 (includes `_print` pages); `data-component` on every block |
| Editor-mode build (`ENV_CLIENT: true`) | Builds; cover images fall back to plain `/images/…` paths; `<img>` counts equal on home, About, a post and a docs page. The 1 processed image left is the `imgproc` shortcode in a post body (content — not rendered in the editor) |
| editable-regions-check (`--source`) | 40 pages, 0 errors, 0 warnings; every content page maps to its source file. It checks region markup only, not the editor bundle: the bundle checks are the Editor bundle and Editor renderer rows |
| Visual parity (headless Chrome vs baseline) | Home cover, About blocks, Community, docs page layout match Docsy. Docs body wrapper keeps Docsy's `.td-content >` styles |

Page parity with the docsy-example baseline is structural, not page-for-page: content was rewritten as starter copy (see `content.md`).

## Build settings

`npm ci` → `npm run build` (`hugo --cleanDestinationDir --minify`), output `public`, `hugo_version` 0.166.0, `node_version: file` (`.nvmrc` 24), `HUGO_CACHEDIR` and `node_modules/,resources/,.hugo_cache/` preserved. The build needs network access to GitHub (Hugo modules and the renderer WASM).

## Needs checking in CloudCannon (human)

1. **Site builds** on CloudCannon with `hugo_version` 0.166.0 (lower it to 0.164.0 if that version isn't offered — Docsy needs ≥ 0.160.1).
2. **Home page and section pages open in the Visual Editor**: `/`, `/community/`, `/docs/`, `/blog/news/` (`_index.md` with `[full_slug]`), and `/about/` (`about/index.md`).
3. **Landing page blocks**: edit a cover title and a feature title inline; add, reorder and remove blocks; add a button to a cover (empty `buttons` array on About).
4. **Cover image**: change the background image in the sidebar; the block re-renders with the new image.
5. **Navbar**: new landing page with a cover first → translucent navbar after save/build.
6. **Docs page**: edit title, description and body inline on `/docs/overview/`; open the Content Editor and edit each snippet on `/docs/getting-started/writing-docs/` (alert, page info, tabs); save and check the diff touches only the edited value.
7. **Blog**: Add → Blog post creates `content/blog/<folder>/<slug>/index.md`; upload an image in the body and confirm it lands in that folder with a relative path; `imgproc` snippet on the Welcome post round-trips.
8. **Docs section**: Add → Docs section creates `<slug>/_index.md`.
9. **Site data**: edit Footer copyright inline (footer text) and in the Data Editor; add/reorder Links — footer icons and Community lists update.
10. **Menu**: set Navigation menu → Main menu → Weight on a new page; it appears in the top nav after a build.
11. **Front matter preserved**: save the home page and the Welcome post; `params.body_class` and `resources` are still in the files.

Send back: the page URL + what you clicked for anything that misbehaves, and CloudCannon build log lines if a build fails.
