# Tools: Encode/Decode, UUID Generator and Text Diff

Day 6 of the [tools roadmap](https://github.com/chalidade/tools/blob/main/ROADMAP.md)
was for developers: three tools in the developer category, 57 in total.

- **Encode / Decode:** Base64 for text (UTF-8, with a URL-safe option), URL
  encoding for a component or a whole URL, HTML entities, and a JWT reader that
  shows the header, the payload and `iat`/`nbf`/`exp` as dates with an
  expired/valid status. It says plainly that the signature is not verified, and
  the token is never sent anywhere
- **UUID generator:** v4 (random) and v7 (time-ordered), 1 to 1,000 at a time,
  uppercase, without dashes or in braces, all from `crypto.getRandomValues`
- **Text diff:** a line diff with word-level highlights on changed lines, a
  unified or side-by-side view, options to ignore case and whitespace, and a
  button to swap the two texts

**Lesson:** a JWT decoder that doesn't verify should say so on the screen.
Decoding looks like checking, and people paste production tokens into these
tools.
