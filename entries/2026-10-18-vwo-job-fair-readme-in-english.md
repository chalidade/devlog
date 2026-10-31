# VWO Job Fair: A README Written for a Stranger

The [vwo](https://jobfair.co.id) repo behind
[jobfair.co.id](https://jobfair.co.id) got an English README (PR #120,
documentation only). Claude Code drafted it from the code and the numbers
already published in this devlog.

- Opens with what the product is and links to both the live site and the
  GitHub Pages demo, with a screenshot of a booth floor, before any setup steps
- Features grouped by who uses them: job seekers, companies and organisers
- Two mermaid diagrams: how a visitor's browser, the API, Postgres and realtime
  talk to each other, and how the workspace packages depend on each other
- **Every performance number says how it was measured** (unit test, local
  benchmark or simulation), so nothing reads like a production metric
- The old Indonesian README stays as `README.id.md`

**Lesson:** a number without its method is a claim. Saying "local benchmark"
or "simulated" next to a figure costs a few words and keeps the README honest
when someone checks.

**Next:** a rehearsal with real visitors on phones and laptops before the first
public event.
