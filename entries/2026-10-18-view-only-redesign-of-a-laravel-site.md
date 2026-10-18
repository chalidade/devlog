# A View-Only Redesign of a Laravel 8 Site

The same course site got a new design from the public pages through to both
dashboards. The rule was "change the views, not the backend", so every price,
discount and date rule stays in the code path it was in before.

- **Public pages** (home, class list, class detail, profile, contact): flat
  amber and near-black on warm paper, Archivo with its width axis at 125 for
  headlines, thin rules instead of shadows. The class posters are the main
  visuals. Motion is [Motion One](https://motion.dev) reveals that switch off
  under `prefers-reduced-motion`.
- My first pass was the stock "AI landing page" (centred hero, glow blobs, pill
  labels, icon-in-a-box cards). I threw it away and took the style from the
  site's own class posters instead.
- **Login, register, reset**: a split layout with the same fields and messages.
  It also keeps the email after a failed login and has a show/hide password
  button.
- **AdminLTE dashboards**: one theme stylesheet restyles the sidebar, tables,
  forms and buttons without touching the ~30 pages' markup. It even overrides
  buttons coloured with inline `style="background-color: rgb(…)"`. The admin
  home showed the template's fake numbers ("53% Bounce Rate"). It now shows
  real counts from the database.
- **CKEditor 4.18** started showing an "is not secure" banner. Version 4 is
  end-of-life (the fixed 4.25 needs a paid licence), so the admin forms now use
  Summernote, which was already bundled. Saved HTML is unchanged.
- **A bug that had been resetting data:** the class edit form's date picker was
  hard-coded to `01/01/2020 – 17/01/2020`, so every edit silently overwrote the
  class date. It now starts from the saved value.
- The class list printed every row into a `<script>`, including customers'
  discount emails. It now renders the cards server-side and reveals them six at
  a time.

I checked all of this on a local copy against SQLite: 36 admin, student and
auth pages, before and after. How I proved that no form changed is in
[proving a redesign changed no forms](https://github.com/chalidade/devlog/blob/main/notes/proving-a-redesign-changed-no-forms.md).

**Lesson:** "view-only" isn't automatically safe. That date picker was view
code that had been corrupting data for years. Read the JavaScript as carefully
as the controllers.
