# Tools: Every Tool Gets Its Own Address for Google

The [tools site](https://chalidade.github.io/tools/) was close to invisible to
search. Every tool lived at `#/<slug>`, which Google treats as one page, there
was no sitemap, and the text about each tool only existed after JavaScript ran.
PR #7 fixes that. Claude Code wrote it; I set it up in Google Search Console.

- **One real page per tool and language:** `/tools/compress-pdf/` in Indonesian
  and `/tools/en/compress-pdf/` in English. A build step writes an `index.html`
  into each folder (102 pages), each with its own title, description, canonical,
  `hreflang` and JSON-LD, and the tool's text as static HTML. GitHub Pages serves
  those files directly, so a reload no longer 404s, which was the old reason for
  hash routing
- **The address decides the language.** The site used to pick Indonesian or
  English from the browser. Googlebot browses as `en-US`, so it would have seen
  English on the Indonesian URLs. Now an Indonesian address always renders
  Indonesian; the ID/EN switch moves to the other address and remembers the
  choice, and only a stored choice (which a crawler never has) redirects
- **Links are plain `<a href>`** that the app intercepts for `pushState`, so
  they work without JavaScript and a crawler can follow every one. Under each
  tool there is now a short "why it is safe" list and links to related tools
- Old `#/<slug>` links are rewritten to the new path on load. Embed snippets
  already pasted on other sites (`#/<slug>?embed`) keep working unchanged
- `sitemap.xml` with all 102 pages, `robots.txt` at the domain root (the
  `chalidade.github.io` repo, since robots is only read there), and the property
  verified in Search Console with an HTML file under `/tools/`
- Checked with 21 browser checks against the built site served under `/tools/`,
  including an English-locale browser on Indonesian pages and a run with
  JavaScript turned off

The same day I also asked "what else should the site have", and the
[roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md) grew from
three planned days to Day 30: Islamic tools (prayer times, qibla, Hijri dates,
zakat), small-business tools (QRIS with an amount, receipts), privacy tools (an
ID-card watermark, photo redaction, PDF redaction, file encryption), scan and
OCR, and more. None of those are built yet; they are plans with the constraints
written down (self-hosted wasm, nothing sent to a server).

**Lesson:** for a single-page app, "can Google see it" is three questions, not
one: does each page have its own URL, does that URL return real text without
JavaScript, and does the crawler get the language the URL promises. The third
one I would have missed without thinking about who Googlebot pretends to be.

**Next:** watch Search Console for the sitemap status and the first indexed
pages; the sitemap showed "couldn't fetch" right after submission, which usually
clears on its own.

How it works: [Making a Hash-Routed App Findable on GitHub Pages](https://github.com/chalidade/devlog/blob/main/notes/making-a-hash-routed-app-findable.md).
