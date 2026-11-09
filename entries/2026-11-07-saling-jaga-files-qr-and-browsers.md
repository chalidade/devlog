# Saling Jaga: Files, QR Codes and Laptops Without Internet

[Saling Jaga](https://saling-jaga.com) v0.47.0 to v0.49.0, the widest day so far.

- **Send any file without internet,** to the group or privately. Chunks travel
  behind voice and chat; a private file is sealed with a fresh AES-256-GCM key that
  goes first in a private message. Only safe file types travel, checked by
  extension and by content on both ends, and an APK shows a warning
- **Join by QR.** Each phone shows a QR made without a library; another phone scans
  it in the app (ZXing's decoder, vendored with its license) or with its camera
  through a `saling-jaga.com/j` link. Links from outside the app always ask first
- **Saling Jaga Web.** A small server on a laptop joins a group over shelter Wi-Fi
  with the app's own Java engine and serves a page to browsers on the same network.
  Each browser is a member: chat, status and SOS, photos, files, roll call and
  push-to-talk. It ships as a portable app for Windows, macOS and Linux with its own
  Java. The Android app can also host the page itself
- A review hardened it the same night: limited code guesses, SOS alerts kept across
  reconnects, and a deadlock in the gateway fixed
- A written plan for a semi-automatic Wi-Fi Direct bridge, with a three-phone test

**Lesson:** the laptop server took a day because it reuses, unchanged, the engine
I moved into a plain Java library on 1 November.
