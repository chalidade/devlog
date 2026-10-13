# Kita Berkembang: A WordPress Multisite Store Builder for UMKM in One Day

[kitaberkembang.com](https://kitaberkembang.com) lets a small Indonesian business
(UMKM) open its own store at `namatoko.kitaberkembang.com`, take orders that land
in WhatsApp, and run everything from a phone. It went from an empty repo to
production in four merged PRs on the same day (about 13,400 lines). Claude Code
wrote most of the code and tests; I set the product scope, the order of features
and the security rules, and checked every build before it was deployed.

- One WordPress Multisite in subdomain mode with a custom plugin, so each store is
  a site with its own tables. Store owners get a phone-first dashboard with only
  their own menus; the rest of wp-admin is blocked
- **Prices, shipping, discounts and the total are computed only on the server.**
  The browser asks a quote endpoint for a preview, but the order endpoint
  re-prices every line, takes stock with an atomic decrement, and claims a
  voucher with an atomic `used + 1`, so the total in the WhatsApp message is final
- Checkout covers shipping per zone or per km from the store's location, a
  service fee, vouchers, opening hours (a closed store cannot take orders) and a
  status page that buyers open with a random key or with the order code plus the
  last digits of their phone number
- New orders are sent to the owner through Telegram or a WhatsApp gateway after
  the response has gone out, so a slow API never slows down the buyer
- Hardening that suits a multi-tenant site: login lockout per IP, XML-RPC and
  username enumeration closed, image-only uploads for owners, no PHP execution
  in uploads, security headers, and quoting user input in CSV exports
- Installable as a PWA, a store landing page with scroll motion, and a main
  marketing page whose template and copy the super admin edits without code.
  CI runs 67 PHPUnit tests and 22 Playwright tests in Docker; merging to `main`
  deploys the plugin over FTP
- A last pass for phones after testing on my own: one-line header, compact
  feature cards, swipeable store and testimonial rows, and a floating sign-up
  button that only appears once the hero buttons scroll away. The page got 17%
  shorter and no longer scrolls sideways at 360px, even with 125% system text

**Lesson:** for a store builder, the WhatsApp message is the receipt. Treating
anything the browser sends as a suggestion, and recomputing the total on the
server, mattered more than any feature on the list.

**Next:** turn the main page into a map of the stores that are open right now, so
buyers have a reason to visit it, not only sellers.
