# VWO Job Fair: VIP Stands, a Faster Hall, and the HR-to-Applicant Loop

[VWO](https://chalidade.github.io/vwo/) is a virtual cafe and job fair you walk
through as a character. Today four PRs merged (#16 to #19). Claude Code wrote the
code; I tested each build on my phone, sent back what looked wrong, and decided
what shipped.

- **Hall is faster on phones:** the map now draws only what is on screen, and the
  simulation pauses when nobody is watching it. Measured at phone size with the CPU
  throttled 4× in headless Chromium: 25 → about 43 fps
- VIP stands are one tile wider on each side, with brand banners, a gate (four
  styles, editable text) and a big video wall that plays the company's video.
  Organisers configure tier, theme, add-ons and video link per stand
- Fixed the logo memory game: the hall re-renders every frame and passed a fresh
  array, so the cards reshuffled on every frame and no pair could ever match
- Closed the loop between HR and applicants: scheduling an interview in the company
  portal now shows the applicant an invitation card with a calendar file, and chat
  or status changes arrive as notices. Organiser announcements finally reach visitors
- Also shipped: bookable empty stands, company login with code and PIN, an ads page,
  map zoom, and semi-3D characters with hijab, peci and batik options

**Lesson:** a feature that only exists on the sender's screen is not a feature. The
announcement box saved, the interview saved, and nobody on the other side ever saw
them. Test every feature from the receiver's side too.

**Next:** the job fair still runs entirely in the browser. Move it onto the server
the cafe already has, starting with the database and real logins.
