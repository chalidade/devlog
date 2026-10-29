# VWO Job Fair: The Day Before Launch

The event opens on 30 October, so 29 October was 16 pull requests on
[jobfair.co.id](https://jobfair.co.id): a front page, a third payment gateway,
a more forgiving Excel import and a lot of smaller fixes. Claude Code wrote the code and tests; I set the rules and checked the
screens.

- **The game is the front page.** After launch, `/` sends a 307 redirect to
  `/play/` and keeps the query (`/?ref=abc` goes to `/play/?ref=abc`). It is a
  redirect, not the app served at `/`, because the manifest scope, the service
  worker, the install button and every link the server sends (Google sign-in,
  invites, push and mail) all live under `/play/`. The landing also lists the
  events open for pre-registration, from a public `GET /api/prereg` cached for
  180 s, and the organiser got a switch that hides the job seeker buttons on the
  home page without blocking anyone who has a link
- **BorderPay as a third gateway**, next to Xendit and Midtrans (QRIS, virtual
  account, e-wallet). The webhook checks its token in constant time, then ignores
  the status and amount in the body and asks BorderPay's API for the payment
  itself. A payment is credited only if it's `paid` and the amount matches what
  we stored. A follow-up fix: after switching from a test key to a live key, an
  old checkout page marked "MODE TEST" was still being reused, so each checkout
  now records which key mode made it
- **The Excel import reads real files.** Files companies had actually filled in
  ("Rp 3–5 juta/bulan", "1-2 Tahun", "Diploma/S1", "31/11/2026") came out as
  "0 siap diimpor, 7 bermasalah". Now each cell is read as the closest value the
  job form allows, and every adjustment shows as a note under the row. A
  location like "SEMUA AREA COVERAGE CABANG KLATEN" now finds Kab. Klaten. The
  organiser can also import vacancies for a company from the hub, for free;
  the server marks those as "Dipasang panitia" and a company's save can't fake
  or remove the mark
- **Company sign-in only lets in a company's email.** Before, any Google account
  could sign in and got a fresh account. Now an email that belongs to no company
  gets no account and no session cookie, and sees a note on how to register
- Smaller fixes: long company names break over two lines on the stand sign
  (a pure `fitSignName` helper picks the lines and font size, with tests); the
  first package is called "Basic" everywhere, and missing features show a red X
  instead of a grey dash; Aula viewers in slide mode see the current slide
  instead of an empty stage; the stage chat follows new messages; the hub and
  company portal got a "Keluar akun" button; a salary field no longer pushes a
  phone page sideways

**Lesson:** never trust a payment webhook's body. Use it only as a signal to go
and ask the gateway, and credit what the gateway says.

**Next:** the event itself, and whatever it turns up.
