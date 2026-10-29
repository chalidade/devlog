# SCORM Exit Page Inside Someone Else's Frame

When a learner finishes a SCORM course, SCORM Cloud sends its frame to an exit
URL. The day before, I gave the LMS its own exit page instead of
`http://localhost/`. On production it still didn't render.

- The Next.js middleware redirected anyone without a live session cookie to
  `/`. Inside SCORM Cloud's frame the cookie can be dropped, because the frame
  is a third-party context, so the exit page never showed.
- Adding the route to the middleware's list of public paths was the obvious fix,
  and it was wrong. That list also sends a *signed-in* user from a public page to
  the dashboard. A learner with a working cookie would have seen the whole
  dashboard inside the course frame.
- The fix is an early pass-through for that one path, before any auth rule
  runs:

  ```ts
  if (path === '/scorm-exit') {
    return NextResponse.next();
  }
  ```

  It went out in the same day's release.

**Lesson:** "public" in this middleware meant "for logged-out users only". A
page that has to render the same for both kinds of visitor needs its own exit
from the middleware, not a place on the public list.
