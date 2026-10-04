# Dry run: "Add French and German to this site" (Docsy, setup A)

Skills followed: `make-site-multilingual/SKILL.md` → `hugo/overview.md` → `hugo/native-multilingual.md` (setup A), then `translate-site/SKILL.md` → `translate-site/content-directories.md` and its scripts.

## What I did, step by step

| Doc section | What I did |
| --- | --- |
| `SKILL.md` § SSG detection | Hugo, so read `hugo/overview.md` before anything else. |
| `hugo/overview.md` § Choose a setup | Q1: one `languages` entry only, so not on Hugo multilingual yet. Q2: layouts come from the Docsy module, so **setup A**. Followed `native-multilingual.md` instead of `setup.md`. |
| `native-multilingual.md` § 1 Audit | Config had `languages.en` only. Content: `content/` only. UI strings: site `i18n/en.yaml` (1 key), theme's `i18n/` found with `hugo config mounts` (ships `fr.yaml`, `de.yaml`). Menus: front matter. Data: `footer.yaml` (`footer/center.html`), `links.yaml` (`footer/left.html`, `footer/right.html`, `blocks/community-links.html`). Link fields: cover buttons, feature links, footer privacy link, community links (all `relURL`). Dates: site-owned `blog/_td-content.html`; theme-owned `blog/list.html`, `page-meta-lastmod.html`, print. Search: Docsy's offline index ranges over `hugo.Sites`. |
| § 2 Content directory per language | Added `fr` and `de` to `languages` with `contentDir: content_fr` / `content_de`, `label`, `weight`, per-language `title` and `params`. English stays at the root. |
| § 3 Untranslated pages | User policy: every page in every language. Copied all 18 English `.md` files into each of `content_fr/` and `content_de/` (bundle images not copied: § 2 says they're shared). Every section has an `_index.md`, so no empty auto-created sections. |
| `translate-site` Part 2 | Ran `prepare-content-translation.mjs --source-dir content --locale-dir content_<l>` for fr and de; added `translated_frontmatter` / `translated_body` for `_index.md`, `about/index.md`, `docs/overview.md` only; ran `merge-content-translation.mjs`. |
| § 4 Link fields | Added `layouts/partials/localized-url.html` (the doc's `site.GetPage` snippet as a returning partial) and used it in `blocks/cover.html`, `blocks/features.html`, `community/links-list.html`, `footer/center.html` (privacy link). `footer/editable-links.html` already used `site.GetPage`. |
| § 4 `data/` files | Added the doc's `lang-data.html` helper. `footer.yaml`: `copyright_authors` keyed by `en`/`fr`/`de`; year and privacy URL left shared at the top level ("move only the text"). `links.yaml`: whole `user`/`developer` lists duplicated under `en`/`fr`/`de` (text translated). Updated four templates to read through the helper and to emit `@data[<file>].<lang>.…` props. |
| § 4 Dates | Site-owned `layouts/blog/_td-content.html`: `time.Format ":date_full" $.Date`. Theme-owned blog list date left English (user declined theme overrides). |
| § 4 `hreflang` | Appended the doc's snippet to the existing Docsy hook `layouts/partials/hooks/head-end.html`. |
| § 4 Search (accepted override) | Copied Docsy's `assets/json/offline-search-index.json` (now ranges over `site.Pages`) and `search-input.html` (target name `offline-search-index.<lang>.json`), `chmod u+w`, theme version noted in a header comment. Put the partial in `layouts/partials/` to match this site's convention. |
| § 4 Site `params` text | Per-language `params.description` and `params.taxonomy.taxonomyCloudTitle` under `languages.fr` / `languages.de`. |
| § 4 Taxonomy term titles, hardcoded theme text | Left English (user declined the theme overrides; term titles left for later with the other untranslated copies). |
| § 5 UI strings | Expanded `i18n/en.yaml` to 10 keys and added `fr.yaml` / `de.yaml`, starting from Docsy's own translations. |
| § 6 CloudCannon | Added `pages_fr/docs_fr/blog_fr/pages_de/docs_de/blog_de` (copies of the English collections with every path, URL, `new_preview_url` and upload path changed), a `ui_strings` collection, collection groups per language, `file_config` labels for every `i18n` key, and `en`/`fr`/`de` object inputs on `footer.yaml` and `links.yaml`. Validated against `.cloudcannon/migration/cloudcannon-config.latest.schema.json` (0 errors). Updated `.cloudcannon/README.md` (how translations work for editors) and `README.md` (new files, override diff instructions). |
| § 7 Verify | See below. |

## Build results

`npm ci` then `PATH=node_modules/.bin:…/.bin:$PATH npm run build` (Hugo 0.166.0 extended): clean, no warnings. EN 58 / FR 56 / DE 56 pages (baseline EN 57; the extra EN page is Hugo's `/en/` → `/` redirect).

## Verified in `public/`

- **Page parity:** list of `.html` files under `public/fr/` and `public/de/` (prefix stripped) is identical to the English list; English list identical to a baseline build of the untouched commit (`git archive HEAD`, built in scratch).
- **English unchanged** apart from expected additions: diffed home, About, Community, a blog post, Overview and the blog list against the baseline build — only the `hreflang` links, Docsy's language menu, the editor bundle hash and the post date format changed.
- **Translated pages:** `/fr/`, `/de/`, `/fr/about/`, `/de/about/`, `/fr/docs/overview/`, `/de/docs/overview/` have French/German `<h1>`, description, blocks, table body. Other copies are English, by policy.
- **`<html lang>`** is `fr`/`de` on every language's pages (home, 404, search checked).
- **Link fields:** `/fr/` cover buttons → `/fr/docs/`, `/fr/docs/getting-started/`; feature links → `/fr/docs/...`; footer privacy → `/fr/privacy/`, About → `/fr/about/`. Markdown links (`/community/` in privacy.md, relative links in getting-started) are localized by Hugo.
- **Data text:** footer copyright `Les auteurs du Docsy Starter` with `data-prop=@data[footer].fr.copyright_authors`; community page and footer link props `@data[links].fr.user` / `.developer`, French names and descriptions.
- **UI strings:** footer "Tous droits réservés" / "Alle Rechte vorbehalten", privacy label, search placeholder, cover down-arrow `aria-label` ("Lire la suite" / "Weiterlesen"), byline "Par".
- **Dates:** post page `mardi 1 septembre 2026` / `Dienstag, 1. September 2026`; English became `Tuesday, September 1, 2026` (was `September 01`). Blog list stays `Tuesday, September 01, 2026 dans News` (theme template, declined).
- **`hreflang`:** en, fr, de and `x-default` on every page checked.
- **Search:** three files `offline-search-index.{en,fr,de}.<hash>.json`, each of 27 entries; FR index has only `/fr/` refs and title "Vue d'ensemble"; each language's search input (including `/fr/search/`) points at its own file. English index hash is identical to the baseline's.
- **Language switcher** (Docsy built-in) on `/fr/docs/overview/` links to `/docs/overview/` and `/de/docs/overview/`.
- **Bundle image:** `imgproc sunset` renders on `/fr/` and `/de/` first-post from the English bundle.
- **Taxonomy cloud titles** French/German; "Tags:"/"Categories:" labels stay English (theme-hardcoded, declined).
- **No `slug`/`url`** in any content file.
- Editor bundle (`public/_cloudcannon/live-editing.*.js`) contains `i18n/fr.yaml`, `i18n/de.yaml` and the French strings.

## How the translate-site scripts behaved

- `prepare-content-translation.mjs` on the whole `content/` dir: walked all 18 files including bundles; manifests named as documented (`.translation-task-fr-content-content_fr.json`). Field extraction was good: block text by path, `linkTitle: ''`, menus, images, URLs, `_name`, colours skipped; `resources.0.params.byline` offered (correct, it's a photo credit). Shortcodes kept in the body.
- `merge-content-translation.mjs`: `--dry-run` showed exact YAML, preserved `|-` block scalars, flow-style `menu: { main: … }`, key order and quoting. Patched 3 files, "Skipped: 15 (no translations provided)", then deleted the manifest.
- Re-running prepare afterwards: `about` and `overview` "already_translated", but **`_index.md` is offered again** as untranslated with only `title: Docsy Starter`, which I kept the same on purpose (it's the product name). See friction.

## Friction table

| Doc file + section | What it said | What actually happened / what was missing | What I did |
| --- | --- | --- | --- |
| `translate-site/content-directories.md` § Phase 2.1 (classification) | Classification is "binary": untranslated (frontmatter text + body still match source) vs already translated. Part 1 has `translate-site-keep.json` for values deliberately kept. | Classification is actually per field. Once translated, the home page is offered again as "untranslated" on every later run, because one field (`title: Docsy Starter`, a brand name) was rightly left the same. Part 2 has no keep list. On a real site, every brand-name title or kept term brings its file back each run, and the doc's description of "binary" doesn't explain it. | Left it; noted that the re-offered manifest lists only the kept field. |
| `translate-site/content-directories.md` § Phase 2.2–2.3 | Translate every file with `"status": "untranslated"`. | Nothing covers translating **only some** files from a manifest (the user's "translate these three now, the rest later"). The merge happens to handle it: "Skipped: 15 (no translations provided)", then it deletes the manifest. That works, but a user can't tell from the doc that it's safe. | Filled in 3 entries per manifest; the merge skipped the rest. |
| `native-multilingual.md` § 4 Dates | "Dates in theme-owned templates (list pages, last-modified lines) stay English without a layout override." `:date_*` tokens change the default language's output too. | On this site the post-page date is in a **site-owned** override (`blog/_td-content.html`), so it can be fixed with no new theme override, but the blog list (theme `blog/list.html`) can't. Result: the English post now says `September 1` while the English blog list still says `September 01`, and `/fr/blog/` mixes an English date with French `dans News`. The doc doesn't warn that fixing one date and not the other leaves English inconsistent too. | Used `:date_full` (the closest to the existing format); recorded the mismatch. |
| `native-multilingual.md` § 4 `data/` files | Key the file by language; "URLs and icons are duplicated in each language's section. Keep them in step, or move only the text into the language sections." | Moving only the text works for flat files (footer), but not for a list of objects that mixes text with URLs/icons (`links.yaml`). That leaves duplicating the whole list per language, so adding a link means adding it in three places. The doc doesn't cover arrays, or whether shared top-level keys may sit next to language keys (they can: the helper ignores them). | Footer: shared year/URL at top level, text per language. Links: full lists per language, with a comment in the file and a note in the editor README. |
| `native-multilingual.md` § 5 UI strings | "Copy the theme keys editors should be able to change" into `i18n/<lang>.yaml`. | No guidance on which keys: Docsy has ~60. Each copied key also stops picking up theme wording updates. A user has to guess. | Picked the 10 visible keys on this site's pages (read more, search, pager, footer labels, byline, last modified, TOC heading, print link). |
| `native-multilingual.md` § 4 Search | Override `assets/json/offline-search-index.json` and "the partial that names it (`search-input.html`)". | The doc doesn't give the partial's path. Docsy has it at `layouts/_partials/search-input.html`, but this site keeps overrides in `layouts/partials/` because the editable-regions bundle only walks `partials/` (site README). Either path builds. | Used `layouts/partials/search-input.html`; worked. |
| `native-multilingual.md` § 4 gap table (taxonomy term titles) and § 3 policy | Fix term titles with `content_fr/tags/<term>/_index.md`. Policy "every page exists in every language": copy every English `.md`. | No guidance on how the two interact: term pages exist in every language automatically, but their titles are English slugs (`editing`, `Guides`) unless term `_index.md` files are created, and the English site has none to copy. | Didn't create term files (left for later with the other untranslated copies); recorded. |
| `native-multilingual.md` § 6 CloudCannon / § 2 bundles | § 2: "Bundle images can stay in the English bundle." § 6: set the French blog's uploads to `content_fr/blog/[relative_base_path]`, "not the English bundle". | Both hold, but together they mean a French post shows images from the English bundle until an editor uploads one, and then it uses its own copy. That's fine, but neither section says so, and an editor can't see the English bundle's images from the French post's folder. | Followed § 6 as written; added a line to the collection description. |
| `hugo/overview.md` § Coverage note / `native-multilingual.md` § 4 `data/` | Visual editing on `/fr/` pages and editing `i18n` are "not yet tested in the CloudCannon editor". | The `lang-data.html` helper keys on `site.Language.Lang`. If the editor's in-browser Hugo renders a `/fr/` page's re-rendered component (the community-links block) as the default language, that block will show English links and point its regions at `@data[links].en`. Nothing in the docs says which language the editor renders. Can't verify locally. | Flagged as a manual check below. |

Smooth, worth keeping: the setup choice (two questions, clear answer A); the `hreflang` snippet and the "Docsy head hook" pointer; the search fix (the warning about `ExecuteAsTemplate` caching by target name was exactly right); the `lang-data.html` helper; the `site.GetPage` link fix; the per-language `params` merge (Hugo deep-merged `params.taxonomy`, the cloud still renders); "Markdown links need nothing" (confirmed).

Defaults I picked because the docs didn't say: `:date_full` token; which 10 `i18n` keys to copy; translated the footer and links data text now (short, site-wide) even though only three pages were asked for; `ui_read_more` FR as "Lire la suite" rather than Docsy's "Lire plus".

## Manual checks for CloudCannon (after pushing)

1. The sidebar shows the English / Français / Deutsch / Site data groups, and each French and German collection lists 18-file mirrors with the right URLs (`/fr/about/`, `/de/docs/overview/`). The home `_index.md` in `pages_fr` opens at `/fr/`.
2. Open `/fr/` in the Visual Editor: edit a cover title and a feature text, save, reload. The edit should be in `content_fr/_index.md`, not `content/_index.md`.
3. Open `/fr/community/` in the Visual Editor. The community-links block should show the **French** link names, and editing one should change `links.yaml` → `fr.user[…]`, not `en`. (This is the editor-language question: does the in-browser renderer run the French site?)
4. On a French page, edit the footer copyright inline. It should change `footer.yaml` → `fr.copyright_authors`.
5. Re-render of blocks in the editor on `/fr/`: the cover down-arrow and feature "read more" text should be French (`ui_read_more` from `i18n/fr.yaml`), and feature/button links should still point at `/fr/…`.
6. **Site data → UI strings**: each file shows labelled fields (not raw keys); change `fr.yaml` → `ui_read_more`, save, and confirm it appears on `/fr/` after the rebuild (not live).
7. **Site data → Footer / Links**: the English / Français / Deutsch object sections appear; Links' per-language `user`/`developer` arrays still use the Link structure (add one).
8. Add a new French blog post (`blog_fr` → + Add): it lands under `content_fr/blog/...`, previews at `/fr/blog/...`, and an uploaded image goes into the French post's folder.
9. The `new_preview_url` for each French/German schema opens a page in that language.
10. The language menu in the navbar (and that it doesn't break the Visual Editor on `/fr/` and `/de/` pages).
