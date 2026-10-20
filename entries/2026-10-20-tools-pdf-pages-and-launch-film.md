# Tools: Organize PDF Pages, and a 16-Second Launch Film

Day 3 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
(PR #6) added two PDF tools, bringing the
[site](https://chalidade.github.io/tools/) to 50. Then I made its first launch video.

- **Organize PDF:** drag page thumbnails to reorder, rotate, duplicate or delete
  pages, with a reset. Previews come from pdf.js and the new file is built with
  pdf-lib
- **Page numbers:** six positions, four formats (`1`, `1 / 10`, `Halaman 1`,
  `- 1 -`), a start page so the cover can be skipped, and correct placement on
  rotated pages. The preview uses the same position maths as the export

**The launch film** (16 s, 1440×1440, loops) is now at the top of the
[README](https://github.com/chalidade/tools#readme): a contract gets dropped in,
is processed on the device with "0 B sent to server", is signed with the cursor,
compressed with a dragged slider, found by typing in the search, and then becomes
one tile in a wall of every tool.

- One element never cuts: the dropzone becomes the file card, the status card,
  the page, the slider, the search box and the tile, and at the end it returns to
  the dropzone, so the last frame matches the first
- The whole film is one HTML page where every frame is a pure function of time,
  built from closed-form springs, then rendered with Playwright at 4 subframes per
  frame and blended by ffmpeg into 60 fps motion blur
- The music is an original 120 BPM score synthesized with numpy (no samples, no
  licence question), and the UI sounds are placed on its beat grid. Its tail is
  folded onto its start so the audio loops too
- The tool names and icons come straight from the site's registry. The contract,
  its 4.2 MB size and the "−74%" are illustration, not a measured result
- In the README it is an animated WebP (GitHub always shows it) linking to the MP4
  with sound

**Lesson:** the film shows 45 tools, and by the time it was in the README the site
had 50. A real number in a video is accurate for a day, so the next cut should
count in a way that doesn't date, or be easy to re-render.
