# QA Report: Tickets by Feature and Done per Day

Two additions to the internal QA report page in the LMS, the one QA uses to see
every open Jira ticket across projects. Both shipped the same day.

- **Group the list by feature.** A ticket's feature is its top-level epic:
  subtask, then story, then epic. The open list often holds a subtask whose
  story is already Done, so the parent is not in the data. The API route walks
  up one level per round and fetches only the missing parents by key, until
  every ticket reaches an epic or a ticket with no parent. A parent Jira will
  not return (no permission) is treated as a root, so the loop always ends. A
  ticket with no parent counts as a feature only when something hangs under it.
- **Tickets moved to Done per day, last 14 days.** The tab never loads Done
  tickets, so the count comes from status history instead: one count query per
  day, all run in parallel,

  ```
  status CHANGED TO Done DURING (startOfDay(-n), endOfDay(-n))
  ```

  `startOfDay(-n)` resolves in the Jira account's own timezone, so the day
  boundaries match what people see in Jira. The days are capped at 30.

**Lesson:** "which feature is this ticket in" sounds like a field lookup, but
it's a tree walk over data you only partly have. Fetching the missing parents
one level at a time keeps it to a few rounds of requests instead of one per
ticket.
