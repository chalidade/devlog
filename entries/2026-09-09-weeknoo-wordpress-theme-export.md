# weeknoo: Any Site Becomes a WordPress Block Theme

`npm run wp -- <site>` now turns a weeknoo site into a WordPress block theme
you can upload through Appearance → Themes → Add New. For clients who want to
edit their own text, this means I can still build in React.

- **The flow:** `npm run build` runs first (it's still the type-check gate and it
  produces the compiled Tailwind CSS). Then every section is prerendered on its
  own with `renderToStaticMarkup`, its HTML is converted to WordPress block
  markup, and the theme is zipped. The one-file-per-section rule is what keeps
  section boundaries intact all the way into the theme
- **`theme.json` comes from the `:root` tokens** in the site's `index.css`, so
  the site's palette and fonts show up in the WordPress editor from one source
- One block pattern per section; a `Nav`/`Navbar`/`Header` section becomes the
  header part and `Footer` the footer part. The index template composes them in
  the same order as `App.tsx`, plus page, single, archive, search and 404
- **Motion animations are replaced** with a scroll-driven CSS animation
  (`animation-timeline: view()`). With a JavaScript reveal, a browser that
  can't run it would hide the content forever; with this one it just shows it
- **Two traps shaped the code.** Tailwind v4 puts everything inside `@layer`
  and WordPress's core CSS has no layer, so core wins every time. And Tailwind
  only compiles classes the site uses, so the generated templates can't use
  utilities. Details in
  [Tailwind's layers vs WordPress's CSS](https://github.com/chalidade/devlog/blob/main/notes/tailwind-layers-vs-wordpress-css.md)
- Tested on a real WordPress 7.1 with the SQLite drop-in: two sites installed
  and activated, all patterns registered, every template rendered with no PHP
  errors, and a full-page pixel comparison against the React version came out
  identical
- **WORDPRESS.md and INSTALL.md**, both in Indonesian. The local-WordPress test
  recipe was run verbatim from an empty folder before it went in

**Lesson:** check an export against the original with pixels. The page looked
fine by eye, and only the diff against the React version showed the 16 px that
core CSS added.
