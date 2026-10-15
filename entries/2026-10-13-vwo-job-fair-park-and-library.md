# VWO Job Fair: A Park, a Library, and a Pre-Launch Audit

[jobfair.co.id](https://jobfair.co.id) is my virtual job fair. Today it got an
outside: a park you walk into from the lobby, with a building per event and a
public library, then a bug and security pass before showing it to people (PRs
#106–#113, about 10,000 lines added). Claude Code wrote the code, tests and
screenshots; I decided what the park should feel like, reviewed each screen and
sent back what looked wrong.

- The park is its own floor, so it gets its own realtime shard. Each event can
  have a building there; ones that are not ready show as a construction site with
  a coming-soon banner
- **Everything that makes the park feel alive runs only in the browser.** Joggers,
  a dog walker, kids on the swings, ducks and koi are computed from the clock, so
  every visitor sees roughly the same scene at zero realtime messages. Day and
  night follow Jakarta time, and a few night-only ghosts are claimable only when
  the server agrees it is night
- A library building reads free books from Project Gutenberg through a small
  allowlisted proxy, with a 15 s timeout and an OPDS fallback when Gutendex is
  slow. The reader parses Gutenberg's HTML edition into a fixed list of block
  types and lays it out as A5 book pages, two-up on a laptop
- The fountain animations kept restarting whenever someone walked past. The
  cause was the scene re-sorting sprites by depth, which made React move DOM nodes
  and restart their CSS animations; depth is now a z-index and node order stays
  stable. Measured restarts in 5 s went 3 → 0
- The audit fixed 8 issues, including a company website field that accepted
  `javascript:` links shown to organisers, old cafe-prototype pages that were
  still reachable, and a booth PIN that could be guessed from many accounts. A
  local load test held 50 concurrent requests at about 390 req/s, p95 277 ms

**Lesson:** ambient life does not need a server. If everyone derives the same
scene from the same clock, a crowd of extras costs nothing to sync.

**Next:** a rehearsal with real visitors on phones and laptops before the first
public event.
