# VWO Job Fair: Coin Audits, Sponsor Controls and a Story Video

Day five of the fair on [jobfair.co.id](https://jobfair.co.id): six pull requests
merged, all from the event partner's feedback. Claude Code wrote the code and tests;
I decided how each request should behave and checked the screenshots before every
merge.

- **Organisers can see where a company's coins came from.** The partner spotted a
  company with over 100,000 coins and asked how. Each stand card now shows the
  coins left across the company's accounts, and tapping it lists every account with
  totals per source (bought, granted, welcome, spent) and its recent ledger rows. The
  source comes from the ledger row's unique key, not its free-text reason. The main
  admin can also take coins back, with a required reason, an audit row and a check
  inside the transaction so a balance never goes below zero
- **The portal showed the wrong wallet to organisers.** When an organiser opened a
  company's portal, the coin count was the organiser's own balance. It now shows the
  company's, and the pay buttons are disabled for that view
- **Sponsor banners can be deleted, hidden and added.** Removing every sponsor used
  to be refused by the guard that protects a setup from being wiped, because an
  empty list counted as no setting at all; an emptied list now counts as one
- **Studio CV on a phone.** The CV form's tab block covered the first fields of
  each section. The cause was a grid row collapsing to 0px inside a fixed-height
  scroll container; the fix is one `grid-auto-rows: max-content` plus letting the
  four rows of tabs scroll away on small screens
- Also shipped: organiser-set aliases for the applicant sign-in link (like
  `/virtualjob`) and a simpler company sign-up form
- Made two narrated story videos with real screens from the app and drawn scenes,
  rendered by [vigenco](https://github.com/chalidade/vigenco) with an ElevenLabs
  voice: a job seeker applying from Sumba (1 min 52 s), then the same hire from the
  HR side (60 s)

**Lesson:** when a number looks wrong, build the screen that explains it before the
button that changes it. The coin breakdown answers "how" for every company; the
deduct button only fixes one.

**Next:** check the coin breakdown against a real company's ledger with the partner.
