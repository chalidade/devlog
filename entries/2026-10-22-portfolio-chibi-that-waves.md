# Portfolio: A Chibi That Waves Back

The hero of [my portfolio](https://chalidade.github.io/) now has a small chibi of
me. It stands still, waves when you hover, and introduces itself when you click
or tap.

- The animation started as a generated 720×1280 video on a white background. A
  small Python script (`matte.py`) removes the background with a flood fill from
  the edges, so the white shirt in the middle survives
- The frames were composited onto pure green and compiled with the oil-motion
  skill into one 212-frame timeline at 24 fps, with three still poses: `rest`
  (frame 0), `waved` (92) and `introduced` (211)
- In the browser a WebGL shader keys out the green, and a segment player plays
  only the part between two poses. Since every state is a still pose, the player
  can jump back to `rest` or `waved` to replay without a visible cut
- Separate desktop (480 px) and mobile (360 px) videos. It greets once when the
  hero first scrolls into view and pauses when the tab is hidden
- With `prefers-reduced-motion`, no WebGL, or a failed video, you get a still
  transparent poster instead, and the green master never shows
- Sources, the timeline and the rebuild steps live in `_motion/`, which Jekyll
  doesn't publish

**Lesson:** a WebGL green-screen effect can fail in several ways (no WebGL,
reduced motion, a video that won't load), and each one has to land on the still
poster. The visitor should only ever see the chibi or its picture.
