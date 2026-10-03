# A Devlog Page That Reads This Repo

Added a [Log](https://chalidade.github.io/log/) page to my portfolio that renders
this repository directly — publishing is just pushing a `.md` file here.

- File list from the GitHub tree API, falling back to jsDelivr's package listing
  when the 60-requests/hour anonymous limit runs out; cached per tab for 10 minutes
- `entries/**/YYYY-MM-DD-slug.md` becomes a timeline (newest first), `notes/**/*.md`
  becomes cards; the first `# heading` is the title
- Markdown rendered with marked and sanitized with DOMPurify, in a static page with
  no build step
- Same day on the portfolio: a **Builds** section driven by a small `builds.js`
  list, weeknoo replacing RuangKelasku in Selected Work, and the tools repo listed

**Lesson:** the lowest-friction publishing flow wins. If logging means editing two
repos, I won't do it; if it's one file, I will.

**Next:** automate it — a Claude Code skill that reads a day's commits and drafts
these entries.
