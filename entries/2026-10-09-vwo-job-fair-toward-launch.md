# VWO Job Fair: From Bot Demo Toward a Real Launch

[VWO](https://chalidade.github.io/vwo/) is a virtual job fair you walk through as a
character. Today five PRs merged (#25 to #29) and the plan changed from "demo" to
"launch on 18 October". Claude Code wrote the code; I set the scope, tested each
build on my phone and decided what shipped.

- **Split demo from live.** The GitHub Pages demo stays browser-only with bots. The
  live version gets its own server side: a Postgres schema for fairs, booths, jobs,
  applications and a coin ledger, plus accounts with scrypt password hashes, hashed
  session tokens, email verify and reset links, and a login rate limit
- **Coins as an append-only ledger.** A balance is the sum of a user's rows, every
  grant or charge carries an idempotency key, and a per-user advisory lock stops two
  taps from spending the same coins. Six racing charges against 50 coins in a test:
  exactly three succeed
- **Busy floors on a phone:** each look is drawn once as a cached picture and only
  the 40 nearest people render. With the CPU throttled 4x, 150 visitors went from
  8 to 11 fps to 17 to 24 fps
- **Organisers can build the venue.** A new floors tab adds or removes booth floors,
  switches rooms off and puts a coin price on any floor. Levels re-flow without gaps
  and promoters move with their floor
- Smaller changes: an info desk on every floor, the character editor shown once and
  then moved into the profile, and a new landing page with a live preview of the
  floors

**Lesson:** a demo that runs entirely in the browser is the fastest way to find out
what to build, but it hides the parts that need a server. Writing the money rules
(coins, idempotency, locks) as tested database code before any UI made the launch
plan concrete.

**Next:** move the job fair screens onto the live app and connect the game's login to
the server accounts.
