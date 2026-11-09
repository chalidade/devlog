# Saling Jaga: Roll Call, Elder Mode and Missing-Person Cards

A long day on [Saling Jaga](https://saling-jaga.com), my offline emergency app:
v0.28.0 to v0.34.0. Claude Code wrote the code and tests; I picked the features
and merged the pull requests.

- **Chat history survives closing the app**, on Android and iOS
- **Roll call:** ask the whole group how they are and see who hasn't answered. The
  group owner holds the open call for phones that join late, and the new frame only
  goes to phones that say they support it, so 0.28 and older stay connected
- **Battery:** Wi-Fi drops out of high-performance mode unless someone is talking,
  on a call or in SOS. GPS rests after a minute within 25 m and wakes on the
  significant-motion sensor, on SOS or when a map page opens
- **A key-change bug.** When a member's private key changed, the app warned but
  still sent queued messages to the new key, so someone joining later under a
  freed-up name would receive them. Now the old key stays pinned and the app asks
  once whether to trust the new one
- **Mode lansia:** an opt-in screen for older family members with three big buttons
  (SOS, I'm safe, hold to talk) and the family's status
- **Cari keluarga:** a "have you seen this person?" card that reaches every phone in
  the group, crosses bridges to other groups, goes out over LoRa as a short line, and
  is kept for 7 days so it reaches the next group a phone joins
- The networking engine moved into `core/`, a plain Java library that builds with
  only a JDK, and the project now builds and tests on macOS

**Lesson:** the app showed a warning and then went ahead anyway. When a key
changes, it has to stop and ask before sending anything.
