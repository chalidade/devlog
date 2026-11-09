# Pulau Aru: An Island Built by TikTok Followers

[Pulau Aru](https://pulau-aru.web.id/) is a 3D low-poly game in the browser
(three.js) and a TikTok series at the same time. Every follower becomes a resident
of the island, and comments decide what gets built next. Each episode shows the
island exactly as the game has it. Built in one day with Claude Code.

- **Followers are residents.** A GitHub Action reads the follower count through
  TikTok's Display API, every 15 to 30 minutes, and updates
  `data/island.json`. Names come from TikTok's data export or an Apify scrape and
  are carved into a Batu Nama (name stone) by the beach. 423 followers in the
  morning, 2,905 by the evening
- **A creator panel** (`?kelola`) edits residents, buildings and episodes and
  publishes straight to the repo with a fine-grained GitHub token kept in the
  browser. A red "not published" bar stays visible, and publishing keeps names
  added elsewhere since the draft was opened
- **Episode 2** came from comments: a pyramid you can climb (13 steps, about 10 m)
  and a spear rack for fishing in the shallows
- **A ship at 1,000 residents.** It can be boarded and steered, and it reaches a
  second island with a ruined house, a chest of clues and a stone circle
- **Residents have jobs:** fishing, cutting trees, building houses together and
  sitting at the campfire, with stuck detection so nobody walks in place
- Its own domain, `pulau-aru.web.id`, plus terms and privacy pages for the TikTok app

**Lesson:** tying the game state to one JSON file in the repo keeps it simple.
The game, the creator panel and the follower sync all read and write the same
file, and git history is the changelog.
