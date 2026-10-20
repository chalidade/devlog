# Making a Hash-Routed App Findable on GitHub Pages

The [tools site](https://chalidade.github.io/tools/) is a React app on GitHub
Pages under a sub-path (`/tools/`). It used hash routing (`#/compress-pdf`)
because GitHub Pages has no rewrite rules: a path like `/tools/compress-pdf`
would 404 on reload. That choice also made every tool invisible to search, since
everything after `#` is the same page to a crawler. This is how it was turned
around without a server. The code is in
[chalidade/tools#7](https://github.com/chalidade/tools/pull/7).

## Real files instead of rewrites

GitHub Pages can't rewrite, but it serves `folder/index.html` for `folder/`. So
after `vite build`, a script (`scripts/seo.mjs`) copies the built `index.html`
into one folder per page and edits each copy:

- `<title>`, meta description, Open Graph and Twitter tags
- `<link rel="canonical">` and `hreflang` links for `id`, `en` and `x-default`
- a JSON-LD `WebApplication` block
- the page text as plain HTML inside `<div id="root">`, which React replaces on
  load. A crawler that doesn't run JavaScript still gets a heading, a
  description and links

The script reads the tool registry, which is TypeScript with React imports,
through Vite's `ssrLoadModule` rather than parsing it by hand. The same module
(`src/lib/seo.ts`) gives the app its titles and "about" text, so the static page
and the rendered page can't drift apart. It also writes `404.html` (marked
`noindex`) and `sitemap.xml` with the `hreflang` alternates.

## The language has to live in the URL

The app picked its language from `navigator.languages`. Googlebot renders pages
with an English browser, so an Indonesian URL would have been indexed in
English. The fix is that the address decides: `/tools/…` is Indonesian,
`/tools/en/…` is English. The header switch moves between the two addresses.

A visitor's own choice still wins, but only through storage: if `localStorage`
says English and the URL is Indonesian, the app replaces the URL before the
first render. A crawler has no storage, so it always stays on the URL it asked
for. Redirecting by browser language would have sent Googlebot away from every
Indonesian page.

## Links that work without JavaScript

Cards and related links are plain `<a href="/tools/merge-pdf/">`. One document
click listener intercepts same-site links (not modified clicks, not
`target=_blank`, not downloads) and switches pages with `pushState`, then
updates `<head>` so the canonical and title follow along. Without JavaScript,
or for a crawler, they are just links.

## Keeping old links alive

`#/<slug>` links are already out there (READMEs, chats). On load they are
rewritten with `history.replaceState` to the matching path, keeping query
parameters like `?bpm=128`. Embeds are the exception: `#/<slug>?embed` stays as
it is, because those snippets live on other people's sites.

## Gotchas

- `robots.txt` is only read at the domain root, so for a project site it goes in
  the `<user>.github.io` repo, not in the project
- Search Console's "Domain" property needs a DNS record, which you can't add to
  `github.io`. Use the "URL prefix" property for `https://<user>.github.io/<repo>/`
  and verify with the HTML file in `public/`
- The submitted sitemap is shown relative to the property (`/sitemap.xml`), which
  looks wrong but isn't. "Couldn't fetch" right after submitting usually clears
  on its own
- The service worker used to cache every navigation as the single shell page.
  With many real pages it now caches each page under its own URL as well
