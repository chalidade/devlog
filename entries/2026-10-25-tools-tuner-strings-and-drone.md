# Tools: Violin, Viola and Cello in the Tuner, Plus a Drone

Day 8 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
added no new tool. The guitar tuner got two additions instead, so the count
stays at 59.

- **Violin (G D A E), viola (C G D A) and cello (C G D A)** tunings next to the
  guitar, bass and ukulele ones
- **The analysis window widens for low notes.** Cello goes down to C2, and a
  window sized for guitar is too short to hold enough cycles of a note that
  low, so the tuner picks a longer one automatically to keep detection stable
- **A reference drone:** a string's note, or any note from C2 to C6, that keeps
  sounding until you stop it, for tuning by ear or practising intonation. It
  follows the A4 setting

**Lesson:** pitch detection needs to see a few full cycles of the note. The
lower the note, the longer the window has to be.
