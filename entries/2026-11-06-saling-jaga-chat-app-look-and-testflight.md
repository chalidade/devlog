# Saling Jaga: A Chat-App Look, TestFlight and a Join Race

[Saling Jaga](https://saling-jaga.com) went from v0.40.1 to v0.46.0: bug fixes in
the morning, a new look in the afternoon.

- **A race when phones join at once.** The group owner listed a new link before
  queueing its own HELLO, so another phone's relayed HELLO could arrive first.
  The new phone then mistook that phone for the owner and, for the whole
  connection, sent no receipts, private messages, voice notes or roll calls. The
  same bug made a CI test fail at random. The owner now queues its own frames
  before the link becomes visible
- Photos decode off the screen thread, only clips that can finish are announced,
  and holding the talk button in simple mode no longer crashes
- **Search shows only group leaders** once a group is in range; tapping a member
  used to pull it out of its group
- **Members across a bridge** are marked: the owner tells its members which far
  group each phone belongs to
- **A chat-app layout** with a dark green header, on Android and iPhone, and a new
  compass radar with a big arrow to the SOS
- **iOS TestFlight** from a GitHub Actions macOS runner with an App Store Connect
  API key, so no Mac is needed
- The launch video was remade with the new look, in Indonesian and English

**Lesson:** a test that fails "at random" was a real bug here, a race in the
order of the first frames. Worth chasing before marking it flaky.
