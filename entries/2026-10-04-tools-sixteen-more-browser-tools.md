# Tools: 16 More, From PDF Signing to QR Codes

My [tools site](https://chalidade.github.io/tools/) went from 19 to 35 tools in one
day, across four merged PRs. Same rule as before: every file is processed on the
visitor's device. Claude Code wrote most of the code; I picked what to build, made
the scope calls below, and reviewed and merged every PR.

- **PDF:** merge, split (pages, ranges, every N pages), watermark, and sign — on
  pdf-lib, drawn in the page's *displayed* orientation so rotated pages come out right
- **Image:** crop & resize, favicon set (`.ico` + iOS/Android icons + manifest),
  image ⇄ Base64, a color picker with WCAG contrast, and background removal
  **without AI** — magic wand, color select, lasso and brush. I chose that over a
  100 MB model download, so nothing on the site leaves the device
- **Video/audio** on Mediabunny: trim, GIF ⇄ MP4, frame extraction, speed change
  that keeps the pitch (my own WSOLA — see
  [Time-Stretching Audio in the Browser](https://github.com/chalidade/devlog/blob/main/notes/time-stretching-audio-in-the-browser.md)),
  and audio merge across mixed formats
- **QR:** a generator that scans back every code it makes, and a reader for QR and
  barcodes. jsQR could not read dot-style codes at all, so the reader switched to
  zxing-wasm, with its wasm bundled instead of fetched from a CDN
- Fixed for everyone: pdf.js 6 needs JavaScript newer than many browsers ship, so
  every PDF tool failed on older Chromium. Now on pdf.js's legacy build
- Said no to a YouTube/Instagram downloader: it can't work without a backend proxy,
  and that breaks the site's one promise

**Lesson:** "it works in the browser" proves nothing; measure the file it produced.
Every tool here passed a click-through, yet ffprobe found a 2× video with 81 frames
instead of 120, and a GIF playing 4% fast. Neither shows up until you count.

**Next:** test the H.264/AAC path in a real Chrome — the test browser had neither,
so only the VP9 and wasm-AAC fallbacks are verified.
