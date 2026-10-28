# VWO Job Fair: VIP Hiring Tools, a Coin Fee per Vacancy, Excel Import

Two days before the 30 October event, three pull requests went live on
[jobfair.co.id](https://jobfair.co.id) (86 files, +4,207 / −247 lines). All of
it is on the company side; job seekers still apply, enter and get seen for
free. Claude Code wrote the code and tests; I set the rules and checked every
screen before it shipped.

- **Each new vacancy now costs the company a fee in coins, set by the
  organiser.** The charge is written in the same database transaction as the
  vacancy, keyed by the vacancy's id, so a failed save never charges and a
  retry never charges twice
- The advanced hiring tools are now VIP-only. The candidate pool, offers,
  matches and webhooks are refused by the server for other stands, not just
  hidden in the UI. Basic applicant processing stays free for every stand
- Companies can import vacancies from an Excel template. The browser unzips
  the .xlsx with the built-in `DecompressionStream` and reads the sheet XML
  directly, so no spreadsheet library is added to the bundle
- Salaries became five ranges (under 3 million rupiah up to over 20 million)
  instead of free text, so pay reads the same way on every stand
- A "CCTV" view lets a company watch each floor live. It only reads the
  presence data already flowing to the floor and never announces itself or
  sends anything, so watchers add no traffic for the players
- The organiser, company and advertiser screens took the event's yellow and
  black brand, and stand logos now keep their own shape (square or wide)
  instead of being squeezed into one fixed box

**Lesson:** when you charge for an action, charge inside the same transaction
as the action and key the charge by what was bought. Then retries,
double-clicks and failed saves are all correct for free.

**Next:** run the full launch checklist on production before the doors open.
