# VWO Job Fair: A Shorter Company Sign-Up That Asks for More

The company form at [jobfair.co.id/daftar-perusahaan](https://jobfair.co.id/daftar-perusahaan)
got the same treatment as the applicant page (PR #129). Claude Code wrote the code,
tests and screenshots; I decided which questions a company should answer and which
it should never be asked.

- Two steps instead of one long page: "Perusahaan" and "Kontak & kebutuhan", with
  one-tap chips, Indonesian inline errors and a draft that survives a reload
- **Every new question is optional:** headcount, how many vacancies and in which
  fields, which event, which package (names only, no prices), a short description,
  a LinkedIn or Instagram link, and how they heard about us. The required fields
  are the same seven as before, so the form is no slower to send
- No tax number or ID fields: a sign-up form is the wrong place for them
- The answers do work later: opening a booth from a request preselects the package
  and fills the booth's description, website, headcount and social link
- The server checks every new field against the same option lists the page shows,
  and drops a chosen event that is no longer open

**Lesson:** collect data at the moment it saves someone a step. A field that pre-fills
the booth is worth asking for; a field nobody reads only makes the form longer.

**Next:** bring the same questions to the booth request inside the game.
