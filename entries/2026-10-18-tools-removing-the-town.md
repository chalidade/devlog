# Tools: Removing the Town

Eleven days ago the [tools site](https://chalidade.github.io/tools/) got a walkable
RPG town as its home page. Today I took it out again and replaced it with a short
static intro, the search and the tool cards.

- Deleted the playground (the town, its buildings, residents, dialog system and
  sprites, about 3,800 lines) and all its CSS animation
- Dropped the `motion` library too; the cards now simply appear
- **Main JS went from 518 kB to 278 kB, CSS from 95 kB to 65 kB**
- Earlier the same day the README became English (pitch, privacy promise, every
  tool by category, stack, quality gates, embedding), with the Indonesian version
  kept as `README.id.md` and a new `docs/ARCHITECTURE.md`. Both were updated again
  after the town went

**Lesson:** the town was fun to build, but every visitor paid about 240 kB of
JavaScript for it, including the ones who only came to merge two PDFs. A home
page for a toolbox should get out of the way.

The old write-up is still worth reading for the technique:
[A Walkable Home Page in Plain DOM](https://github.com/chalidade/devlog/blob/main/notes/walkable-home-page-in-plain-dom.md).
