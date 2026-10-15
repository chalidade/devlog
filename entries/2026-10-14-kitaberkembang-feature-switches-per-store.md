# Kita Berkembang: Feature Switches per Store, Enforced on the Server

On [Kita Berkembang](https://kitaberkembang.com) the super admin now decides which
features each store has, store owners can design their own landing page, and the
admin pages no longer look like WordPress. Five merged PRs (#11 to #15, about
1,600 lines) ending at version 0.9.0. Claude Code wrote the code and tests from
my requirements; I tested the live site and reported what broke.

- A feature registry with one switch per feature per store (landing page, free
  design, map listing, vouchers, ratings, statistics, AI), plus defaults for new
  stores. A rule in the README says every new feature must be registered there
- **A switch turned off is checked at every entrance, not just hidden from the
  menu.** With vouchers off, an existing code fails at checkout; with the map
  listing off, the store drops out of the map cache; the REST handlers refuse too
- Free landing design per store: colors, fonts, button shape, hero layout and the
  order of sections. The super admin uploads templates as small JSON files and
  assigns them to stores. I chose this over uploading WordPress themes, because a
  theme is PHP that would run across the whole network; every JSON value is
  checked against a fixed list
- The super admin pages now use the same app shell as the store dashboard:
  sidebar on desktop, tabs on a phone, store tables become cards, and a link opens
  any store's dashboard and comes back
- Two fixes from using it myself: visits from the map and from the super admin
  were not counted, and Groq removed the default AI model, so the plugin now asks
  the provider for an available model and retries once
- CI runs 94 PHPUnit tests and 31 Playwright tests in Docker before each deploy

**Lesson:** a feature flag that only hides a menu is a suggestion. If a feature
can be paid for later, the check has to live where the action happens.

**Next:** group the switches into plans, so changing a store's plan sets its
features in one step.
