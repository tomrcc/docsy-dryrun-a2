# Visual editing — Docsy starter

Module `github.com/CloudCannon/editable-regions` v0.0.21, Hugo 0.166.0 (editor renderer 0.164.0). Included via Docsy's `hooks/head-end.html` partial hook, which every Docsy base layout (`baseof.html`, `docs/baseof.html`, `blog/baseof.html`, `swagger/baseof.html`) calls from `head.html`.

## Where the templates live

| Templates | Location | Bundled for the editor? |
| --- | --- | --- |
| Page-builder blocks, footer, navbar, community list overrides | project `layouts/partials/` | Yes |
| Page templates (`landing.html`, `_td-content.html`, `docs/list.html`, `blog/_td-content.html`) | project `layouts/` | No — primitives only |
| Docsy theme | module cache | **No** |

**Not vendored.** `hugo mod vendor` fails on Docsy with Hugo 0.166: the theme mounts `node_modules/bootstrap` and Font Awesome, Hugo resolves those mounts to the *project's* `node_modules`, and vendoring then joins that absolute path under the module-cache dir (`stat …/theme@…/Users/…/node_modules/bootstrap: no such file`). So the editor bundle has none of Docsy's templates, i18n or config, and the project supplies what the editor needs from them:

- **Config.** The editor loads only the project's `hugo.yaml`. `outputs` names Docsy's `print` output format, so `hugo.yaml` repeats Docsy's `outputFormats` (`print`, `LLMS`); without them the editor can't load the config and every block fails with `unknown output format "print"`. Docsy's other config (`params.time_format_*`, `rss_sections`, the KaTeX/Mermaid versions, the woff media types) is used only by page templates, which the editor never renders. When upgrading Docsy, compare its `hugo.yaml` `outputFormats` with ours.
- **Templates.** Every component the editor re-renders is a project partial, and none calls a Docsy partial.
- **i18n.** The one Docsy string the blocks use, `ui_read_more`, is repeated in project `i18n/en.yaml`, which is bundled.

**Partials are in `layouts/partials/`, not Hugo 0.146+'s `layouts/_partials/`.** The module's template discovery (`find-template-files.html`) walks only `partials/`, `shortcodes/` and `_default/_markup/` in the project. A partial under `_partials/` builds fine but is missing from the editor bundle, so its component region can't re-render. Hugo still resolves `layouts/partials/` and it still overrides the theme's `_partials/` files.

## Section census

| Page | Section | Partial? | Treatment | Binding plan | Data completeness | Justification |
| --- | --- | --- | --- | --- | --- | --- |
| Landing pages (home, About, Community, new) | Block list | page template `landing.html` | array | `data-prop="content_blocks" data-component-key="_name"`; each item `data-component="{{ ._name }}"` | — | — |
| Landing | Cover | `blocks/cover` | component + text + array | `title`, `subtitle` (span), `description` (block, markdownify), `buttons` array → `text` | Image, colour, height, anchor, link-down, byline: sidebar (structure inputs) | Background image is CSS `background-image`, not an `<img>` — no image region; edited in the sidebar |
| Landing | Lead | `blocks/lead` | component + text | `content` (block) | colour/height/below_navbar in sidebar | — |
| Landing | Features | `blocks/features` | component + array | `features` array → `title` (span), `content` (block) | icon, url, url_text in sidebar | Link text is a `default`ed i18n fallback — sidebar |
| Landing | Section | `blocks/section` | component + text | `content` (block) | colour/height/switches in sidebar | — |
| Community | Community links | `blocks/community-links` | component + text + data-file array | `user_heading`, `user_intro`, `developer_heading`, `developer_intro`; lists `@data[links].user` / `@data[links].developer` arrays with `name` text per item | desc/url/icon in the Links data file | — |
| Landing | Markdown body under blocks | `landing.html` | text | `@content` | — | Only when a landing page has a body |
| Docs page / section / Text page (`type: docs`) | Title, description, body | page templates `_td-content.html`, `docs/list.html` (project overrides) | text | `title` (span), `description` (block, markdownify), `@content` | Taxonomies, reading time, last-modified: computed | — |
| Blog post | Title, description, body | `blog/_td-content.html` (override) | text | `title`, `description`, `@content` | Byline (author markdownify + formatted date): sidebar | Formatted date + markdownified author string — sidebar-only per skill |
| All pages | Navbar | Docsy `navbar.html` (project override, page context) | sidebar-only | — | Site title & logo: `hugo.yaml`/`assets` (developer-owned). Menu items: each page's `menu.main` front matter | Nav is Hugo's `site.Menus.main`, built from every page's front matter; no single file to bind. Edited per page in the sidebar |
| All pages | Footer link icons | `footer/left.html`, `footer/right.html` (overrides) | data-file + array | `@data[links].user`, `@data[links].developer`; items have no visible text (icon + tooltip) | name/url/icon/desc in `data/links.yaml` | Items are icon-only: array region gives reorder/add/remove; fields edit in the sidebar |
| All pages | Footer copyright | `footer/center.html` (override) | data-file text | `@data[footer].copyright_authors` (text, markdownify) | Year range computed from `copyright_from_year` + now | — |
| All pages | Footer privacy/about links | `footer/center.html` | sidebar-only | — | Link labels are Docsy i18n strings; URL in `data/footer.yaml` | i18n strings are theme translations, not content |
| Docs/blog sidebars, TOC, breadcrumbs, section index, blog list, taxonomy pages | generated | Docsy | sidebar-only | — | Built from page titles/weights | Generated from other pages — edit the pages |
| 404, search | Docsy layouts | — | none | — | i18n only | No content file |
