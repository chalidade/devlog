# Pulau Aru: Two Episodes a Day

By now [Pulau Aru](https://pulau-aru.web.id/) runs on a runbook: a scheduled Claude
Code session makes one roughly 60-second episode at 10:00 and another at 17:00 WIB,
builds what the episode promises into the game, records it, adds the
[Vigenco](https://github.com/chalidade/vigenco) voice-over and hands it to me to
post on TikTok. Episodes 7 to 12 went out over these two days.

- **Paid requests.** A Trakteer donation becomes a request that gets built right
  away: an honesty canteen, ten "lamps of encouragement", a coffee shop and a night
  watch post, a welcome gate
- **Kebunku (my garden):** visitors buy seeds, plant and harvest in a fruit field,
  saved on their own device
- **Performance.** Buildings were made of dozens of small boxes, over 3,500 draw
  calls together with the residents. Merging each building into one mesh per
  material brought it to about 1,900, with shadows updated every 2 frames (3 on
  phones), pixel ratio capped, and fewer walkers (64 on desktop, 36 on phones)
- Buildings resized against people: the school, pharmacy, hospital and police post
  had been toy-sized
- The runbook now keeps every episode's video as a GitHub Release, so one can be
  posted later

**Lesson:** a low-poly scene can still be slow. The cost was the number of
objects, not polygons, and merging meshes fixed it without touching how anything looks.
