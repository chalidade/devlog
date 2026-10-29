# Saling Jaga: Private Messages and a Meeting Point

Day three of [Saling Jaga](https://github.com/chalidade/saling-jaga), v0.19.0
and v0.20.0, plus a shorter website.

- **End-to-end encrypted private messages (v0.19.0).** Tap a member, then "Kirim
  pesan pribadi". Each phone keeps its own P-256 key, and messages are sealed with
  ECDH plus AES-GCM, with the sender and recipient names authenticated too. The
  group owner and bridges only relay them. A message to someone who's out of range
  waits ("Menunggu X tersambung…") and goes out when their key arrives again.
  Notifications don't show the text. The first key seen for a name is pinned, and
  a changed key shows a warning in the chat. Tests check that only the recipient
  can open a message, that a forged sender is refused, and that a fake member
  can't publish a key in someone else's name
- **A shared meeting point (v0.20.0).** Anyone in the group can set a "titik
  kumpul" at their own location or on the map. It shows as a flag on the compass
  and map with distance and direction, plus a banner on the main screen, and
  members within 30 m are marked as arrived. The owner hands the latest point to
  phones that join or come back. An older point never replaces a newer one, and
  older phones aren't sent the new frame
- **A shorter landing page.** The [site](https://chalidade.github.io/saling-jaga/)
  is cut to what a visitor needs to decide and install: a one-line hero, six
  feature cards, five screenshots, three install steps, four security points and
  a short FAQ. The full install walkthrough and the permission list moved into
  collapsible sections

**Lesson:** encrypting each link (yesterday) protects the group from outsiders.
Private messages need a second layer, because the owner relaying the message is
inside the group.
