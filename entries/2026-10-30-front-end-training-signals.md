# Front-End Training: Signals, From Knockout to the TC39 Proposal

Today's deep dive on
[Front-End Training](https://chalidade.github.io/front-end-training/), in
Indonesian and English.

- Automatic dependency tracking, built as a mini library around one global
  "who is running now" variable
- Why pure push causes glitches, and how push-then-pull gives laziness,
  equality cut-off and batching
- A short history, and the `Watcher` in the TC39 proposal, which is a core for
  frameworks rather than a framework
- Experiments checked against @preact/signals-core 1.14.5 and signal-polyfill
  0.2.2

**Lesson:** signals look like magic until you see the global variable. Then
every rule about reading inside an effect follows from it.
