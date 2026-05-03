# 07 · Walkthrough booking

**Path:** `/walkthrough`
**Page type:** Custom (calendar slot picker)
**Visibility:** Logged-in Owner
**Linked Airtable tables:** WalkthroughSlots, WalkthroughBookings, Lots, Owners

---

## PROMPT

> Create a "Walkthrough booking" page at `/walkthrough` for the `taylored.HOME` portal.
>
> Regina picks a 45-minute slot for her walkthrough with Damien and Simon. Booking opens 10 days before her settlement date.
>
> **Page header:**
> - Eyebrow: `WALKTHROUGH · LOT 11`
> - Headline: `Your final walkthrough.` (citron full-stop)
> - Sub: `Sat 16 – Mon 18 May. 45 minutes with Damien and Simon. Bring your questions.`
>
> **Layout (desktop):** Two columns, 60/40.
>
> *Left column — Slot picker:*
> - Day tabs across the top: `Sat 16 May` · `Sun 17 May` · `Mon 18 May`
> - Below tabs: a 5-column grid of slot pills showing all available slots for that day. Each pill: time range (e.g. `10:00 – 10:45`), conducted-by initials (e.g. `DT · ST`), and status (Available / Booked).
> - Available slots: white surface, ink text, citron border on hover.
> - Booked slots: light grey, struck-through, not clickable.
> - Selected slot: citron background, ink text.
> - Below the grid: a `Confirm booking →` button (disabled until a slot is selected).
>
> *Right column — Sidebar:*
> - Lot card: `LOT 11 · 19 KNIGHTS RD · SEAVIEW RISE` with thumbnail.
> - Eyebrow `WHAT TO EXPECT` + bullet list:
>   - 45 minutes onsite with Damien and Simon
>   - Bring any questions about the home
>   - Bring a phone or notepad
>   - Wear closed-toe shoes
> - Eyebrow `WHAT WE'LL COVER` + bullet list:
>   - Walkthrough of every room
>   - How appliances work
>   - Snag list (anything to fix before settlement)
>   - Q&amp;A
> - Eyebrow `CAN'T MAKE THESE TIMES?` + button: `Email Damien` (mailto link).
>
> **Empty state** (no slots available for the selected day):
> "No slots open on this day. Try the next day, or email Damien if these don't work."

---

## Manual setup

1. **Slot data source:** WalkthroughSlots Airtable table (see `airtable/schema.md`). Each row: SlotID, Date, StartTime, EndTime, Duration, ConductedBy (linked to People), Status (Available/Booked), BookedBy (linked to Owners), Lot (linked).

2. **Day tabs:** Use Softr's "Filter by user input" with a date field, displayed as segmented buttons. Filter the list block to `Date = selected_day`.

3. **Slot pill grid:** 5-column List block on the WalkthroughSlots filtered table. Card template:
   ```
   {StartTime, formatted "HH:MM"} – {EndTime, formatted "HH:MM"}
   {ConductedBy.Initials}
   ```
   Conditional formatting on the card based on Status: white if Available, grey-strikethrough if Booked, citron if BookedBy = current user.

4. **Confirm booking flow:**
   - On slot click → set "selected_slot" client-side state (Softr Custom Code with `localStorage`)
   - On `Confirm booking →` → triggers a Softr **Form action** that:
     1. Creates a WalkthroughBookings record (Owner, Slot, Lot, BookedAt)
     2. Updates WalkthroughSlots.Status = Booked, BookedBy = current user
     3. Sends confirmation email (Email 04 — see `softr/copy/email-04-booking-confirmed.md`)
     4. Redirects to `/walkthrough/booked` (the confirmed page) — see `prompts/08-walkthrough-confirmed.md`.

5. **Slot manager (admin)** — Damien adds slots from `/admin/slots` — see `prompts/13-slot-manager.md`.

---

## Acceptance check

- [ ] Day tabs filter the slot grid correctly
- [ ] Booked slots are visually distinct and not clickable
- [ ] Selected slot is highlighted citron
- [ ] Confirm button is disabled until a slot is selected
- [ ] On confirm, the WalkthroughBookings record is created and the slot is marked Booked atomically
- [ ] User is redirected to `/walkthrough/booked` after confirm
- [ ] Confirmation email lands within a minute
