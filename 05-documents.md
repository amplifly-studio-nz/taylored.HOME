# 04 · Step detail

**Path:** `/steps/{record_id}`
**Page type:** Details
**Visibility:** Logged-in Owner
**Linked Airtable table:** Steps

---

## PROMPT

> Create a step detail page at `/steps/{record_id}` for the `taylored.HOME` portal.
>
> **Top bar:** Back chevron labelled "Back to all steps" linking to `/steps`.
>
> **Hero (full-width, ink background):**
> - Eyebrow: `STEP {StepOrder} OF 7 · {StepCategory}`
> - Headline: `{StepTitle}` in Mansfield Bold 56px, citron full-stop appended
> - Status pill (top-right): Done · In progress · Upcoming
> - Due date subhead: `Due {StepDueDate, formatted "Mon 4 May 2026"}`
>
> **Body — three-column grid (collapses to single column on mobile):**
>
> *Column 1 — What's involved.*
> Reads from `Steps.Description` (long text, may include markdown-style bullets).
>
> *Column 2 — Who's responsible.*
> Reads from `Steps.Responsible` (linked to People table). Shows avatar, name, role for each, with `Call · Text · Email` quick-action row beneath.
>
> *Column 3 — What we need from you.*
> Reads from `Steps.OwnerActions` (long text). If empty, show: "Nothing right now — we'll let you know."
>
> **Related documents block** (full width, below the columns):
> Heading "Documents for this step." A horizontal scroll of document cards from `Steps.RelatedDocuments`. Each card: file icon, name, date. Tap → open `/documents/{record_id}`.
>
> **Bottom CTA** (full width, citron background):
> "Got a question about this step?" + button "Ask taylored. →" linking to `/ask?step={StepOrder}`.

---

## Manual setup

1. **Linked record fields:** Set up `Steps.Responsible` as a multi-link to a `People` Airtable table. Softr Details blocks can pull and render linked records with avatar.
2. **Markdown in `Steps.Description`** — Softr renders Airtable Long Text as plaintext by default. Switch the field type to "Rich text" in Airtable, or use Softr's Markdown rendering toggle on the Details block.
3. **Step pre-fill on Ask** — Build the CTA button as a link with format:
   ```
   /ask?step={{StepOrder}}&context={{StepTitle}}
   ```
   The Ask page reads these query params and pre-fills the chat input.

---

## Acceptance check

- [ ] Hero shows the right step number and title from the URL's record_id
- [ ] All three body columns render their respective fields
- [ ] Empty `OwnerActions` shows the fallback copy, not a blank column
- [ ] Related documents tap-through opens the document viewer for the correct file
- [ ] Ask button URL includes the step number and title as query params
