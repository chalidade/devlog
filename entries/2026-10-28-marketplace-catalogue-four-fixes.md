# Marketplace Catalogue: Four Fixes

Four bugs from QA on the Lerero marketplace catalogue, each a small change in
the Next.js front end. Three went to production the same morning. The fourth is
waiting for review.

- **"Showing 10 of 433 items" on page 2.** The pagination label printed only the
  first item's position. It now prints the range the page holds, "Showing
  10–18 of 433 items", or one number when the page has a single item.
- **Picking a provider from the header menu.** Two bugs in one handler. It
  spread the menu's own list of provider *objects* into the filter, so the URL
  ended up with `[object Object]` four times. And from a product page it pushed
  a bare `/category`, where the catalogue reads its filters from the address on
  mount and overwrote the value the menu had just put in Redux. The pick now
  replaces the selection, and off the catalogue it travels in the URL as
  `?provider=<id>`, the way the old version did it.
- **Every product rated 4.8 in the "Added to Cart" pop-up.** The pop-up read a
  `rating` field that no cart item carries, then fell back to a hard-coded
  `'4.8'`. The card now passes the product's real average into the pop-up, and
  an unrated product shows no star at all.
- **The page number was not in the address.** Page 3 of the catalogue could not
  be bookmarked, refreshed or reached with Back. Page changes now push
  `?page=N` with `history.pushState`, and a `popstate` listener restores the
  filters and the page on Back and Forward. Changing a tab, sort or filter
  still starts again at page 1. This one is
  [a note](https://github.com/chalidade/devlog/blob/main/notes/keeping-list-state-in-the-url.md).

**Lesson:** two of the four were placeholders that outlived the feature: a
fallback rating that was never real, and a label that only had room for one
number. A placeholder needs a comment saying it is fake, or it ships.
