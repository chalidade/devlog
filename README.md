# Devlog

The public engineering log of [Chalid Ade Rahman](https://github.com/chalidade), Senior Frontend
Engineer (React · Next.js · TypeScript, 8+ years).

My day job lives in private repositories, so this is the public record of what I build and fix
on my own projects. Each entry covers what shipped, the decisions behind it, and one lesson.
Measured numbers are labelled as measured, simulated or local.

**Read it as a site:** [chalidade.github.io/log](https://chalidade.github.io/log/), or browse
[`entries/`](entries/) and [`notes/`](notes/) here.

## Projects covered

| Project | What it is | Links |
| --- | --- | --- |
| **VWO** | A virtual job fair you walk through as a character, with a coin ledger, realtime floors and a company portal | [Demo](https://chalidade.github.io/vwo/) · [Source](https://github.com/chalidade/vwo) |
| **tools** | My everyday file toolbox, free for everyone: 38 tools that run entirely in the browser | [Live](https://chalidade.github.io/tools/) · [Source](https://github.com/chalidade/tools) |
| **Kita Berkembang** | A store builder for Indonesian small businesses on WordPress Multisite | [Live](https://kitaberkembang.com) |
| **weeknoo** | Prompt → GitHub issue → site, Android APK or WordPress block theme | [Live](https://chalidade.github.io/weeknoo/) · [Source](https://github.com/chalidade/weeknoo) |
| **Laravel course site** | Maintenance work on a client's site: auto-deploy, a security pass, a view-only redesign | — |
| **Portfolio** | [chalidade.github.io](https://chalidade.github.io), including the page that renders this repo | [Source](https://github.com/chalidade/chalidade.github.io) |

## Notes

Longer write-ups on a single problem:

- [Time-stretching audio in the browser](notes/time-stretching-audio-in-the-browser.md): streamed WSOLA, so speed changes keep the pitch
- [Rebuilding tables from PDF text](notes/rebuilding-tables-from-pdf-text.md): turning positioned text runs back into rows and columns
- [Paginating a .docx in the browser without cutting lines](notes/paginating-docx-in-the-browser.md)
- [Proving a redesign changed no forms](notes/proving-a-redesign-changed-no-forms.md): a per-page form signature, diffed before and after
- [Next.js 16 upgrade plan](notes/nextjs-16-upgrade-plan.md): written for RuangKelasku, a project since retired

## Format

- `entries/YYYY-MM-DD-slug.md`: one piece of work, usually a short context paragraph, the changes
  as bullets, then **Lesson** and often **Next**.
- `notes/slug.md`: one problem in depth, covering the approach, gotchas and when to use it.

## How it's written

I build with Claude Code, and entries are drafted from my commits and notes, then reviewed and
edited by me before they're published. The rules:

- Only work that actually happened, with numbers I can point to.
- No details of my employer's or clients' private systems.
- Security issues are written up only after they're fixed.

Started August 2026.
