# VWO Job Fair: Launch Day

The event opened on 30 October. The day was 21 commits on
[jobfair.co.id](https://jobfair.co.id), mostly closing the gaps that real
companies and job seekers ran into. Claude Code wrote the code and tests; I set
the rules and checked the screens.

- **Applying needs a complete profile:** name, email, WhatsApp, education,
  skills and a CV link, so HR gets data they can act on. One shared rule drives
  the game form, the lite form and the API, which answers with the list of
  missing fields in Indonesian
- **"Mulai di sini" checklists** for companies (logo, profile, recruiter, an
  open vacancy, FAQ, then legal details, "x dari 6 selesai") and for job
  seekers, with an applicant funnel card for the organiser
- **A company sign-in page:** Google, or a company code and PIN for teams
  without a Google account
- **Halls fit their floors:** the organiser sets how many stands a floor has
  and how far apart, and the hall narrows to fit, so a small fair does not look
  empty. The main hall can be switched off
- Privacy policy and terms pages, free applying without a "-0" voucher line,
  and phone polish for the game UI

**Lesson:** a validation rule that lives in one shared module can be enforced
by the server and explained by every form, and the two never disagree.

**Next:** watch the applicant funnel during the fair and fix what it shows.
