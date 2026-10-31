# A Page That Renders the Same for Signed-In and Signed-Out Visitors

Some pages are loaded by someone else's frame: an e-learning player's exit page,
an OAuth return page, a payment provider's "done" screen. Inside a third-party
frame the browser can withhold your session cookie, so the same person may
arrive signed in one time and signed out the next. In a Next.js app with auth
middleware, that page needs its own way out of the middleware.

## The approach

The usual middleware has two rules: send signed-out visitors on private pages to
the login, and send signed-in visitors on public pages (login, sign-up) to the
dashboard. The obvious fix, adding the exit page to the public list, is wrong:
a visitor whose cookie *did* arrive gets redirected to the dashboard, which then
renders inside the other site's frame.

"Public" in that middleware means "for signed-out visitors only". A page that
must render for both needs to leave before either rule runs:

```ts
const PASS_THROUGH = new Set(['/embed-exit'])

export function middleware(req: NextRequest) {
  const { pathname } = req.nextUrl
  if (PASS_THROUGH.has(pathname)) return NextResponse.next()
  // ...auth rules below
}
```

Keep the page itself static: no session reads, no personalised data. It only
has to say "you can close this" or post a message to the parent window.

## Gotchas

- It works on localhost and fails in production, because locally the frame and
  the app share a site and the cookie is first-party. Test it from the real
  embedding origin.
- `SameSite=None; Secure` lets the cookie travel in some browsers, but
  third-party cookie blocking can still drop it. Design for the cookie being
  absent rather than trying to force it.

## When to use it

Any route that another origin loads in a frame or redirects back to. For routes
that only your own pages link to, the public/private lists are enough.
