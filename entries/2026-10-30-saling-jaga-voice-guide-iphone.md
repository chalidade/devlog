# Saling Jaga: Voice Notes, a First-Aid Guide and an iPhone App

The afternoon on [Saling Jaga](https://saling-jaga.my.id), v0.24.0 to v0.27.0.
Claude Code wrote the code and tests; I decided the scope and checked every
screenshot.

- **Voice notes (v0.24.0):** with nothing typed, the send button records up to
  a minute of AAC at 24 kbit/s, about 180 KB, with "Terkirim ke" receipts.
  Phones announce that they can play them, so 0.23 phones are never sent one
  and stay connected. A test failed once in CI: the note went out before the
  owner had read one member's announcement. The fix waits for a text from each
  phone first, since frames on one link arrive in order
- **An offline disaster and first-aid guide (v0.25.0):** six disasters and ten
  first-aid topics, from CPR to snake bites, with emergency numbers that open
  the dialer. It opens without a group
- **An iPhone version**, in the same repo. iPhones have no Wi-Fi Direct, so
  iPhones join each other over Bonjour and join Android groups through post
  Wi-Fi mode. CI runs the Android Java protocol code against the Swift code in
  both directions. It is not installable yet; that needs TestFlight
- **English as well as Indonesian (v0.26.0)**, and a new layout in v0.27.0
- **The website moved to [saling-jaga.my.id](https://saling-jaga.my.id)** with a
  night-themed redesign

**Lesson:** when two codebases speak one protocol, the useful test runs one
side's real code against the other's, not two copies of the spec.

**Next:** field tests with three phones, then the Play Store closed test.
