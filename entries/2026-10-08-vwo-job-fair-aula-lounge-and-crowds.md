# VWO Job Fair: Aula, a Call Lounge, Logins, and Busy Floors

[VWO](https://chalidade.github.io/vwo/) is a virtual cafe and job fair you walk
through as a character. Later the same day five more PRs merged (#20 to #24). Claude
Code wrote the code; I tested each build on my phone, sent back what looked wrong,
and decided what shipped.

- **Aula and live talks:** a new Aula floor with a stage, an MC and a rundown. A
  speaker's shared screen and voice now play on the Aula's LED wall and in a corner
  panel for every applicant in the room (WebRTC, one connection per viewer).
  Before this fix, the speaker's page showed the broadcast while the applicants'
  page stayed empty
- **Consultation lounge:** a new floor with big sofas, where applicants call an HR
  consultant or each other. A call costs coins up front, lasts 10 or 15 minutes,
  shows the time left and hangs up by itself
- **Accounts and pictures:** applicants sign in before entering (stored in the
  browser until launch, passwords kept only as a salted PBKDF2 hash), upload a
  profile photo, and companies upload their own logo. Images are redrawn on a
  canvas and only accepted as small base64 PNG, JPEG or WebP data URLs
- **VIP stands that look different:** five styles (gold, platinum, royal, garden,
  cyber) with their own ornaments and headline, so paying for VIP shows
- **Two-way notifications:** HR and applicants get a bell inbox. It replaced the
  mini map to keep the top bar clean. A security pass shared one URL check for all
  user links and bumped two vulnerable dependencies
- **Characters stop looking like paper:** turning left or right mirrored the sprite
  with a transition, so halfway through it was squashed to a 0 px line. The turn now
  snaps, with deeper shading, a soft contact shadow and idle breathing. A walk lean
  and a turn hop I tried read as choppy, so they came out again
- **Busy floors stay smooth:** at phone size in the production build, 150 visitors
  ran at 31 fps. The cost was CSS animations on parts inside each SVG sprite (eyes,
  arms, legs), since each one repaints the whole sprite every frame. With more than
  16 people on screen, everyone but the player now keeps only the walk bob: 31 → 58
  fps

**Lesson:** measure before guessing, and measure the build users get. The dev build
pointed at React (`jsxDEV` was the top function). The production build showed the
real cost was paint, and that small decorative animations were most of it.

**Next:** move the job fair onto the server, and send each player only the people
near them, so one floor can hold a crowd without loading every phone.
