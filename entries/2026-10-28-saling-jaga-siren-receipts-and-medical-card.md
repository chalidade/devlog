# Saling Jaga: A Siren, Read Receipts and a Medical Card

The evening of day two on [Saling Jaga](https://github.com/chalidade/saling-jaga).
Most of it came from feedback after a hike with testers.

- **Siren and SOS flashlight (v0.17.0).** A "Sirine & senter" chip opens a
  full-screen page that starts right away: a wailing siren on the alarm stream at
  full volume, and SOS in Morse on the camera flash. Phones without a flash blink
  the screen instead. Turning it off restores the alarm volume and the screen
  brightness. It needs no group and no signal
- **Missed announcements are replayed.** The owner keeps the last 50
  announcements and replays them, oldest first, to a phone that joins or comes
  back. The phone shows only the ones it hasn't seen, marked "terlewat saat
  terputus". Replays are accepted only from the owner's side, so a member can't
  fake one
- **"Terkirim ke: Budi, Sari".** Every text and announcement is acknowledged, so
  the sender sees who got it, including phones that got it later by replay. The
  ids come from the content, so no id travels with the message. Older phones
  close a link on an unknown frame, so new phones first send an empty CAPS frame
  (older ones ignore it), and ACK and REPLAY only go to links that sent one
- **Rejoin in seconds.** Testers thought rejoining didn't work, because scans
  backed off to once a minute and a failed dial waited 20 s. Now the first scan
  runs after half a second, scans back off to every 10 s at most, and the old
  owner is redialed every 6 s while it's in range
- **An emergency medical card**: blood type, allergies, conditions, regular
  medicines, a family contact and notes, kept only on the phone and shown in
  large print so a rescuer can read it. If the owner allows it, a short summary
  rides along with presence while they're in SOS or injured. It's appended after
  the existing presence fields and cut to fit the 256-byte frame, so older
  versions just ignore it

**Lesson:** rejoining worked all along. With one scan a minute and a 20 s wait
after a failed dial, testers reasonably decided it didn't.
