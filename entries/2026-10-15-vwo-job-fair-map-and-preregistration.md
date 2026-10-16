# VWO Job Fair: A Floor Map, Pre-Registration Codes, and Anti-Bot Checks

[jobfair.co.id](https://jobfair.co.id) is my virtual job fair. Today was about
the day the doors open: visitors can see where each company is, register for an
event before login opens, and the sign-up form got harder to spam (PRs
#114–#117). Claude Code wrote the code and tests; I decided what each screen
should do, reviewed it on desktop and phone, and sent back what looked wrong.

- A map panel in the bottom menu shows every floor and which companies are
  hiring there, so you can walk to a stand the way you would follow a map in
  Minecraft. I dropped the corner minimap from the first version because it
  crowded the screen, and redid the phone layout with floor chips, a plan/list
  toggle and a card when you tap a stand
- **Pre-registration per event.** Organisers create an event and share its
  link; applicants fill in their data once and get a code like `JF-XXXX-XXXX`
  with a QR to screenshot. When login opens, signing in with the same Google
  account links the registration and fills only empty profile fields, so the
  launch-day sign-up spike moves to the weeks before it
- The sign-up form now carries a signed, single-use token that must be between
  3 seconds and 2 hours old, plus a small proof-of-work puzzle in the browser.
  Throwaway email domains are refused and Gmail dot/+tag variants count as one
  inbox. In a local bot simulation, accepted fake sign-ups went from 100/100 to
  0/100 for a plain script, and from 200/200 to 1/200 for variants of one Gmail
- Suspicious sign-ups get a badge with the reason, and organisers can delete
  them in bulk. Only salted hashes of the network and inbox are stored, never
  the raw IP
- The bot test caught a race of its own: 19 of 200 parallel Gmail variants
  slipped past the duplicate check. Moving that check inside the event's locked
  database transaction brought it to 1

**Lesson:** a duplicate check that runs before the write is a suggestion. Under
parallel requests, the only check that holds is the one inside the same lock as
the insert.

**Next:** a rehearsal with real visitors on phones and laptops before the first
public event.
