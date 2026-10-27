# Saling Jaga: Walkie-Talkie, Chat and SOS Between Phones With No Signal

[Saling Jaga](https://chalidade.github.io/saling-jaga/) ("look out for each
other") is an Android app for when the network is gone: after an earthquake, on
a mountain trail, in a crowd that jams the towers. Phones talk to each other
directly over Wi-Fi Direct. No SIM, no server, no account. Claude Code wrote
most of the code; I set the scope, the brand and the business model, and
reviewed every build and screenshot. Seven PRs merged today, v0.6.0 is out.

- **Wi-Fi Direct instead of a web app.** A browser can't open phone-to-phone
  links without internet, so it had to be an APK. One phone owns the group and
  relays every frame to the rest of the group (up to 16 phones) over a small
  binary protocol on TCP
- **SOS that can't be faked.** The group owner drops any frame whose sender
  isn't the link it arrived on, so nobody can raise an alarm in someone else's
  name. SOS shows distance and direction ("259 m to the north-west") and stays
  on for late joiners until the sender cancels it
- **SOS + SMS** for the in-between case: towers up, no data. It opens the SMS
  app with a Google Maps link and battery level for up to three emergency
  contacts, so the app never needs the SMS permission
- **Built without Gradle.** Google's Maven was blocked in the cloud sandbox
  Claude Code ran in, so the APK comes from Ubuntu's Android SDK packages,
  `javac`, `dx`, `aapt` and `apksigner`. The result is 214 KB with zero
  dependencies. How:
  [building an Android APK without Gradle](https://github.com/chalidade/devlog/blob/main/notes/building-an-android-apk-without-gradle.md)
- **Every push to main ships a release** with the APK, its SHA-256, the signing
  certificate fingerprint and the build log, so people who get the file from a
  WhatsApp group can check it. A permanent release key and an auto-increasing
  `versionCode` mean the next APK installs as an update
- Licensed AGPL-3.0 with an open-core plan: free for citizens, paid editions for
  disaster posts, SAR teams and schools. The name and logo stay trademarks

**Lesson:** for an app people install from a link instead of a store, trust is
a feature you have to build. Reproducible builds, a published checksum and a
short permission list do more than a "safe" badge ever could.

**Next:** test with five phones from different brands in the field. The
protocol is tested over real sockets, but nothing has run on real hardware yet.
