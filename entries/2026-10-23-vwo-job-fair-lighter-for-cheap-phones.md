# VWO Job Fair: Lighter for Cheap Phones, Pictures Out of the Database

A week before the 30 October event, five pull requests went live on
[jobfair.co.id](https://jobfair.co.id). Most of the work was making it cheaper to
run and lighter on the phones visitors actually use. Claude Code wrote the code
and tests; I chose what to cut, what to keep and how to check it.

- **First visit to the game is 18 KB lighter (gzip).** JS went from 176.9 to
  168.2 KB and CSS from 56.0 to 46.7 KB. Dashboard styles now load only when a
  dashboard opens, and lists the landing page never reads are left out
- On the busiest floor (150 chairs), the hall redrew 159 components every frame.
  Memoising the furniture brought it to 12, and fps went from 27 to 36 with the
  CPU throttled 4x
- Moving CSS between files can silently change which rule wins, so a split was
  only accepted after comparing computed styles on 122 screens, at phone and
  desktop width: 0 differences
- Uploaded pictures used to be stored inline in Postgres. They now go to object
  storage, shrunk in the browser first (WebP, 160 px for profile photos, 800 px
  for wide images), so uploading stays free for job seekers
- Companies can submit their legal papers for a verified badge, and every
  vacancy says that companies may not ask applicants for money, with a button
  to report one that does
- Organisers now see where visitors came from (campus, community, referral) and
  how many people each source brought in

**Lesson:** a CSS refactor that "looks the same" in a few screenshots is not
proof. Compare computed styles on every screen, or don't move the rules.

**Next:** run the whole flow end to end on a cheap phone before 30 October.
