# A Truthy Check Is Not a Guard

Three bugs from one week of triage had the same shape: something checked that a
value existed, the value existed, and it was the wrong value. Nothing crashed,
so nothing was reported until a person looked at the screen.

## The approach

**Check the field you are about to use, not the object around it.** A
"duplicate" feature copied a record by calling a service and saving the new
`_id` it returned:

```ts
const created = await provider.duplicate(source)
if (created) {                       // passes for { project, items } too
  await outline.add({ ref: created._id })   // ref: undefined
}
```

One provider wrapped its record (`{ project, items }`), so `created._id` was
`undefined`. The check passed, the outline row was saved pointing at nothing,
and the copy opened as an empty form. The guard that would have caught it:

```ts
const id = created?._id ?? created?.project?._id
if (!id) throw new Error(`duplicate returned no id: ${Object.keys(created ?? {})}`)
```

A duplicate that fails loudly is better than one that "succeeds" with nothing
inside.

**A placeholder needs to say it is fake, or it ships.** In the same week:

- a pop-up read a `rating` field no cart item carries, then fell back to a
  hard-coded `'4.8'`, so every product looked rated 4.8
- a pagination label had room for one number and printed "Showing 10 of 433"
  on page 2, where it meant "10–18"

Both were written as stand-ins while a feature was being built. Neither had a
comment, a `TODO` or a test that would fail, so they outlived the feature. The
fix for the rating was to pass the real average and show no star when there
isn't one. A missing value displayed as nothing is honest; a missing value
displayed as a plausible number is a lie the user believes.

## Gotchas

- `'assignments'` joined to a base URL without a leading slash produced
  `http://host:PORTassignments/…`. `new URL(path, base)` would have thrown
  "Invalid URL" at the line that built it, instead of at the request.
- A bare identifier left between two JSX blocks (`loadFile`) is valid JSX and
  renders as text. It sat on a page for months. A quick scan for a lone
  camelCase word between closing and opening tags answered "is it anywhere
  else?" in seconds.

## When to use it

Any time a value crosses a boundary you don't own (another service, another
team's response shape, a form field that can be empty), validate the exact
field you consume. Inside one module with typed data, a truthy check is fine;
at the edges it hides the bug until a user finds it.
