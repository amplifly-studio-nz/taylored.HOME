# 06 · Document viewer

**Path:** `/documents/{record_id}`
**Page type:** Details
**Visibility:** Logged-in Owner
**Linked Airtable table:** Documents

---

## PROMPT

> Create a document viewer page at `/documents/{record_id}` for the `taylored.HOME` portal.
>
> **Top bar:** Back chevron labelled "Back to documents" linking to `/documents`. Right side has a `Download` button (downloads the file directly) and a `Mark as read` toggle (auto-marked on first view, but user can untoggle).
>
> **Layout — desktop:** Two columns, 70/30.
>
> *Left column (preview, 70%):*
> - PDF: inline PDF viewer (Softr's File Preview block, or `<iframe>` to the file URL).
> - Image: inline image, click-to-zoom.
> - Office docs: thumbnail + "Open in new tab" button.
> - Video: inline video player.
>
> *Right column (sidebar, 30%):*
> - Document title (Mansfield Bold 22px)
> - Category pill
> - Eyebrow `SHARED BY` + Damien's avatar + name + role
> - Eyebrow `DATE` + formatted date
> - Eyebrow `RELATED STEP` + linked step name (links to `/steps/{step_id}`)
> - Eyebrow `WHAT THIS IS` + plain-English description from `Documents.Description`
> - At the bottom: "Have a question about this document? Ask taylored. →" button linking to `/ask?doc={record_id}`.
>
> **Layout — mobile:** Single column. Preview on top (max height 60vh), sidebar info stacks below.

---

## Manual setup

1. **PDF preview** — Softr's File Preview block handles PDFs natively. For images, use the Image block with click-to-zoom enabled.
2. **Read tracking** — Auto-mark as read on page load via Softr's "On page load" automation, or via an Airtable webhook from a Custom Code block:
   ```html
   <script>
   fetch("/api/markRead", {method: "POST", body: JSON.stringify({docId: "{{Documents.RecordId}}"})});
   </script>
   ```
3. **Pre-fill Ask** — Same pattern as step detail: `/ask?doc={record_id}&context={DocumentTitle}`.

---

## Acceptance check

- [ ] PDFs render inline; user doesn't have to download to view
- [ ] Document is auto-marked as read on first view
- [ ] Related step link routes to the correct step detail
- [ ] Mobile layout stacks correctly with preview-on-top
