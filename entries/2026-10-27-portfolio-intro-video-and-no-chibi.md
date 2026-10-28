# Portfolio: A 60-Second Intro Video, and the Chibi Comes Out

Two days of small changes to [my portfolio](https://chalidade.github.io/) and
[GitHub profile](https://github.com/chalidade), ending with the removal of the
chibi I [added on the 22nd](https://github.com/chalidade/devlog/blob/main/entries/2026-10-22-portfolio-chibi-that-waves.md).

- **Six years of contributions (26 October).** The experience section now uses
  numbers from my work account's contribution graph: 2,675 contributions in the
  past 12 months, plus a block per year from 2021 to 2025. The GitHub profile
  README got the same numbers
- **A 60-second intro video** above the hero on the portfolio and at the top of
  the profile README. On the portfolio it sits on a full-screen stage with a
  scroll cue, and the nav appears below it. It loads with
  `preload="metadata"` and a poster image, so the file only downloads on play
- **Saling Jaga** went into the builds list as an MVP
- **The log page reads `index.json`** from the devlog repo instead of the
  jsDelivr directory listing
- **The chibi is gone.** I first made it static, without the hover wave or the
  click greeting, then deleted the `_motion/` sources (about 1,700 lines), and
  then removed the chibi from the hero entirely. With the video at the top of
  the page, the chibi was a second introduction

**Lesson:** a page should introduce me once. When the video went in, the
chibi had nothing left to do, so I took it out, even though it had taken a day
to build.
