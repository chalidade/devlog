# Tools: A Music Category and an Installable App

The same evening the [tools site](https://chalidade.github.io/tools/) got a new
Music category with seven tools, all on the browser's own Web Audio API with no
extra library and no sample files. Claude Code wrote the code from my list.

- **Guitar tuner:** McLeod pitch detection (NSDF) on the microphone, decimated so
  each analysis takes under 1 ms, with 8 tunings plus bass, ukulele and chromatic
- **Metronome** on a Web Audio lookahead scheduler, with accents, subdivisions and
  tap tempo
- **Chord dictionary:** guitar and ukulele shapes computed for 12 keys × 16 chord
  types, playable, plus a transposer that keeps chord columns aligned and
  suggests a capo
- **BPM & key detection** in a Web Worker: onsets and a comb search for tempo, a
  chromagram matched against Krumhansl key profiles for the key
- **Piano:** every note synthesized and cached, 88 keys, 6 voices, multi-touch,
  computer keyboard and Web MIDI, and a practice mode where the next key lights up
  and waits (7 public-domain songs, scales, or your own MIDI file)
- **Guitar:** Karplus-Strong strings with an all-pass filter for fractional
  delay, which keeps every fret within about 2 cents; strum by swiping
- **Drums:** 9 synthesized pads and a 16-step sequencer, measured at 125 ms per
  step at 120 BPM
- Fixing the tuner turned up a real bug: notes above about 1 kHz sometimes read a
  fifth low, because downsampling left too few samples per period. It is now
  capped at 16 samples per period at minimum

Then the site became **installable** (manifest, icons and a service worker
generated at build time: pages network-first, build files cached on first use, so
it never downloads all tools up front). Piano, guitar and drums got a full-screen
mode that turns a phone sideways, and a tool chunk that fails to load now shows a
message instead of a blank page.

**Lesson:** an instrument is judged by ear and by latency, and neither shows up in
a build. The cents-level tuning and the sequencer timing only got fixed because
they were measured, not because they sounded "fine" at first.
