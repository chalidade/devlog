# Tools: Password Generator, Word Counter, and a GIF Back on the README

Day 4 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
(PR #8) was text and security: two tools in the productivity category, bringing the
[site](https://chalidade.github.io/tools/) to 52.

- **Password generator:** random passwords of 4–64 characters, or passphrases of
  3–10 words from an Indonesian or English word list. Every pick goes through
  `crypto.getRandomValues` with rejection sampling, so there is no modulo bias, and
  the result is guaranteed one character of each chosen kind before a Fisher–Yates
  shuffle. An option drops look-alikes (`l I O 0 1`)
- **Strength meter:** entropy in bits and an average time to guess at 10 billion
  guesses a second. A "check my password" mode estimates a typed password with
  penalties for repeats, runs like `abcd` or `4321`, and common words, including
  Indonesian ones like `rahasia` and `bismillah`. Nothing typed is sent or stored
- **Word counter:** words, characters with and without spaces, sentences,
  paragraphs, lines, and reading (230 wpm) and speaking (130 wpm) time. Characters
  are counted as graphemes with `Intl.Segmenter`, so an emoji counts as one, and
  `kupu-kupu` or `don't` count as one word
- **Platform limits:** live bars for X, Instagram caption and bio, TikTok,
  WhatsApp status, LinkedIn, SMS, and SEO title and meta description (those two
  are marked as advice, not a hard cut-off)

**README:** yesterday the launch film became a real GitHub video player. Today I
put an animated GIF back at the top instead (480 px, 12 fps, about 4.7 MB per
language, rendered from the MP4 with an ffmpeg palette pass). The GIF links to the
video, with a "watch with sound" link underneath. A first render at 640 px came
out at 10 MB, too heavy for a page people only skim.

**Lesson:** a README visitor gives the top of the page a few seconds. A GIF that
plays on its own uses those seconds, while a player needs a click first. Sound
is for people who choose it, so a link is enough.
