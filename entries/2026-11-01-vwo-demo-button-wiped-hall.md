# VWO Job Fair: A Demo Button That Wiped the Live Hall

Day three of the fair on [jobfair.co.id](https://jobfair.co.id): five pull
requests merged, all from feedback the event partner sent during the day.
Claude Code wrote the code and tests; I sorted the feedback, picked what to fix
first, and checked every screen before it went live.

- **A demo button reset the organiser's hall.** The profile panel still had
  "Hapus data demo", left over from the GitHub Pages demo. On the live site it
  reset the local game state to the demo defaults, and because an organiser's
  browser keeps the hall setup in sync with the server, the reset was saved
  over the real setup. The button is gone from the live build, a reset no
  longer touches the organiser's setup there, and the same PR replaced a line
  that read as if companies pay to see job seekers' profiles
- **Riwayat pengaturan:** every change to the hall setup now keeps the
  previous version, and the organiser can restore one from the hub. The server
  also refuses a save that would replace a full setup with a blank one. This
  could not bring back the setup lost that morning, because the history starts
  now
- **Peta:** the company list moved under the floor plan instead of covering it
- **Staff Umum clean-up:** an old seed added a "Staff Umum" vacancy to every
  new stand. The seed was removed days ago, but the vacancies stayed in the
  data, so the hub got a one-click tool to delete them all
- **A new hall layout:** lifts, sofas and coin stands moved into bands along
  the side walls, sponsor standees into the aisle between stands, and the info
  desk into the bottom aisle. A new test walks every stand count and spacing
  and checks that nothing overlaps a stand and every stand, lift and seat can
  still be reached

**Lesson:** a demo-only control has to be removed from the live build, not
just hidden behind a label. Here it combined with an auto-sync loop, and
together they wrote demo defaults over production data.

**Next:** VIP stands that take the space of two regular stands, at most three
per row.
