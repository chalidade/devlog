# VWO Job Fair: Clothes You Earn, and Shorter Event Links

Besides the advertiser work, [jobfair.co.id](https://jobfair.co.id) got four
smaller PRs (#124–#128), written by Claude Code with tests.

- **Wardrobe from missions.** The character creator now starts with a small set
  (5 hair styles, 4 outfits, every skin tone). Everything else comes from 15 item
  missions across the fair: visiting stands, applying, the psychometric test, the
  seminar, the park and library, a consultant, mini-game scores. No coins involved.
  Unlock rules are pure functions with vitest tests, the saved wardrobe is checked
  with a zod schema, and characters made before this keep what they wear
- **Pre-registration at `jobfair.co.id/<slug>`.** The old `/daftar/<slug>` now
  redirects there (308, query kept). Names the site already uses are refused when
  an event is created or renamed, and a test fails if someone adds a new top-level
  route without reserving it. Links also ignore letter case (`/UNNES` → `/unnes`)
- **A redesigned sign-up page:** the banner shown whole whatever its shape, the
  event facts with a deadline countdown in WIB, and a three-step form with a
  progress bar, Indonesian inline messages and a draft kept in the tab. The
  anti-bot checks are unchanged
- A `CLAUDE.md` codebase guide: map, commands, conventions and env var names

**Lesson:** a short URL claims a namespace. The test that fails when a new route
isn't reserved matters more than the redirect, because the collision would only
show up months later.
