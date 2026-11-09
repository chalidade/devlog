# Saling Jaga: Safety Codes, Forward Secrecy and a .com

[Saling Jaga](https://saling-jaga.com) private messages got stronger in three
steps, v0.39.0 to v0.40.0, and the site moved to its final domain.

- **Safety codes.** Two people compare a code made from both public keys; a match
  marks the chat as verified until a key changes. A review the next morning
  hardened it: pins now keep the full SHA-256 of a key instead of a 4-byte
  fingerprint someone could match, and the code grew from 15 digits to 60 from
  SHA-512, because a phone in the middle only has to make its two codes collide
- **Sessions.** Each connection now uses a throwaway P-256 key, signed by the
  phone's identity key and kept only in memory, and the message key comes from
  those through HKDF. Stealing an identity key later no longer opens recorded
  messages. Messages carry no recipient and are padded, so relays don't learn who
  a message is for or how long it is; they still see the sender and the timing
- **The identity key is sealed** by an AES key in Android Keystore
- **New domain:** `saling-jaga.com`, with `saling-jaga.my.id` redirected through a
  small [redirect repo](https://github.com/chalidade/saling-jaga-redirect). The
  link preview went from a 380 KB PNG to a 105 KB JPEG
- A Support button next to Download, and the release now signs and deploys in
  a separate GitHub release environment

**Lesson:** encrypting the message body still leaves a lot exposed: who the
message is for, how long it is, and every recorded message once a key leaks.
