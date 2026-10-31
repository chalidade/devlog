# VWO Job Fair: Analytics for the Organiser, Seats for Companies

Day two of the fair on [jobfair.co.id](https://jobfair.co.id): six pull requests
merged, all from what the organiser asked for while watching the event. Claude
Code wrote the code and tests; I set the rules and checked every screen.

- **Analisa, a new tab in the organiser hub:** how long people stay (average,
  median, longest, shortest, a histogram), the busiest hours in WIB, new and
  returning visitors, applications per vacancy and per stand, seminar
  attendance, mini game players and coins earned and spent, with a CSV export.
  Staff, panitia and company accounts are left out of every number, and the
  export holds only totals, no names
- **Seats per package for the company portal:** each package includes a set
  number of people who can open the portal, the company registers their emails
  itself, and extra seats cost coins at a price the organiser sets. Existing
  team members kept their access
- **Stand spacing in floor squares:** the organiser sets "kiri-kanan" and
  "atas-bawah" from 1 to 6 squares per floor, and the hall grows taller to fit,
  so a wide gap no longer pushes stands off the map
- **Two fixes to Analisa the same evening.** It could hang on "Memuat…": the
  server ran 17 queries at once on a small shared connection pool with no time
  limit. They now run one after another on one connection, with a timeout per
  query, a deadline for the whole answer, and a page that stops waiting. On
  30,000 invented accounts a week of data takes about 1.5 s. And "returning
  visitors" showed 0 for the full range, because it only counted people seen
  before the range began; it now counts anyone who came back on a later day

**Lesson:** a metric's definition has to survive the widest range the screen
allows. "Returning = seen before the start date" looked right for one week and
was always zero for "all time".

**Next:** a visitor funnel (sign-up, hall, stand, application) once the
organiser picks which numbers matter most.
