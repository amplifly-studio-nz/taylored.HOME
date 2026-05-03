# 11 · Profile

**Path:** `/profile`
**Page type:** Form (edit current user's record)
**Visibility:** Logged-in Owner
**Linked Airtable table:** Owners (current user's record)

---

## PROMPT

> Create a "Profile" page at `/profile` for the `taylored.HOME` portal.
>
> Lightweight settings — the user only needs to change a few things, and most of the lot info is read-only.
>
> **Page header:**
> - Eyebrow: `YOUR ACCOUNT`
> - Headline: `Profile.` (citron full-stop)
>
> **Section 1 — Your details (editable form):**
> - Avatar (upload, max 1MB)
> - First name (text, required)
> - Last name (text, required)
> - Email (read-only — to change, contact Damien)
> - Phone (text, optional)
> - Preferred contact method (radio: Email · Phone · Text)
>
> Save button: `Save changes` — citron primary.
>
> **Section 2 — Notifications:**
> - Toggle: `Email me when a new document is shared` (default ON)
> - Toggle: `Email me when a step changes status` (default ON)
> - Toggle: `Email me when Damien sends a message` (default ON)
> - Toggle: `Send me a daily summary` (default OFF)
>
> **Section 3 — Your home (read-only card):**
> - Lot number (e.g. `Lot 11`)
> - Address (`19 Knights Rd, Seaview Rise`)
> - Settlement date
> - Linked owners (if multiple)
> - To change anything here: "Email Damien" link.
>
> **Section 4 — Sign out:**
> Plain text link, bottom of page: `Sign out`. On click: signs out and redirects to `/`.

---

## Manual setup

1. **Form binding:** Softr Form block in "Update record" mode, bound to current user's Owners record.
2. **Email read-only:** Set the email field's `Disabled` property = true, with help text: "Email Damien to change the email on your account."
3. **Avatar upload:** Use Softr's File Upload field, max 1MB, single image.
4. **Notification toggles:** Stored on the Owners record as boolean fields. Trigger the actual emails via Airtable automations that read these flags.
5. **Sign-out:** Standard Softr Logout action.

---

## Acceptance check

- [ ] Saving updates the Airtable Owners record correctly
- [ ] Email field is visibly disabled with the help text shown
- [ ] Avatar upload works and shows the new image after save
- [ ] Toggling a notification preference disables the corresponding email automation
- [ ] Sign out works and lands the user on `/`
