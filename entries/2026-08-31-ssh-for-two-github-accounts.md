# Two GitHub Accounts on One Laptop: SSH Instead of Switching

My first push to weeknoo was rejected. The cause was how `gh` handles accounts,
and the fix was one remote URL.

- `gh` has one active account for the whole machine, and Git over HTTPS asks
  `gh` for credentials. The active account was my work one, so the push to my
  personal repo went out with the wrong token
- Switching the active account only moves the problem: the work repos on the
  same laptop need the work account
- I moved weeknoo's remote to SSH (`git@github.com:chalidade/weeknoo.git`). With
  SSH the identity belongs to the key, so `gh`'s switch doesn't matter. The
  weeknoo push went through, and the work repos still worked, without
  switching anything
- The reason is written down in the repo docs, so nobody switches it back to
  HTTPS later

**Lesson:** when two accounts fight over one global setting, take one of them
off that setting entirely. Here that meant moving the personal repo to SSH.
