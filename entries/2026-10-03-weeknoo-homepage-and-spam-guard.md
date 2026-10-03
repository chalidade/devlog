# weeknoo: New Homepage, and Deleting a Gate That Protected Nothing

[weeknoo](https://chalidade.github.io/weeknoo/) is my website workspace: a prompt
on the homepage becomes a GitHub issue, and a Claude Code routine builds the
requested site, commits and closes the issue. Yesterday was cleanup and hardening.

- Removed three sites nobody used anymore (−20k lines) and moved the file tools
  into their own repo
- **Deleted the homepage's access-code screen.** The repo is public — anyone can
  open an issue directly — so a client-side gate added friction and zero security.
  The real checks stay in the pipeline: GitHub only applies the `prompt` label for
  collaborators, and the routine only runs issues that are labeled `prompt` *and*
  authored by me
- Added a GitHub Action that comments on, closes and locks any issue opened by
  someone other than the repo owner, plus `npm run guard -- on|off` to flip GitHub's
  temporary "collaborators only" interaction limit during a spam wave
- Redesigned the homepage: floating navbar, gradient-ring prompt box, gallery with
  mini browser previews, Geist + Instrument Serif, a proper weeknoo wordmark, and
  an Open Graph card so shared links render as an image

**Lesson:** a security control in client code of a public repo is decoration. Put
the check where the action actually happens — here, the runner.

**Next:** keep the runner's two checks in place whenever the routine is edited.
