# VWO Job Fair: Advertisers, Video Ads, and Coins for Watching to the End

[jobfair.co.id](https://jobfair.co.id) is my virtual job fair. Today it got a
second paying customer besides companies: advertisers (PRs #121–#123). Claude
Code wrote the code, tests and screenshots; I specified the flow, from the
application form to who approves what and how ads are paid for in coins.

- Advertisers apply through a public form with Google sign-in. An organiser
  approves them, and only then do they get their own portal: top up coins,
  create banner or video campaigns with a total and daily budget, and see
  30-day stats. Every new or edited ad goes through review before it runs
- Prices live in the existing price table and are editable: 25 coins per
  1,000 banner impressions and 50 coins per 100 completed video views to
  start. Charges are kept in thousandths of a coin so a single view never
  rounds past the budget
- **Watching an ad to the end earns a seeker one coin, and the server decides
  what "the end" means.** It issues a view token when the video starts and
  pays only after the video's length has passed on its own clock, once per
  token, at most 10 paid videos a day, and the same campaign pays a person
  once in 24 hours
- The advertiser's charge and the viewer's reward are booked in one database
  transaction, each with an idempotency key in the coin ledger, so a retry can
  never pay twice
- Organisers can now set a sign-up bonus and give free top-ups to seekers or
  companies, each with a required reason, a cap, and an audit log

**Lesson:** any reward that depends on the client saying "done" will be farmed.
The server's clock is the only stopwatch worth trusting.

**Next:** a rehearsal with real visitors on phones and laptops before the first
public event.
