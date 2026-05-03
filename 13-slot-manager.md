# 12 · Letter outbox (admin only)

**Path:** `/admin/letters`
**Page type:** List + form
**Visibility:** Logged-in Admin
**Linked Airtable table:** SettlementLetters

---

## PROMPT

> Create an admin-only "Letter outbox" page at `/admin/letters` for the `taylored.HOME` portal.
>
> Damien (and only Damien) uses this to draft and send Settlement Letter 1, Letter 2, and any ad-hoc letters to owners. Replaces the manual Airtable CSV workflow he's been using.
>
> **Page header:**
> - Eyebrow: `ADMIN · LETTER OUTBOX`
> - Headline: `Letters to send.`
> - Right side: `+ New letter` button (opens form panel)
>
> **List (default view):**
> - Two tabs across the top: `Drafts` · `Sent`
> - Each row in Drafts:
>   - Letter title (e.g. "Settlement Letter 1 — Title insurance")
>   - Recipients (count, e.g. "12 owners")
>   - Last edited (mono date)
>   - Actions: `Edit` · `Preview` · `Send`
> - Each row in Sent:
>   - Letter title
>   - Sent date
>   - Recipients (count)
>   - Open rate (e.g. "8 of 12 opened")
>   - Action: `View`
>
> **+ New letter form (panel slides in from right):**
> - Letter title (text)
> - Recipients picker (multi-select from Owners; default = all current Owners with a Lot in active build)
> - Body (rich text editor; markdown OK)
> - Attachments (multi-file upload)
> - Schedule send (datetime picker; default = now)
> - Buttons: `Save as draft` · `Send now` · `Schedule`
>
> **Preview** (modal):
> Renders the letter in the same shell as the email templates Regina would receive. See `softr/copy/email-template-shell.md` for the exact wrapper.

---

## Manual setup

1. **Recipient picker:** Softr's Multi-select field bound to Owners. Filtered to `Lots.Status = "InBuild"`.
2. **Rich text body:** Softr's Rich Text field. Allow markdown headings, bullets, bold/italic, links.
3. **Send action:** Softr Form action triggers an Airtable automation that:
   - Renders the letter via the email template (Email 02 shape)
   - Sends to each recipient
   - Logs to SettlementLetters table with SentAt timestamp
   - Tracks open rate via pixel tracking (or simpler: a "Mark as read" link in the email body)
4. **Schedule send:** Stores the desired send time in `SettlementLetters.ScheduledFor`. An Airtable scheduled trigger fires at the right time.
5. **Visibility lock:** `Logged-in Admin` only. Owners attempting to load this URL → redirect to `/dashboard`.

---

## Acceptance check

- [ ] Page is invisible to logged-in Owners (404 or redirect)
- [ ] Damien can compose, save as draft, preview, and send
- [ ] Scheduling works (a letter scheduled for tomorrow doesn't send today)
- [ ] Sent letters show open rates after recipients click the tracking link
- [ ] Preview matches the email template shell exactly
