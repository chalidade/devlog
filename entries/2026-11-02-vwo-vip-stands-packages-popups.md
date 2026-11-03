# VWO Job Fair: VIP Stands, Clearer Packages, One Look for Pop-ups

Day four of the fair on [jobfair.co.id](https://jobfair.co.id): three pull
requests merged, all from the event partner's feedback. Claude Code wrote the
code and tests; I decided how each request should behave and checked the
screenshots before every merge.

- **VIP stands take two slots.** A VIP stand now sits centred across two
  regular stand slots, with at most three VIPs per row. Where the VIPs go is
  computed fresh from the saved stand order every time, by the same function
  on the server and in the game, and never stored, so switching a floor back
  to the old layout puts every stand on its own slot again. The organiser's
  Lantai tab counts a VIP as two places, and the server refuses a booking on
  the second half of a VIP
- **Package names a company understands.** The company sign-up page now
  offers Paket Promosi, Paket VIP, Paket Reguler or "Belum tahu", each with
  one line on who it is for, and says that every package comes with free
  coins to try the virtual features. The partner asked for this so companies
  don't hold back thinking they must pay before they start. The stored values
  stayed the same, so earlier requests still read correctly
- **One look for in-game pop-ups.** Profile, map, wallet, applications and
  the apply form moved from the game's cream and orange to the brand's black,
  white and yellow, with one button size, one tab grid and yellow only for
  each pop-up's main action. It is a CSS-only change that adds about 1 kB
  gzipped

**Lesson:** derive layout from saved data instead of saving the layout. The
VIP placement can change its rules later without migrating anything, and
undoing it is just a setting.

**Next:** check the pop-ups not covered by screenshots (lift, library, park,
games) on a real phone.
