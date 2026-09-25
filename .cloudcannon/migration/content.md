# Content — Docsy starter

This is a starter, so content was rewritten as CloudCannon-oriented placeholder copy rather than preserved. Parity with the baseline is therefore structural (same theme chrome, same page types), not page-for-page.

## Structural changes

- Home, About, Community → `layout: landing` + `content_blocks` (`blocks/cover`, `blocks/lead`, `blocks/features`, `blocks/section`, `blocks/community-links`). Replaces Docsy's `blocks/*` shortcodes, the inline HTML CTA buttons and `_param` interpolation.
- `height="full td-below-navbar"` class-string hack replaced with a `below_navbar` switch per block.
- Cover background images moved from bundle resources (`**background*` glob) to `static/images/` and a block `image` field.
- Blog posts converted to leaf bundles (`<slug>/index.md`) so every post can hold its own images. First post image renamed `sunset.jpg`.
- Removed: `site.md` (Netlify build info), `docs/concepts.md`, `examples.md`, `contribution-guidelines.md`, two tutorial stubs. Added `privacy.md` (footer link target).
- `docs/getting-started/example-page.md` → `writing-docs.md` (formatting + every snippet type); `reference/parameter-reference.md` → `front-matter.md`.
- `draft: false` added to every docs page and post.
- Menus kept as flow-style YAML (`menu: { main: { weight: 10 } }`) — CloudCannon will rewrite to block style on first save.

## Build

`npm run build` — 57 pages, no new warnings (only the no-commits git warning).
