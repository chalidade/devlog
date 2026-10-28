# A Copy With Nothing In It

A day of bug triage on the Lerero LMS at work. Most of it was finding out where
a bug actually lived, then sending it to whoever owns that part.

- **Duplicating a Portfolio made an empty copy.** The copy showed up in the
  course outline, but Edit opened with `edit=undefined` and a blank form. The
  front end was fine. The server's duplicate service takes the new record's
  `_id` from the activity provider's response, and the Portfolio provider
  returns `{ project, assignments }` instead. So `_id` was `undefined`, and the
  outline row was saved pointing at nothing. The check before saving was
  `if (newActivity)`, and an object without an id still passes it. I wrote up the
  one-line fix (unwrap `data.project`, and refuse to save when there is no id)
  and handed it to the backend team. A day earlier, a sibling activity type broke
  on the same duplicate path for a different reason: its endpoint was
  `'assignments'` with no leading slash, so the service called
  `http://host:PORTassignments/…` and got "Invalid URL".
- **A stray word on the Add Presentation page.** Support sent a screenshot of
  the word `loadFile` sitting under the course title. It was a bare identifier
  left between two JSX blocks, which React prints as text, and it had been there
  since April. I deleted the line. Then I scanned every `.tsx` file for a lone
  camelCase word between JSX blocks, to answer "is it anywhere else?". It
  wasn't.
- **Checking a fix was live without the right account.** A ticket asked for a
  Retake button that a colleague's change had already added. I couldn't sign in
  as the learner, so I fetched the deployed page's JavaScript chunk and matched
  the minified condition: the new rule was there and the old one was gone. The
  ticket says plainly that the button itself hasn't been seen on screen yet.
- **A retest that failed for another reason.** QA reopened a SCORM ticket
  because the id in the page address and the id sent on upload looked swapped.
  They are different ids on purpose: one belongs to the package record, the
  other to the course activity.
  The real blocker was the SCORM Cloud account sitting at its 3-course limit. I
  sent it back with two plain questions: which test package can be deleted, and
  what learners who already started should get.
- **Outside work:** a Vercel Pro upgrade quote listed two members, with $20 a month for the second one.
  The second "member" was a pending access request created by a GitHub commit
  from my other account. Declining it left me as the only member.

**Lesson:** a duplicate that fails loudly is better than one that "succeeds"
with nothing inside. The truthy check let an empty copy through. The guard that
would have caught it checks for the field you actually use, here `_id`.

**Next:** retest the Portfolio duplicate once the backend fix is out, and
reproduce the outline not refreshing after a duplicate. I couldn't explain that
one from the code.
