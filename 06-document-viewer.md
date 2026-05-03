# 05 · Documents

**Path:** `/documents`
**Page type:** List (with category tabs)
**Visibility:** Logged-in Owner
**Linked Airtable table:** Documents (filtered by Owner = current user)

---

## PROMPT

> Create a "Documents" page at `/documents` for the `taylored.HOME` portal.
>
> **Page header:**
> - Eyebrow: `EVERYTHING DAMIEN &amp; SIMON SHARE`
> - Headline: `Your documents.` (citron full-stop)
> - Sub: `Settlement letters, plans, legal — all in one place.`
>
> **Tabs (segmented control across the top):**
> Categories from `Documents.Category`:
> - All · Settlement · Legal · Construction · Insurance · Other
>
> Default tab: All.
>
> **List below the tabs:** Grouped by month, sorted newest first within each group.
>
> Each row is a card with:
> - **File-type icon** (left, 40×40px) — PDF, image, doc, video. Citron circle background for unread, neutral grey for read.
> - **Filename** (Mansfield Bold 16px)
> - **Category pill** (sky, olive, citron, etc. depending on category)
> - **Date** (subdued mono, right-aligned)
> - **Read indicator** (citron dot if unread)
> - On click: opens `/documents/{record_id}` (the document viewer).
>
> **Empty state** (when filtered tab has no records):
> "Nothing here yet. New documents land here as Damien shares them."

---

## Manual setup

1. **Tabs as Softr filters:** Use the List block's "Filter by user input" feature with `Documents.Category` as the filter field. Display as segmented control.
2. **Read tracking:** Add a join table `DocumentReads(Owner, Document, ReadAt)`. When the user opens `/documents/{record_id}`, an Airtable automation creates a DocumentReads row. The unread indicator is a formula on Documents: `IF(NOT(FIND(CURRENT_USER_EMAIL, ReadByEmails)), TRUE, FALSE)`. Wire this to the citron dot's conditional visibility.
3. **File-type icon:** Use a formula field on Documents: `IF({FileType}="pdf", "📄", IF({FileType}="image", "🖼️", "📎"))` — but **prefer SVG icons** from `softr/assets/brand/icons/` over emojis. Wire via a lookup to a `FileTypeIcons` Airtable table.

---

## Acceptance check

- [ ] All categories render as tabs in the right order
- [ ] Tab switching filters the list without page reload
- [ ] Unread indicator works (citron dot disappears after first open)
- [ ] List groups by month with month headers ("MAY 2026", "APRIL 2026")
- [ ] Tapping a row opens the viewer page
- [ ] Empty state shows the correct copy, not "no records found"
