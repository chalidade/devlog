# Vigenco: Spec In, MP4 Out

[Vigenco](https://github.com/chalidade/vigenco) is a video generator I built over
two days: write a JSON spec, run GitHub Actions, get a 60 fps vertical MP4 with
music and sound effects. Every frame is HTML computed from time (`seek(t)`); there
is no video model and no editor. Claude Code wrote the code; the technique is
adapted from the MIT-licensed product-launch-motion project, credited in `NOTICE`.

- **The renderer.** Playwright captures several subframes per frame, ffmpeg's
  `tmix` blends them into real motion blur, and the result is encoded as H.264.
  A small Python synth writes an original 120 BPM bed and puts sound effects on
  the cue peaks. Standard quality uses JPEG subframes, and the README records measured render times
- **A page that turns a prompt into a video.** [The page](https://chalidade.github.io/vigenco/)
  takes a prompt, a format (portrait, landscape, square), attachments and links,
  commits the request to the repo and starts a workflow. Claude Code directs: a
  quick mode fills the `launch` template in 6 to 12 minutes, and a full mode writes a
  bespoke HTML film per request in 20 to 40 minutes. The finished MP4 is published as a
  GitHub Release and plays in a gallery
- **Silent videos.** One film's cue index produced a pan value outside [-1, 1],
  which turned the whole mix into NaN and encoded as silence. The pan is clamped
  now, the renderer refuses to publish silent audio, and each gallery video has
  "fix the sound" and "re-render" buttons that reuse the saved film without calling
  Claude again
- **A second type, `story`:** narrated, illustrated animation in Remotion, with SVG
  scenes, Edge TTS or ElevenLabs narration with word timings, and karaoke captions.
  Stories can now run 2, 3 or 5 minutes, written in three acts
- The page found its workflow run by comparing timestamps on the phone's clock,
  so a phone running fast never matched. It now matches by the run title, which
  carries the unique request id

**Lesson:** a mix with one NaN sample is silent everywhere. Check the output
(here: is the audio silent?) before publishing, since the error won't surface
on its own.
