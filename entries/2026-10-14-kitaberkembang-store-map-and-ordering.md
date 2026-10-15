# Kita Berkembang: A Map of Open Stores You Can Order From

[kitaberkembang.com/map](https://kitaberkembang.com/map/) now shows every store
that is open right now, and a buyer can order without leaving the map. Six merged
PRs (#5 to #10, about 4,800 lines). Claude Code wrote the code and tests from my
requirements; I tested every release on the live site with my own phone.

- A Leaflet map with an "open now" filter, named pins, swipeable store cards and a
  detail panel with logo, address, route and menu. Owners set their category,
  address and pin from their own settings, with search, "my location" or a tap
- **Ordering happens inside the map panel.** Tapping a menu item opens the store's
  order page in the panel, so quantity, buyer details, payment and the WhatsApp
  message all happen without a page change. Product pop-ups show buyer ratings
- Store owners got an onboarding guide, visitor statistics, a digital receipt,
  buyer ratings and AI help that drafts product descriptions and promo captions
- Two free providers changed under me in one day. The CARTO map tiles started
  returning "API KEY REQUIRED", so the map moved to OpenStreetMap and the tile
  provider became a filter. New Gemini keys were rejected by the OpenAI-compatible
  endpoint, so Gemini now uses its native API, and the super admin can test a key
  and read the provider's last error message

**Lesson:** every free API is a dependency that can break on someone else's
schedule. Make the provider a setting, and show its real error to the admin, so
the next outage is a five-minute fix instead of a debugging session.

**Next:** let the super admin choose which features each store gets.
