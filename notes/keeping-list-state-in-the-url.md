# Keeping List State in the URL

A paginated, filterable list feels broken when page 3 can't be bookmarked,
refreshed or reached with Back. Users don't report it as "state isn't in the
URL"; they report that Back threw them to page 1. The fix is to make the address
the source of truth for the list, not a copy of it.

## The approach

- **Write on change.** When the page changes, `history.pushState` a URL with
  `?page=N` (plus the filters). Use `pushState` for actions a user would want
  Back to undo (page, filter), `replaceState` for ones they wouldn't (typing in
  a search box).
- **Read on mount and on `popstate`.** One function parses the query into
  `{ page, filters, sort }` and applies it. Call it on first render and from a
  `popstate` listener, so Back and Forward restore the exact list.
- **Reset the page when the question changes.** Changing a tab, sort or filter
  goes back to page 1; otherwise page 7 of a filter with two pages is empty.
- **Pass state between pages through the URL too.** A menu that sets a filter
  from another page should navigate to `/catalogue?provider=<id>`, not put the
  value in a global store and push a bare `/catalogue`. A catalogue that reads
  its filters from the address on mount will overwrite whatever the store held.

## Gotchas

- Spreading an array of objects into query parameters gives
  `?provider=[object Object]`. Serialise ids, not objects.
- Next.js `router.push` re-runs data loading on the server. For client-only
  list state, `window.history.pushState` is lighter, and Next.js App Router
  keeps `useSearchParams` in sync with it.
- Store only what defines the list. Scroll position and open pop-ups don't
  belong in the URL.

## When to use it

Any list a user might share, bookmark or come back to: catalogues, search
results, admin tables. For a short list that fits on one screen, it's overhead.
