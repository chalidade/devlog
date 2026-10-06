# Tools: The Home Page Becomes a Walkable Town

The [tools site](https://chalidade.github.io/tools/) used to open with a hero and a
card grid. Now it opens with a small top-down town you walk with the keyboard: each
category is a building, and inside, each of the 33 tools is a person who explains
what it does and offers to open it. Claude Code wrote the code; I drove the design
over four rounds of "this isn't it yet" and reviewed every step in a real browser.

- **Round 1:** a robot walking between tool stalls, WASD/arrows, Shift to run, E to
  open. It worked, but it was still a grid of cards with a robot on it
- **Round 2:** every tool became a talking character with an RPG dialog box:
  typewriter text, three pages on what the tool does and its limits, then
  *Buka* / *Nanti saja*. I called the file-shaped characters cringe
- **Round 3:** cartoon people instead, one house per category, with doors you walk
  into and a fade between scenes. Still too static
- **Round 4:** a building style per category (print shop, library, vault, studio,
  lab), keepers in matching uniforms, winding paths, a pond, tall grass that rustles
  and hides your feet, benches, lamps that light up in dark mode, and residents with
  routines: an old man by the bench, a kid running around, a woman walking her dog,
  two friends chatting in turns
- All original SVG/CSS art, no Pokémon assets. The layout is built from the tool
  registry, so the 16 tools merged a few days ago got their own keepers with no
  layout work. They only needed dialog lines
- Tagline changed from "convert files, no upload" to "Semua tools, langsung di
  browser.": the site is no longer only converters
- The plain searchable grid stays below the map. The map is `aria-hidden`, so a
  screen reader skips straight to the grid

Bugs that only showed up by actually playing it:

- Visited stamps never saved. The write sat inside a React state updater, and
  opening a tool unmounted the page before the updater ran
- Click-to-walk went in a straight line and stuck on the first tree. Replaced with
  A* on a 20 px grid
- On phones, tapping a character scrolled the map sideways and pushed the dialog
  off screen. `overflow: hidden` can still be scrolled by code; `overflow: clip`
  can't
- A talking resident seemed to stand on the lab's roof. I had raised a speaker's
  z-index so its bubble wouldn't hide behind trees, and that lifted the whole body
  over the building

**Lesson:** describing the look in words never got it right; screenshots did.
Every round only moved forward after I looked at the page and said what felt
wrong. Things like "cringe" or "static" never show up in a build log.

**Next:** watch whether people actually use the town or scroll past it to the
grid. If they scroll past, the map should get smaller, not fancier.

How it's built: [A Walkable Home Page in Plain DOM](https://github.com/chalidade/devlog/blob/main/notes/walkable-home-page-in-plain-dom.md).
