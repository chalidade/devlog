# fet: A Front-End Roadmap That Asks If You Understood

New repo: [fet](https://github.com/chalidade/fet) (Front-End Toolkits), with
docs at [chalidade.github.io/fet](https://chalidade.github.io/fet/). It's a
front-end roadmap where each stage covers why the topic matters, how to learn
it, questions that check whether you understood it, and something to rebuild
from scratch. Everything went in as pull requests over one day, with Claude Code
writing most of it.

- **The roadmap:** 20 stages in 8 phases, adapted from
  [roadmap.sh/frontend](https://roadmap.sh/frontend), from how the internet
  works to mobile and desktop. Each stage has a concept map, a way to study it,
  understanding checks, a practice project and primary sources, plus a page on
  the learning method and a template for new stages
- **Deep dives** that go further than the roadmap: the event loop, the browser
  rendering pipeline, the CSS cascade and specificity, and HTTP caching
- **A VitePress site in two languages.** Indonesian is the default and the full
  English translation lives under `/en/`. It has local search, mermaid diagrams,
  a sidebar per phase, and a GitHub Pages deploy that CI also builds
- **A landing page I redesigned the same day.** The default VitePress hero and
  emoji feature cards are gone. The new page has a left-aligned headline, one
  primary action, a preview of the learning room, the three-step method and all
  eight phases. The phases moved into `stages.ts` so the config and the home
  page read the same list
- **The toolkit**, a pnpm monorepo with tsup, vitest and changesets:
  - `@chalidade/utils`: `debounce`, `throttle`, `cx`, `clamp`
  - `@chalidade/tokens`: primitive and semantic (light/dark) design tokens,
    with helpers and a generated `tokens.css`
  - `@chalidade/react-hooks`: SSR-safe hooks (debounced value and callback,
    media query, `localStorage` synced across components and tabs, click
    outside, intersection observer and a few more) with jsdom tests
- A small CI fix along the way: the root scripts passed the package filter
  unquoted, which was fine with one package. With a second package, the shell
  expanded the glob before pnpm ever saw it.

**Lesson:** a roadmap that only lists topics is easy to agree with and easy to
fake progress on. The understanding checks are the part that tells you which
stage you only think you know.

**Next:** the packages aren't on npm yet. Publish them through changesets.
