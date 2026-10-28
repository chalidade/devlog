# Saling Jaga: Photos, Video, Bridged Groups and an Offline Map

The [morning's entry](https://github.com/chalidade/devlog/blob/main/entries/2026-10-27-saling-jaga-offline-emergency-app.md)
covered the first seven PRs. The rest of the day took
[Saling Jaga](https://github.com/chalidade/saling-jaga) from v0.6.0 to v0.10.1,
with Claude Code writing the code and me reviewing builds and screenshots.

- **Photos (v0.7.0).** A new IMAGE frame, at most 400 KB. A picked or captured
  photo is shrunk to 1280 px, the EXIF rotation applied, and saved as JPEG under
  400 KB. Capture goes through the phone's camera app into a one-file content
  provider, so the app still needs no CAMERA permission
- **Short video clips (v0.8.0).** Up to 15 s and 4 MB, sent as 32 KB chunks on a
  separate bulk queue so voice and chat always go out first. Receivers
  reassemble per sender with bounded memory
- **A smaller layout (v0.8.1)** so chat gets most of the screen: the group card
  folds to one line of status-ringed faces
- **Bridging two groups (v0.9.0, experimental).** A member's phone forms its own
  Wi-Fi Direct group for phones further away and joins the original group as a
  normal Wi-Fi client. Every group owner sits at `192.168.49.1`, so owners share
  their IPv6 link-local address with members, because that address is the only
  thing that tells two owners apart. The hub still binds each sender to the
  link it first appeared on, so relaying reaches everyone once and nobody can
  speak for someone else
- **Wi-Fi Direct BUSY errors.** Tapping connect while an earlier invitation was
  still pending failed with "kode 2". The app now cancels the pending
  invitation and scan, retries twice, and otherwise says in plain words what
  went wrong
- **An offline street map (v0.10.0).** OpenStreetMap tiles within 3 km, kept
  under OSM's limit of 250 tiles at zoom 13 and above, with a proper
  User-Agent, downloaded only when the user starts it. The map shows every
  member's position with a status ring
- **A more honest radar (v0.10.1).** The compass corrects for magnetic
  declination, smooths jitter the short way round, and asks for a figure-8
  calibration when the magnetometer reports low accuracy. When two members'
  GPS accuracy circles overlap, it shows "dekat, ±X m" (close) instead of an
  arrow it can't actually know
- **The website:** a redesign, a 32-second demo video that loads only on play,
  a link-preview card (the old `og:image` was a relative path, which scrapers
  ignore), SEO and an issue-form feedback section, and an install guide with
  real Play Protect screens plus a 40-second walkthrough video

**Lesson:** when two members stand closer together than GPS can resolve, any
direction arrow is a guess, and "close, ±X m" is the most the app can honestly
say.
