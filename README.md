# Docsy Starter for CloudCannon

A documentation site built with [Hugo](https://gohugo.io/) and the
[Docsy](https://www.docsy.dev/) theme, set up for editing in
[CloudCannon](https://cloudcannon.com/): docs and blog in markdown with Docsy's
components as snippets, page-builder landing pages, and inline editing in the
Visual Editor.

Editors: see [.cloudcannon/README.md](.cloudcannon/README.md), which CloudCannon
shows on the site dashboard.

## Requirements

- Hugo **extended** 0.160.1 or later (built and tested with 0.166.0)
- Go (Hugo modules) and Git
- Node.js 20+ and npm (Bootstrap, Font Awesome and Dart Sass come from npm)

## Run it locally

```sh
npm ci
npm run serve
```

`npm run build` makes the production build in `public/`. Run Hugo through
`npm run` (or put `node_modules/.bin` on your `PATH`) so it finds Dart Sass.

## How it's put together

| Path | What it is |
| --- | --- |
| `hugo.yaml` | Site config: imports Docsy (`github.com/google/docsy/theme`) and CloudCannon's editable regions (`github.com/CloudCannon/editable-regions`) as Hugo modules |
| `content/` | Home, About, Community (page-builder pages), `docs/`, `blog/` (posts are page bundles), `privacy.md` |
| `data/` | Text shared by every page: `footer.yaml`, `links.yaml` |
| `layouts/landing.html` | The page-builder layout: renders `content_blocks` |
| `layouts/partials/blocks/` | One partial per block type; `_name` in content is the partial path |
| `layouts/partials/footer/`, `navbar.html`, `hooks/head-end.html` | Overrides of Docsy partials: footer reads `data/`, navbar goes translucent over a cover block, head loads editable regions |
| `layouts/_td-content.html`, `docs/list.html`, `blog/_td-content.html` | Overrides of Docsy templates adding editable regions to the title, description and body |
| `static/images/` | Uploaded images (mounted into `assets/` too, so the cover block can resize them) |
| `cloudcannon.config.yml`, `.cloudcannon/` | CloudCannon collections, schemas, block structures and snippets |
| `content_fr/`, `content_de/` | French and German content, one file per English file at the same path (Hugo `contentDir` per language in `hugo.yaml`) |
| `i18n/` | Interface strings per language; these override Docsy's keys one by one |
| `layouts/partials/lang-data.html`, `localized-url.html` | Read a `data/` file keyed by language; resolve a link field to the current language's page |
| `layouts/partials/search-input.html`, `assets/json/offline-search-index.json` | Overrides of Docsy's offline search: one index per language |

Partials live in `layouts/partials/` (not Hugo's newer `layouts/_partials/`):
CloudCannon's editable-regions module bundles that directory for the Visual
Editor's in-browser Hugo.

## Updating Docsy

```sh
npm run update:docsy
```

After an update, compare the overridden Docsy files listed above with their new
versions in the theme. The search override was copied from Docsy
v0.17.1-0.20260831231032-2c44726e7773; find the theme's copy with
`hugo config mounts` and diff, for example:

```sh
diff <docsy-dir>/layouts/_partials/search-input.html layouts/partials/search-input.html
diff <docsy-dir>/assets/json/offline-search-index.json assets/json/offline-search-index.json
```

## License

Apache 2.0, like Docsy and docsy-example. See [LICENSE](LICENSE).
