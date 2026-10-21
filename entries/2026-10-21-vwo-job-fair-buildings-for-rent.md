# VWO Job Fair: Renting Out Whole Buildings, Two Gateways, Gift Cards

[jobfair.co.id](https://jobfair.co.id) went from one job fair to a platform that
can host several. Eleven pull requests merged today; Claude Code wrote the code
and tests, and I made the product calls and checked each deploy on the live site.

- **A "building" is a whole fair another organiser can rent.** It has its own
  hall, organisers, pre-registration and short link (`jobfair.co.id/<name>`),
  and moves through draft, live and ended. Shared places (park, library, food court) and
  the coin wallet stay global, so a visitor keeps one account across buildings
- I chose to add a building column to the tables that hold event data instead
  of new tables per tenant. The main fair is just the building called `main`,
  so a default value covered every existing row and nothing had to be rewritten
- Organisers can pick Midtrans or Xendit for coin sales. A checkout opened on
  the old gateway is closed out cleanly, and a late payment on it still credits
  once
- Gift cards: organisers create coin codes with a quota or unlimited, and each
  job seeker or company account can redeem a code once
- SEO basics (titles, sitemap, share image, event structured data), a tidier
  company portal on phones, and released stands can now be put back
- The repo went private, so CI now runs once per pull request and skips
  docs-only changes instead of running again on every merge

**Lesson:** multi-tenancy is cheapest when the first tenant already is one.
Treating the original fair as building `main` turned a rewrite into a column
and a filter.

**Next:** stands, company sign-ups and booth payments per building, so a tenant
can sell its own stands.
