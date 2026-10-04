# Time-Stretching Audio in the Browser

Speeding up a recording by just resampling it turns voices into chipmunks. For the
speed tool on my [tools site](https://chalidade.github.io/tools/#/change-speed) I
needed 0.25×–4× with the pitch unchanged, offline and in the browser, and on files
too long to decode into memory at once.

## The approach
WSOLA (waveform-similarity overlap-add), streamed chunk by chunk:

- Output is built from Hann-windowed frames of about 50 ms at a fixed hop of half a
  frame. With 50% overlap the windows sum to one, so the volume stays flat.
- Frame *k* is read from the input near `k × hop × speed`, which is what changes the
  duration. The pitch stays put because each frame is a copy of real input, never
  resampled.
- Before taking a frame, slide its start up to ±10 ms to the spot whose waveform best
  continues the previous frame (normalized cross-correlation). This is the step that
  removes the phasing and clicks of plain overlap-add.
- After each output hop, drop input that no future frame can reach, so memory stays
  bounded no matter how long the file is.

The audio comes from Mediabunny's conversion `process` hook. The hook receives decoded
chunks and returns new samples whose timestamps are written back to back.

## Gotchas
- **Matching cost.** A full search at every sample is too slow. Comparing every 4th
  sample and stepping candidates by 4, then refining ±3 around the winner, brought 60 s
  of stereo down to about 1.6 s in Node.
- **The end of the file.** The last half-frame sits in the overlap buffer. Flush it
  when the chunk that reaches the track's end arrives, or the output loses its tail.
- **Video alongside.** When the audio is stretched, the video has to be re-timed with
  it. Dividing timestamps by the speed is not enough: when sped up, keep one frame per
  `1/fps` slot. Round to the nearest slot, because WebM stores whole milliseconds, and
  a strict "next frame at t + 1/fps" check dropped a third of the frames.

## When to use it
WSOLA suits speech and most music at moderate factors. It is how I checked it: a
440 Hz tone stayed at 440 Hz from 0.5× to 4×, at the same RMS, with no sample jumps.
Past about 2× on dense music, a phase vocoder sounds smoother. When pitch is *meant*
to change (the "tape" effect), a plain resampler is simpler and correct.
