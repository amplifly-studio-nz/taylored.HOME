# 08 · Walkthrough confirmed

**Path:** `/walkthrough/booked` (or `/walkthrough` after a booking exists for the current user — same page, conditional)
**Page type:** Details (single record from WalkthroughBookings)
**Visibility:** Logged-in Owner
**Linked Airtable table:** WalkthroughBookings (filtered to current user)

---

## PROMPT

> Create a "Walkthrough confirmed" view at `/walkthrough/booked` for the `taylored.HOME` portal.
>
> Shown after Regina confirms a slot, OR shown at `/walkthrough` if a booking already exists for the current user.
>
> **Hero card** (citron background, full width):
> - Citron tick icon top-left
> - Headline: `You're booked in.` (in script + Mansfield mix, ink text)
> - Subhead: `{BookingDay, e.g. "Sunday"} {BookingDate, e.g. "17 May 2026"} · {StartTime}–{EndTime}`
> - Quick actions row:
>   - `Add to calendar` (downloads .ics)
>   - `Get directions` (opens Google Maps to lot address)
>   - `Reschedule` (opens slot picker again, marks current slot Available)
>   - `Cancel` (with confirm dialog; marks slot Available, deletes booking)
>
> **Below the hero, two columns:**
>
> *Column 1 — What we'll cover.* Bullet list (same content as the booking page sidebar's "What we'll cover").
>
> *Column 2 — Who you'll meet.* Avatar + name + role + Call/Text/Email row for each:
> - Damien Taylor — Founder, Taylored Group
> - Simon Tate — Site manager
>
> **Below the columns: Map preview** (a static image of the lot location, with a "Get directions" overlay button).

---

## Manual setup

1. **Conditional `/walkthrough` page**: In Softr, set up `/walkthrough` to show the booking flow if `WalkthroughBookings filtered to current user` is empty, else show this confirmed view. Use Softr's "Conditional page content" or two separate pages with a redirect rule.

2. **Add to calendar** — Generate an .ics file. Use a Custom Code block:
   ```html
   <a href="data:text/calendar;charset=utf8,..." download="walkthrough.ics" class="btn btn-secondary">Add to calendar</a>
   ```
   Inject the booking details via Softr dynamic tags.

3. **Reschedule** — Link to `/walkthrough?reschedule=true`. The slot picker page reads this param, marks the current booking's slot as "available again pending change", and on new confirm, atomically swaps slots.

4. **Map** — Use a Static Map API (Mapbox or Google) with the lot's coordinates from `Lots.LatLng`. Overlay a citron pin SVG.

---

## Acceptance check

- [ ] If a booking exists, going to `/walkthrough` shows the confirmed view (not the picker)
- [ ] Add to calendar downloads a working .ics
- [ ] Reschedule and cancel work and update the slots table atomically
- [ ] Map shows the right lot location with a custom pin
