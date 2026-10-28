# Tailwind's Layers vs WordPress's CSS

When weeknoo started exporting React sites as WordPress block themes
([the entry](https://github.com/chalidade/devlog/blob/main/entries/2026-09-09-weeknoo-wordpress-theme-export.md)),
the theme loaded the site's compiled Tailwind CSS next to WordPress's own block
CSS. The page looked almost right. One section had 16 px too much space.

## The problem

Tailwind v4 emits everything inside cascade layers: `@layer theme, base,
components, utilities`. WordPress core's block CSS has no layer.

In the cascade, **an unlayered rule beats every layered rule**, whatever the
specificity. Specificity is only compared between rules in the same layer. So:

- `:where(figure){margin:0 0 1em}` from core has zero specificity, and it still
  beat Tailwind's preflight reset. That's the extra 16 px
- `.is-layout-flex > :is(*,div){margin:0}` from core beat `.mt-6` on a section

Nothing in devtools looks wrong at first. The winning rule is a weak selector,
and the losing one is the more specific utility, which is backwards from what
you'd expect until you remember layers.

## The fix

Remove Tailwind's `@layer` wrappers when building the theme, so both
stylesheets are unlayered and plain specificity decides. Utilities win again,
as they do in the React build.

The unwrapping in
[`scripts/wp/build-theme.mjs`](https://github.com/chalidade/weeknoo/blob/master/scripts/wp/build-theme.mjs)
is a small character scanner, not a regex:

- a `@layer name { … }` block drops its own braces and keeps the contents
- a bare `@layer a, b;` only declares an order, so it's removed
- escapes are skipped first, because Tailwind writes class names like
  `.\[\&_svg\:not\(\[class\*\=\'size-\'\]\)\]`, and that `\'` must not be read
  as the start of a string

## Gotchas that follow from it

- **Keep the theme's own CSS narrow.** Once everything is unlayered, a broad
  reset in the interop CSS would outrank the utilities on the sections too
- **Never use utilities in the generated templates.** Tailwind only compiles
  classes it finds in the site's source. A `page` or `404` template styled with
  `mt-8` gets nothing if no section happens to use `mt-8`. Those templates use
  theme-owned classes (`site-main`, `site-content`) instead
- **Check with pixels.** A full-page pixel diff against the React version is
  what caught the 16 px. Looking at the page, I wouldn't have noticed
