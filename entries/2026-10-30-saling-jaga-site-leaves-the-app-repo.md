# Saling Jaga: The Website Moves Out of the App Repo

The [Saling Jaga](https://saling-jaga.com) app repo went private, and that took
its GitHub Pages site and public APK download with it. The evening went into
giving the website a home of its own.

- **First stop: my profile site.** The site (Indonesian and `/en/`), the privacy
  policy and the v0.26.0 APK with its SHA-256 moved to `chalidade.github.io/saling-jaga/`,
  copied over by a `publish-site.sh` script in the app repo
- **Then its own domain.** The same evening it moved again, to a public
  [saling-jaga-site](https://github.com/chalidade/saling-jaga-site) repo on
  `saling-jaga.my.id`. The old `/saling-jaga/` pages became redirects that keep
  the `#hash` and are marked `noindex`; the APK and its checksum stayed so links
  already shared still download
- Released 0.27.0 the same day: a profile sheet of tiles, a one-row bottom bar
  and new screenshots
- Two syncs went out by hand because GitHub Actions was blocked by billing that night

**Lesson:** making a repo private turns off more than the code view. Pages and
release downloads go with it, so move them before you flip the switch.
