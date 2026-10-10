# VWO Job Fair: One Coin Wallet for Every Company Purchase

[jobfair.co.id](https://jobfair.co.id) is the live version of my virtual job fair.
Today companies stopped paying per purchase in rupiah and moved to one coin wallet,
and the company and organiser pages got a proper dashboard (PR #75). Claude Code
wrote the code; I set the payment rules, reviewed the screens and asked for the
changes.

- **Every company purchase is paid in coins**: the stand registration, the VIP
  upgrade, the promoter, stand accessories and food court stalls. Prices stay in
  the organiser's rupiah table and convert at one rate they control (default
  Rp200 per coin), so changing the coin value is one field, not forty prices
- Companies top up with four business packs (5,000 to 86,000 coins, bonus on the
  bigger ones) through Xendit, from the portal, the stall rental and the
  registration page. One checkout covers many small purchases
- The server recomputes every coin price, spends with an idempotency key, then
  delivers the purchase; if delivery fails the coins are refunded and the payment
  is marked refunded. Tested locally against a fake Xendit: a short balance is
  refused with the exact shortfall, a top-up is credited, and paying the same
  bill twice is refused
- A shared dashboard frame for the company portal and the organiser pages:
  sections grouped in a sidebar (Recruitment, Stand, Money), which turns into a
  scrolling strip on phones, and a top bar with the balance and main actions
- The in-game top bar now has two pills of the same height instead of three loose
  buttons

**Lesson:** a payment gateway per small purchase is the wrong unit for a business
customer. Selling credit once and spending it internally makes every later sale
a database transaction I can test, and keeps the gateway at the edge.

**Next:** switch Xendit to the production key and open the site for registrations.
