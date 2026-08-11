# learn-be — public backend learning notes

## What this repo is

One file: `index.html`. It is a self-contained, publicly published page of my
backend-engineering notes. No build step, no dependencies, no CDN links — it must
keep working as a single file opened straight from disk or served statically
(GitHub Pages). **Never** split it into multiple files, add a framework, or add a
package.json unless I explicitly ask.

I am learning backend from a video course. As I go through it I come back here
and tell you what to write up — in short bursts, often weeks apart. When I say
things like "add a note on X", "add these notes", or paste rough notes from the
course, the job is to turn them into the note format below and insert them into
`index.html`.

**Write only what I give you.** Don't invent notes, don't pad a topic with
material I didn't mention, don't pre-emptively add "related" notes. If my input
is thin, expand it into clear prose and a fitting example — but stay on what I
actually said. If something I said looks wrong or incomplete, add the note as
asked and flag the concern to me separately.

## How to add a note

All content lives in the `NOTES` array inside the `<script>` tag in `index.html`.
Append the new object to that array. Everything below the
`RENDERING + SEARCH` comment is machinery — don't touch it unless a feature is
being added or fixed.

```js
{
  id:       "kebab-case-unique-id",   // becomes the #anchor URL — NEVER change it later
  title:    "Short name — the slightly longer, more specific part",
  category: "Databases",              // reuse an existing category name if one fits
  tags:     ["sql", "indexes"],       // lowercase, few, reused across notes
  body:     `<p>Plain-language explanation. HTML allowed.</p>`,
  highlight:`The one thing worth remembering.`,      // optional — omit if nothing earns it
  examples: [ { label:"SQL", code:`SELECT 1;` } ]    // optional — omit if none
}
```

### Rules for every note

1. **Title has two parts** — a short name, an em dash, then the specific bit.
   The point of the second half is that the title alone tells me what the note
   says. Good: `"Indexes — the reason one query takes 2ms and its twin takes 4 seconds"`.
   Bad: `"Indexes"`.
2. **Description in simple language.** Write like you're explaining to someone
   who has never built a backend. No jargon without defining it in the same
   sentence. Short paragraphs, `<ul>` lists where it helps. Explain *why* it
   exists, not just what it is.
3. **Include an example when one makes it concrete** — code, an HTTP exchange, a
   bad-vs-good comparison. Real and runnable-looking, not `foo`/`bar`. Escape
   nothing by hand; the renderer escapes code automatically. Avoid backticks
   inside `code` strings (they're JS template literals) — use a `<pre>`-free
   plain-text layout instead.
4. **`highlight` is for the gotcha** — the thing that bites people, the sentence
   worth remembering. It renders as a "Worth remembering" callout. Only add it
   when there genuinely is one. Not a summary of the note.
5. **Newest notes go at the bottom** of the array. Rendering groups by category
   and preserves array order within each category.
6. **Never change an existing `id`** — published links point at it. Titles and
   text can be edited freely.
7. **Categories grow organically.** The page started empty, so categories are
   whatever already exists in the `NOTES` array — read them off the file before
   adding. Reuse a fitting one rather than inventing a near-duplicate
   (no "Database" alongside "Databases"). Keep them broad; a category holding
   one note forever is a sign it should have been folded into another.
8. Keep the tone factual and personal-notes-like. No filler, no "In today's fast
   paced world", no emoji.

## Existing page features (don't break these)

- Live search over title, body, code, tags — with match highlighting; `/` focuses
  the box, `Esc` clears it.
- Category chips with live counts.
- Clickable `#tag` buttons that run a search for that tag.
- Sticky contents sidebar, per-note `#` anchor links.
- Light/dark theme following the OS, with a manual toggle stored in localStorage.
- Fully responsive; sidebar hides under 860px.
- Empty state: with zero notes the page hides the search box, chips and sidebar
  and shows a placeholder. That's handled automatically — nothing to do beyond
  adding the first note.

## After adding notes

- Sanity-check by opening `index.html` in a browser (`open index.html`) — a JS
  syntax error in the `NOTES` array blanks the whole page, so this matters.
- Don't commit or push unless I ask.
