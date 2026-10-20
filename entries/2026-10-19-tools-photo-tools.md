# Tools: Three Photo Tools for Everyday Paperwork

Day 2 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
(PR #5): three image tools, bringing the
[site](https://chalidade.github.io/tools/) to 48.

- **Convert image:** HEIC (iPhone photos), WebP, AVIF, PNG, JPG, GIF, BMP and SVG
  to JPG, PNG or WebP, in batches downloaded as a ZIP. HEIC is decoded by libheif
  compiled to wasm, bundled and self-hosted, and loaded only when a HEIC file
  shows up
- **Pas Foto (ID photo):** crop to 2×3, 3×4 or 4×6 with pan and zoom, swap the
  background to red, blue or white (detected from the top-edge colour, reusing the
  remove-background engine), then lay copies out on 4R or A4 at 300 dpi with cut
  lines
- **Strip photo metadata:** shows the EXIF (camera, lens, date, exposure, GPS) and
  saves a clean copy. JPG and PNG are cleaned without re-encoding the image; WebP
  and photos rotated by an orientation tag are re-encoded

**Lesson:** the tools people need for Indonesian paperwork (a 3×4 photo with a red
background, an iPhone photo a form won't accept) are small, but they are exactly
the files you shouldn't upload to a random converter.
