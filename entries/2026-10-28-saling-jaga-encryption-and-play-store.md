# Saling Jaga: Encrypted Links, Android 16 and a Play Store Build

Day two of [Saling Jaga](https://github.com/chalidade/saling-jaga), v0.11.0 to
v0.12.0. Most of the day went to privacy.

- **Android 16 (API 36) and an App Bundle.** Edge-to-edge layout padded by the
  system bars and keyboard, back handled with `OnBackInvokedCallback` (since
  `onBackPressed` is no longer called), and foreground service types
  `connectedDevice|microphone`. The Gradle-free build script now uses the
  Android SDK's `aapt2` and `d8` and builds an `.aab` with bundletool. CI checks
  the Play requirements on the built APK and bundle
- **A Play Store kit:** a privacy policy page, listing text and graphics, and a
  publishing guide. The app has been field-tested now, so the README no longer
  says it hasn't
- **Tighter privacy.** A member has to ask the group owner before becoming a
  bridge, and only an approved member gets the group's Wi-Fi password plus a
  random token its uplink must present. Before this, a forged BRIDGE frame could
  add made-up members and speak as them. Video clips are remuxed to strip MP4
  metadata (location, phone model) before sending, and a clip that can't be
  cleaned isn't sent. Message notifications are hidden on the lock screen, SOS
  stays visible. The bundletool checksum is pinned in CI, since that step can
  use the release key
- **Every link is encrypted (v0.12.0).** Each side opens with a KEY frame
  carrying a fresh P-256 public key. ECDH plus HKDF-SHA256 gives one AES-256-GCM
  key per direction, and every later frame (type, sender and payload) is sealed
  with a counter nonce, so an altered, replayed or reordered frame closes the
  link. Knowing the group's Wi-Fi password is no longer enough to read the
  group. Tests record the wire and check that names and messages never appear in
  the clear, and that one flipped bit drops the link. Older versions are told to
  update
- **Rejoining after walking out of range.** A member now remembers its owner,
  scans with backoff while the group is lost, and redials that owner when it's
  back, asking not to become owner itself. That stops the group from splitting
  in two. It gives up after 15 minutes
- Smaller things: releases skip pushes that only touch the website or docs
  (re-uploading reset the download counts), and GoatCounter visitor stats are
  on for the site

**Lesson:** the group's Wi-Fi password protects the radio link, not the
conversation. Anyone with that password could listen to the group until every
link was encrypted on its own.
