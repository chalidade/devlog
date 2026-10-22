# weeknoo: Bubur Bara, Breakfast Porridge to Order

Another [weeknoo](https://chalidade.github.io/weeknoo/) site, this one shaped like
an app: ordering for Bubur Bara, grilled claypot rice porridge sold as breakfast.

- Menu (porridge, wonton, toppings, drinks) and a cart
- Two ways to order: pick up today as soon as possible, or schedule a pickup date
  and time. A scheduled order closes at 17.00 the day before, and the cart says
  which is the earliest date still open
- Pay by QRIS and upload the transfer proof, then the order goes out as a
  prefilled WhatsApp message
- Receipts and order history are kept in IndexedDB through the workspace's Dexie
  library, so they stay on the buyer's phone
- Sections on the outlet concept and locations, plus a partnership section that
  simulates profit sharing for a passive partner: the central team runs the
  outlet and the partner watches the numbers
- New card on the homepage

**Lesson:** a cut-off rule needs to explain itself. Telling the buyer the earliest
date they can still get is more useful than just refusing a date that is too
soon.
