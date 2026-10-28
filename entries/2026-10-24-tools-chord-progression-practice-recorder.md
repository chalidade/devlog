# Tools: Chord Progressions and a Practice Recorder

Day 7 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
went back to music: two tools, 59 in total.

- **Chord progression:** pick a pattern (pop I–V–vi–IV, the 50s progression,
  canon, ii–V–I, 12-bar blues, four minor patterns and more) and a key, then
  hear it on guitar or piano at a tempo you choose, one or two bars per chord.
  Transpose by semitones, copy the chords as text, or open them in the online
  guitar through `?chords=C,G,Am,F`
- **Practice recorder:** record from the microphone with a metronome and a
  one-bar count-in. The click plays through the speaker only, so it isn't in
  the recording. On playback the click is laid back on top, with a ±200 ms
  slider for latency. Save as WAV, MP3 or M4A
- The metronome's click moved to `metronome/click.ts` so both tools share it

**Lesson:** the hard part of recording with a metronome is the click itself.
Keeping it out of the recording and adding it back on playback is what makes
the take usable, and latency differs per device, so the offset had to be
adjustable.
