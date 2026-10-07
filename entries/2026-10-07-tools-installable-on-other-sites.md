# Tools: Installable on Other Websites

I wanted anyone to be able to take one tool from my
[tools site](https://chalidade.github.io/tools/), say just the screen
recorder, and put it on their own website. Today it became possible, with one
step still blocked on my side.

- **The repo is now MIT-licensed.** Without a license, a public repo still
  can't legally be reused. The bundled dependencies are MIT, Apache-2.0, ISC
  and MPL-2.0 (Mediabunny), and the package ships a notice file for them.
- **Every tool can be embedded with an iframe** today: `#/<tool>?embed`
  renders the tool alone, with an optional `&theme=light|dark`. Each tool page
  now has a "Pasang di situsmu" card with the snippet. I recorded a screen from
  inside a cross-origin iframe to check that `allow="display-capture"` is
  really enough.
- **[`@chalidade/screen-recorder`](https://github.com/chalidade/tools/tree/main/packages/screen-recorder)**,
  the first package:
  - A `<screen-recorder>` custom element, one `<script type="module">` and
    99 KB gzipped with React inside.
  - A headless API for people with their own UI: `recordScreen()`,
    `capture.stop()`, `toMp4()`, about 3 KB gzipped.
  - It builds the site's own source rather than a copy. To get there, the
    recording logic moved out of the React component into a small controller
    that both the site and the package use.
- I tested it on a deliberately hostile page (pink `!important` buttons, serif
  fonts). The element looked right, recorded, and handed the file to the page
  through a `recording` event.

What didn't happen: the npm publish.

- npm now requires two-factor authentication to publish.
- The OTP prompt can't appear in the non-interactive shell I was running it
  from, and two six-digit codes were rejected.
- After the failed attempts in a row, GitHub put my network behind "Access
  temporarily restricted".
- The package is built and verified with `npm pack`. It goes out once the
  block lifts, from a normal terminal, in one calm attempt.

**Lesson:** publishing is an account action, not a build step. Repeated
failures on a login or OTP prompt look like an attack, and the platform
responds like it is one. Slow down after the first rejection instead of
retrying.

**Next:** publish the package, switch the card to show the script tag, and add
`lang="en"`, since the UI is Indonesian-only and npm's audience isn't.

How the packaging works: [Shipping a React Tool as a Web Component](https://github.com/chalidade/devlog/blob/main/notes/shipping-a-react-tool-as-a-web-component.md).
