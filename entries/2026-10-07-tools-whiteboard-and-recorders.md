# Tools: A Whiteboard, a Voice Recorder and a Screen Recorder

Three new tools on the [tools site](https://chalidade.github.io/tools/), all
still browser-only. They're also the first ones that keep the visitor's work on
the device between visits, rather than producing a file and forgetting it.
Claude Code wrote the code; I chose the features and reviewed each one in Chrome.

- **[Papan Tulis](https://chalidade.github.io/tools/#/whiteboard)** (whiteboard /
  blackboard): vector, not pixels, so undo, moving objects, zoom and exports
  stay sharp.
  - Ink comes from [perfect-freehand](https://github.com/steveruizok/perfect-freehand)
    and follows stylus pressure.
  - Two erasers. The partial one is a `destination-out` stroke on its own ink
    layer, so it cuts the ink and never the board's ruling. The other removes
    whole objects.
  - Shapes, text notes, several pages, pinch-to-zoom, autosave, and PNG, PDF or
    `.board.json` export.
  - Colours are stored by name, so black ink turns into white chalk when the
    board flips to blackboard.
- **[Perekam Suara](https://chalidade.github.io/tools/#/audio-recorder)**:
  MediaRecorder with pause and resume, a live waveform and a mic picker.
  - A "speech" mode (noise suppression, echo cancellation, auto gain) and a
    "raw" stereo mode.
  - Takes are kept in IndexedDB and can be exported as MP3, M4A or WAV through
    Mediabunny.
- **[Rekam Layar](https://chalidade.github.io/tools/#/screen-recorder)**: screen,
  window or tab via `getDisplayMedia`.
  - Tab/system sound and the microphone are mixed through Web Audio, because a
    recorder takes a single audio track.
  - A 3-second countdown, the take's length in the tab title, and it stops
    cleanly when the browser's own "Stop sharing" is pressed.
  - WebM can be converted to MP4 (H.264 + AAC).
  - The camera bubble is a picture-in-picture window rather than canvas
    compositing. A background tab throttles `requestAnimationFrame`, and the
    tab being recorded is rarely the one in front.

Bugs caught by actually using them:

- The whiteboard never painted in development. React's StrictMode cancelled
  the animation frame but the code kept its id, so every later "schedule a
  redraw" thought one was already pending.
- MediaRecorder's WebM has no duration in its header, so the player showed
  `Infinity` and couldn't seek. Seeking past the end once makes the browser
  scan the file and learn its length.

**Lesson:** headless Chrome's fake devices (`--use-fake-device-for-media-stream`,
`--auto-accept-this-tab-capture`) made recorders testable end to end. A
3 s + pause + 2 s take came out at 5 s, and ffprobe confirmed every export's
codec. What a fake device can't tell me is whether a real microphone sounds
right.

**Next:** try the camera bubble, system audio and a real microphone on real
hardware; so far only fake devices have run through them.
