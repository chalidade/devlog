# VWO Job Fair: Fitting a Crowd Into the Free Realtime Budget

[jobfair.co.id](https://jobfair.co.id) is my virtual job fair. Planning for 3,000
visitors showed the realtime layer would blow through Supabase Free's 100
messages a second long before the database struggled, so I asked for the load to
fit the free tiers first, with every limit as an env var I can raise when there is
budget (PRs #103–#105). Claude Code wrote the code and the load simulations; I set
the constraints, chose the order and tested the result on two devices.

- **Movement is sent as intent, not position.** A click sends one message with
  the route and speed and every screen walks the player along it; floors are
  sharded into channels of 10, Presence replaces the hello-reply storm, and DMs go
  to the recipient's inbox channel. Simulated 100 players: about 4,560 → 58
  messages a second
- Seminars can stream from a YouTube or Vimeo link instead of the speaker's
  laptop, which tops out at 8 direct viewers; a room-wide slow mode holds chat to
  a budget. Simulated 200 watchers: about 2,500 → 40 messages a second
- The public event state is cached at Vercel's edge with an ETag and private
  data moved to its own endpoint; logos are served once by content hash. On
  synthetic data with 60 companies the payload went 660 KB → 115 KB, and a
  visitor's requests 19 → 8 a minute, zero while the tab is hidden
- Every limit lives in env (`LIVE_MSG_BUDGET`, `LIVE_FLOOR_CAP`,
  `STAGE_MESH_MAX_VIEWERS`, poll intervals, DB pool size) and reaches the static
  game through one cached config endpoint, so raising them needs no rebuild

Smaller changes the same day: floors that can be closed as "coming soon", a
consultant lounge with bookable desks, 12 stands per floor, booth booking as an
inquiry form, and more anomaly easter eggs with a per-account collection.

**Lesson:** on a managed realtime plan the bill is messages, not users. Designing
what goes over the wire mattered far more than upgrading the database tier.

**Next:** a park outside the building where each event gets its own building,
future ones shown under construction.
