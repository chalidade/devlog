# Front-End Training: Proof of Learning, and a Theme Other Repos Can Use

The second day on [fet](https://github.com/chalidade/front-end-training), which
was renamed to **Front-End Training** by evening. The site moved to
[chalidade.github.io/front-end-training](https://chalidade.github.io/front-end-training/).

- **A deep dive on efficiency in React** (Indonesian and English): debounce
  inside a component, throttle, `memo`/`useMemo`/`useCallback`,
  `useTransition`/`useDeferredValue`, and virtualisation. It's linked from
  stages 04, 07 and 16
- **Two new hooks** in `@chalidade/react-hooks`: `useThrottledCallback` and
  `useOnline`, with tests and a changeset
- **Bukti Belajar (proof of learning)**, at `/bukti-belajar` and
  `/en/evidence`: per stage, the concepts ticked, the work published, and (for
  the owner only) notes and code. It works in local mode too, and it prints
  cleanly to PDF. A migration makes ticked concepts public while notes and code
  stay private
- **The learning site became a package**, `@chalidade/learn-theme`. The learning
  room, community, profile, Bukti Belajar, stage banner and checklist plugin
  moved into it, so another learning repo (back-end, for example) can use the
  same theme and the same Supabase project. The site now calls
  `createLearnTheme({ stages, phases, concepts, siteName, subject })`. Text that
  named the site or the subject comes from that config, and stage slugs can
  carry a prefix like `be-01-http`, with a migration to allow them in the
  database
- **A 33-second launch video** (1080p60) in the README, with its poster, served
  from `docs/public` so it deploys with the site
- **The rename broke the site.** GitHub Pages moved to `/front-end-training/`,
  and the VitePress `base`, the icons and every repo and site link still
  pointed at `/fet/`. They were fixed the next day (PR #14)

**Lesson:** a rename is a breaking change for anything served under the repo's
name. The site's base path, icons and links all depended on the old name, and
nothing flagged it until the deployed site broke.
