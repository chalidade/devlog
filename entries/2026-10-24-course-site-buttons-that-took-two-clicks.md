# Course Site: Buttons That Took Two Clicks

Two small rounds on the Laravel course site from
[last week's redesign](https://github.com/chalidade/devlog/blob/main/entries/2026-10-18-view-only-redesign-of-a-laravel-site.md).

- **A PHP mitigation (23 October).** A `.user.ini` that sets
  `session.upload_progress.enabled = 0`, the stop-gap for the PHP2Shell CVE
  published this month. The comment in the file says to remove it once PHP on
  the host is patched.
- **Buttons on My Course needed two clicks.** The dashboard loads
  `mdb.min.js` but never shipped `mdb.min.css`. On press, the script adds a
  ripple `<span>` inside every `.btn`. With no styles, that span took up space
  and widened the button while the mouse was still down, so the release landed
  on a different element and the click never fired. Three CSS rules in
  `dashboard.css` give the ripple `position: absolute` and
  `pointer-events: none`, and the stylesheet version went from `?v=7` to
  `?v=8` so browsers fetch it.
- **Adding a tutor failed when the description was empty.** An empty editor
  posts `null`, and the column is `NOT NULL`. Store and update now save `''`.
  The create form also shows validation errors now, so a rejected form says why.
- The same form loaded every province, regency, district and village row from
  the database and never used any of them. It doesn't load them anymore.

**Lesson:** half a UI library is worse than none. The script without its
stylesheet broke the most basic thing a button does, and the page looked fine
until you clicked.
