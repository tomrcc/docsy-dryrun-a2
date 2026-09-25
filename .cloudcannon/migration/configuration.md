# Configuration — Docsy starter

Validated with `npx @cloudcannon/cli validate` (all files valid). Schemas downloaded to `.cloudcannon/migration/*.schema.json` (gitignored).

## Collections

| Collection | Path / glob | URL | Schemas | Notes |
| --- | --- | --- | --- | --- |
| `pages` | `content`, `**/*.md` minus `docs/**`, `blog/**`, `search.md` | `/[full_slug]/` | `default` = Landing page (`content_blocks`), `page` = Text page | Home (`_index.md`), `about/index.md` (leaf bundle, kept), `community/_index.md`, `privacy.md` |
| `docs` | `content/docs` (incl. every `_index.md`) | `/docs/[full_slug]/` | `default` = Docs page, `section` = Docs section (creates `<slug>/_index.md`) | Sorted by weight. `_index.md` kept in — every docs section index has body content. |
| `blog` | `content/blog` (incl. `_index.md`) | `/blog/[full_slug]/` | `default` = Blog post (creates `<slug>/index.md` bundle), `section` = Blog section (not in `add_options`) | Posts are all leaf bundles. Upload path via `_editables.content.paths` → post folder, relative. |
| `data` | `data/*.yaml` | none | — | `links.yaml`, `footer.yaml`, `tags.yaml`, `categories.yaml`; `data_config` entries for all four, `file_config` for inputs. |

`search.md` (Docsy search results page, `layout: search`) is excluded — nothing to edit.

## Decisions

- **Blog permalinks dropped.** docsy-example used `blog: /:section/:year/:month/:day/:slugorcontentbasename`. That applies to posts but not to `blog/news/_index.md`-style section pages, so no single collection `url` fits both, and CloudCannon has no per-schema `url`. For a starter, the default `/blog/<subsection>/<post>/` is simpler and fits `/blog/[full_slug]/`.
- **Shared UI → data files.** Docsy reads footer links, copyright and privacy URL from `site.Params`. Moved to `data/links.yaml` + `data/footer.yaml`; overrode `footer/left.html`, `footer/right.html`, `footer/center.html` to read `hugo.Data`. The Community page's `community_links.html` equivalent is now the `blocks/community-links` block reading `hugo.Data.links`.
- **Taxonomies → data files.** `tags` and `categories` are top-level `multiselect` inputs with `values: data.tags` / `data.categories`, from `data/tags.yaml` and `data/categories.yaml` (top-level string arrays, editable under Site data). No `allow_create`: editors add a term to the data file, so every page picks from one list. No template reads these files; Hugo still builds term pages from front matter.
- **Navigation** stays Hugo-native: `menu.main.weight` in each page's front matter, exposed as a `menu` object input with a structure.
- **Site title, logo, colours, search** stay developer-owned in `hugo.yaml`/`assets/` — documented in `.cloudcannon/README.md`.
- **Images** in `static/images/`, with a `static → assets` mount so the cover block can `resources.Get` + `.Fill` at build time and use the plain path in the editor. Blog post images stay in their bundles.
- **timezone** `Etc/UTC` (starter; no owner timezone). CLI had written the machine's `Pacific/Auckland`.
- **Snippets**: `alert`, `pageinfo` (paired markdown, named args), `imgproc` (paired, positional), `tabpane` + `tab` (raw, `repeating`). No `_snippets_imports` — content uses no Hugo built-in shortcodes.
- **Markdown** options match Goldmark: `html: true` (unsafe), `table`, `strikethrough`, `linkify` true, `typographer` false, `attributes: true` (Goldmark `parser.attribute.block`).
- **Build**: `npm ci` + `npm run build` (`hugo --cleanDestinationDir --minify`), `hugo_version` 0.166.0, `node_version: file` (`.nvmrc` = 24). Removed the npm `hugo-extended` pin so CloudCannon's Hugo is the one that runs.

## Unverified — needs CloudCannon

- `_index.md` with `[full_slug]`: home (`content/_index.md` → `/`), `community/_index.md` → `/community/`, docs/blog section indexes. The Hugo skill flags this as unknown.
- `about/index.md` with `/[full_slug]/` → expect `/about/`.
- `_editables.content.paths.uploads: content/blog/[relative_base_path]` with `uploads_use_relative_path` — does `[relative_base_path]` resolve to the post's folder inside a collection-level `_editables`?
- Schema `create.path` for Docs section/Blog post (`[relative_base_path]/{title|slugify}/_index.[ext]`).
- Snippet round-trips, especially `tabpane` (`text=true` unquoted boolean) and `imgproc` positional args.
- `instance_value: NOW` on the global `date` input.
