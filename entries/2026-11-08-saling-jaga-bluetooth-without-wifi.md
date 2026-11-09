# Saling Jaga: Chat and SOS Over Bluetooth

[Saling Jaga](https://saling-jaga.com) v0.49.0 to v0.52.1: phones near each other
can now talk with no Wi-Fi and no group at all.

- **Bluetooth nearby.** Every Android phone runs a small GATT server and client.
  Messages reuse the LoRa format, so one id de-duplicates them across Bluetooth,
  LoRa and the Wi-Fi group. Store and forward for 6 hours; location goes along only
  with an SOS
- **Hop limits by kind:** SOS, status and meeting points travel 7 hops, chat 3. A
  sender claiming more than its kind allows is cut back at the next phone
- **Private messages over Bluetooth,** end-to-end encrypted with a key from ECDH of
  the two identity keys, padded to one size and with no recipient named. Every phone
  passes it on; only the recipient can open it. Safety codes can now be matched by
  scanning a QR
- **A chat list as the main screen:** Nearby, Group, and one row per private chat,
  with an emergency menu in place of the SOS button. iPhone got the same
- **Review fixes (0.52.1):** emoji count as 6 bytes in Java's modified UTF-8, so
  emoji-heavy chat outgrew the packet and crashed Android; an SOS handed on after
  it was cancelled no longer comes back
- **Tests gate releases.** JaCoCo coverage is reported in CI (66% of lines), new
  tests cover the UTF sizing, the laptop app's WebSocket, the LAN and the bridge.
  Until now a push to main could ship without running the tests

**Lesson:** a byte budget has to be counted the way the bytes are written. A
string's length and its encoded size differ most for emoji.
