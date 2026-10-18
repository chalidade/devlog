# Proving a Redesign Changed No Forms

When you rewrite the markup of a server-rendered app, the risk isn't how it
looks. It's a form that now posts somewhere else, or drops a field the
controller expects. On a Laravel 8 redesign (36 admin, student and auth pages)
I checked for that mechanically instead of by clicking around.

## A signature per page
A tiny Python `HTMLParser` reduces each page to the parts that talk to the
server:

- every `<form>`: method, action (query string stripped) and enctype
- every named `input`, `select`, `textarea` and `button`, by name and type
  (`_token` skipped)
- every link back to the app's own host

The lines are sorted and de-duplicated, so layout and ordering changes don't
count, only what gets submitted or requested.

## Before and after
1. Run the app locally (SQLite, sample data, seeded accounts).
2. Log in with `curl` cookie jars, one per role, and save the signature of
   every page.
3. Redesign.
4. Fetch the same pages again and diff.

Field differences must be zero. Links may be *added* (a new Dashboard item)
but never removed, so the check counts `<` lines in the diff separately.

## What it caught, and what it can't
- It confirmed that a WYSIWYG editor swap kept `name="description"`, and that
  the one new field (a honeypot on register) was the only change.
- It does **not** prove JavaScript behaviour. A date picker that overwrote its
  input on load passed the diff, because the field name never changed. I found
  that bug only by saving a record and reading it back from the database. So
  pair the diff with at least one real save per form type.

## Gotchas
- An empty signature means the page errored or redirected. Count those
  explicitly, or a broken page looks like "no changes".
- Re-run the diff after every late fix, not just once. Mine went green, then
  I edited the navbars again.
