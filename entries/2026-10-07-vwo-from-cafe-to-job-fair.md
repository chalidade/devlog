# VWO: From a Virtual Cafe to a Walkable Job Fair in One Day

[VWO](https://chalidade.github.io/vwo/) started the day as design docs for a
virtual cafe (ERD, DFD, notes) and ended it as a job fair you walk through as a
character: 15 PRs merged (#1 to #15). Claude Code wrote the code and the docs; I
set the direction after each build and tested on my phone.

- Base first: database schema, a realtime world and a live view (#1), then
  top-down RPG art so tables, seats and people read as a place, not a floor plan
- **The pivot:** a Job Fair room with company booths, vacancies and applications
  (#5), grown the same day to six floors joined by a lift, a food court, and
  psikotes and seminar rooms
- A coin economy with levels and ratings, so applying costs something and
  booths earn a reputation (#9); sofa mini games and daily missions give a reason
  to stay after the booths
- Live multiplayer, and the two sides the fair needs to run: a company portal
  for booths, vacancies and applicant review (#14), and an organiser hub with a
  speaker stage (#15)

**Lesson:** a cafe was a nice demo with no reason to come back. Giving the same
walking engine a job to do, literally, gave every feature after it a purpose.

**Next:** make the hall fast on phones and close the loop from HR back to the
applicant.
