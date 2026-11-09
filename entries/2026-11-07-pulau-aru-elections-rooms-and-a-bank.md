# Pulau Aru: An Election, Rooms Inside and a Bank

Episodes 13 to 19 of [Pulau Aru](https://pulau-aru.web.id/), where the island
started to have politics and a cast.

- **Rooms inside buildings.** Interiors you can walk into, locked until an episode
  opens them. Furniture meshes are merged and add no light, so entering a room
  doesn't recompile shaders, and its memory is freed on exit
- **Places to do things:** sit and order at a food stall, work shifts at the
  island office for coins shared with the garden game, and a Bank Pulau with daily
  interest on savings
- **An election.** In episode 15 the president and vice president resigned, both
  seats went empty, and the most-liked candidate comment won. An election board,
  banners and candidates carrying placards are in the game, not only in the video
- **A cast of residents.** Fourteen recurring residents with fixed nicknames,
  traits, poses and catchphrases, defined once in a `warga.json` and reused across
  episodes
- **New rule:** everything shown in an episode must exist on the website. The
  runbook now checks that before an episode is delivered
- Two episode videos were lost when the session couldn't upload releases, so
  videos are now saved on a `videos` branch instead

**Lesson:** "the video matches the game" only holds if something checks it. A
written step in the runbook enforces it better than intending to keep them in sync.
