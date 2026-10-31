# Saling Jaga: Further Than Wi-Fi Direct, With LoRa

[Saling Jaga](https://saling-jaga.my.id) is my offline emergency app. Wi-Fi
Direct reaches about 100 m, so the morning went into reaching further, then two
smaller safety features. Three versions, v0.21.0 to v0.23.0. Claude Code wrote
the code and tests; I chose what to build and in which order.

- **Post Wi-Fi mode.** Phones on the same Wi-Fi (a building, a router, or a
  long-range antenna link between posts) form a group with a 6-digit code. The
  code is mixed into the encryption keys, so a wrong code never opens a link,
  and repeated wrong guesses from one address are shut out for a while
- **A LoRa gateway.** A Meshtastic radio connects over Bluetooth, and messages,
  announcements, status, SOS and the meeting point travel to other groups that
  have one, several kilometres away. I wrote the protobuf by hand rather than
  adding a library, and each message fits in one 233-byte packet. It has not
  been tested on real radios yet
- **An antenna helper:** direction, distance, Fresnel zone and Earth bulge to
  another post, from GPS and the compass
- **SOS from the volume keys:** five presses in three seconds, with a five
  second countdown to cancel. Android does not pass the keys to apps when the
  screen is off, and the README says so
- **Battery saver:** location every 2 minutes instead of 30 seconds and a dim
  screen, back to full speed during SOS. It turns itself on once at 15%

**Lesson:** for a radio link with 233 bytes per packet, a few lines of
hand-written protobuf beat a library that is bigger than the whole app.

**Next:** two Meshtastic radios on 923 MHz for a real range test.
