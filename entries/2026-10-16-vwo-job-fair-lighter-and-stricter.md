# VWO Job Fair: 40% Less JavaScript on the Home Page, and a Stricter Server

[jobfair.co.id](https://jobfair.co.id) is my virtual job fair. Today was a
performance and hardening pass before the first public event (PRs #118 and
#119). Claude Code did the measuring, the code and the browser checks; I set the
goal, "light, fast, and nothing a visitor can abuse", and reviewed the results.

- **Screens load when they are opened, not up front.** The organiser hub,
  company portal, map, library and the rest of the hall screens became
  `React.lazy` chunks that prefetch once the player is inside. Gzipped JS on the
  home page went 253 → 152 KB, entering the game 350 → 270 KB, and the organiser
  hub 310 → 162 KB. Locally, first contentful paint went 960 → 348 ms
- zod was quietly shipping to every browser through shared modules. Schemas now
  live in `*-schema.ts` files that only the server imports, and a test fails if
  a browser entry point pulls them back in
- Every API route used to read the whole request body before validating it. A
  small streaming reader now stops at the size limit and returns 413, so a 30 MB
  POST is refused unread
- A full Content Security Policy on the game and the web pages, checked in
  Chromium across every portal tab: zero violations, and a planted script,
  iframe or cross-site fetch is blocked
- New booths no longer copy the requester's email into the public booth card,
  and a test now fails on any raw SQL that is not a constant

**Lesson:** bundle size creeps in through imports, not features. Measure what
a first-time visitor downloads, not what the build reports in total.

**Next:** a rehearsal with real visitors on phones and laptops before the first
public event.
