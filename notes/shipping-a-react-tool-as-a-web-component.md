# Shipping a React Tool as a Web Component

The screen recorder on my [tools site](https://chalidade.github.io/tools/#/screen-recorder)
is a React + Tailwind v4 component. To let other sites use it, I package it as a
custom element, `<screen-recorder>`, that works on any page: plain HTML,
WordPress, Vue, or React. Code:
[`packages/screen-recorder`](https://github.com/chalidade/tools/tree/main/packages/screen-recorder).

## One source, two builds
The package doesn't copy the tool. Its Vite config aliases `@` to the site's
`src/`, so the site and the package compile the same files. A library build
with two entries produces:

- `element.js`: React, the component and its CSS, all bundled. One
  `<script type="module">` from jsDelivr is all a page needs, because jsDelivr
  serves every npm package for free.
- `index.js`: the headless API with no React.

Heavy parts like Mediabunny stay dynamic imports. They become separate chunks
that load from the package's own URL, and only when someone converts to MP4.

## Shadow DOM, and what breaks in it
The element renders React into a shadow root, so the host page's CSS can't
reach in and Tailwind's preflight can't leak out. Three things needed fixing.

- **Design tokens.** The site defines colours on `:root`, which doesn't exist
  inside a shadow root. The tokens now live in `src/theme.css` under
  `:root, :host`, so one file serves both.
- **`@property`.** Tailwind v4 registers its internal variables (translate,
  shadow, ring…) with `@property`. Browsers honour those registrations at
  document level, not inside a shadow root. The element moves the `@property`
  rules out of its CSS string into one `<style>` in the page `<head>`. They're
  global and harmless. The toggle knobs' `translate-x-4` resolving to 16px
  confirmed it worked.
- **Dark mode.** The site toggles `.dark` on `<html>`, but the host page has
  its own `<html>`. The element puts `.dark` on its inner wrapper instead,
  driven by a `theme="auto|light|dark"` attribute and `prefers-color-scheme`.

## Letting the host restyle it
Custom properties do cross the shadow boundary through inheritance, but the
dark theme re-declares the brand colours on the inner wrapper, which beat
anything set on the host. So the element exposes its own hooks: the wrapper
reads `var(--sr-brand-1, <default>)` in both themes. A page can then set
`screen-recorder { --sr-brand-1: … }` and it holds in light and dark. I tested
it in both before documenting it.

## Gotchas
- **Re-attach.** Frameworks move nodes around. `connectedCallback` runs again,
  and a second `attachShadow` throws. Reuse `this.shadowRoot`.
- **Hand-written types drift.** The public `.d.ts` is written by hand for
  readability, so `types/check.ts` asserts it's mutually assignable with the
  source's types, and the package build type-checks it.
- **Props, not assumptions.** The site's component changed the tab title and
  always saved to IndexedDB. In someone else's page those are rude defaults, so
  they became props (`showInTitle`, `persist`), and the element maps them to
  attributes. Finished recordings are announced with a composed `recording`
  event that carries the file.

## The cheaper alternative
Every tool also works in an iframe (`#/<tool>?embed`), which costs almost
nothing to build. It runs from my origin, so the visitor's storage is
partitioned per site, and screen capture needs `allow="display-capture"`. The
web component is worth it when the host wants the file itself, wants to match
its own colours, or doesn't want to depend on my hosting.
