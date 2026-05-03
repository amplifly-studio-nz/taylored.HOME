# 02 · Dashboard

**Path:** `/dashboard`
**Page type:** Custom (multiple blocks stacked)
**Visibility:** Logged-in Owner
**Linked Airtable tables:** Owners (current user's record), Lots, Steps, Documents, WalkthroughBookings, ConciergeMessages

---

## PROMPT

> Create a dashboard page at `/dashboard` for the `taylored.HOME` portal. The user is a logged-in homeowner viewing their own lot.
>
> The dashboard is **content-rich but calm**: one hero countdown card, a steps-timeline strip, four equally-sized panels in a 2×2 grid, then a recent updates list. No hover animations, no auto-rotating carousels.
>
> **Block 1 — Hero countdown card** (full width)
> Dark `#2B2B2B` background, `#FAF8F2` text. Padding 56px.
> Layout: left side has a citron eyebrow `SETTLEMENT · MONDAY 18 MAY 2026`, then a giant countdown like `28 DAYS · 14 HOURS` rendered in 96px Mansfield Bold; right side has the lot card showing "LOT 11 · 19 KNIGHTS RD · SEAVIEW RISE" and three icon-stat tiles (Bedrooms 4, Bathrooms 2.5, Carpark 2).
> The countdown is computed from `Lots.SettlementDate`. Use `softr/custom-code/countdown.html` as a Custom Code block.
>
> **Block 2 — Steps timeline strip**
> A horizontal pill timeline showing the 7 settlement steps, each in one of three states: done · in-progress · upcoming. Done = `#898F64` olive, in-progress = `#CEFF35` citron, upcoming = light grey. Reads from `Steps` table filtered by current Lot.
> Use `softr/custom-code/steps-timeline.html`.
>
> **Block 3 — 2×2 panel grid**
> Four equally-sized panels, white surface, 1px line border `#E5E1D7`, padding 32px:
>
> *Panel A — Steps to settlement.* Heading "What's next." Body lists the next two upcoming step names with their due dates. CTA: "See all steps →" links to `/steps`.
>
> *Panel B — Documents.* Heading "Latest documents." Lists the 3 most recent Documents records (filename, category, date). CTA: "Open documents →" links to `/documents`.
>
> *Panel C — Walkthrough.* If the current Lot's WalkthroughBooking is empty: "Booking opens 10 days before settlement." If a booking exists: "Walkthrough booked · {date} · {time}". CTA: "Manage booking →" links to `/walkthrough`.
>
> *Panel D — Ask taylored.* The concierge bubble teaser. Avatar (lowercase t with citron dot), one-line prompt "Ask taylored. anything about your home." Three example chips: "When is settlement?" / "What to bring on walkthrough day" / "Who is my lawyer?" Each chip → opens `/ask` with the question pre-filled.
>
> **Block 4 — Recent updates list** (full width, below the panels)
> Heading "Latest updates." Read from a unified feed: most recent Documents, recent step changes, recent ConciergeMessages from Damien. Each row: 14×14px coloured dot (citron for new docs, olive for step changes, sky for messages) · timestamp · plain-language description. 5 most recent rows.
>
> **Padding/spacing:** The whole dashboard sits inside a max-width 1280px container with 32px side margins.
>
> **Tone:** Direct, second-person, owner addressed by first name. No exclamation marks except in the welcome moment after settlement.

---

## Manual setup

1. **Hero countdown** — Custom Code block. Paste `softr/custom-code/countdown.html`. Edit the `data-settlement-date` attribute to point at a Softr **dynamic value** wired to `Lots.SettlementDate`. Pattern:
   ```html
   <div class="t-countdown" data-settlement-date="{{Lots.SettlementDate}}"></div>
   ```

2. **Steps timeline** — Custom Code block. Paste `softr/custom-code/steps-timeline.html`. Wire the `data-steps` attribute to a Softr List block underneath that's filtered to the current Lot's Steps.

3. **2×2 panel grid** — Use a four-column **List block** with the layout set to "Grid · 2 columns" and "Display: 4 items max". Each panel binds to a different Airtable view, but they share the same template:
   - Card heading (display font, 17px)
   - Body text (Inter 14px)
   - Bottom-right CTA pill linking to the relevant page

4. **Recent updates list** — Use a List block with layout "Compact list", 5 items max, sorted by `LastUpdated DESC`. Source: a Softr View that combines Documents + StepEvents + ConciergeMessages (or build a single "Updates" Airtable table that mirrors all three).

5. **Welcome banner above hero (after settlement)** — When `Lots.Status = "Settled"`, the dashboard hero is replaced by the celebration moment (see `prompts/02b-celebration.md`). Wire this with Softr's conditional visibility on the Lot status.

---

## Acceptance check

- [ ] Hero countdown shows real days/hours, not a static value
- [ ] Steps timeline reflects actual step states from Airtable
- [ ] All four panels link to their respective pages
- [ ] The Ask taylored. panel chips open `/ask` with the question pre-filled in the URL hash (e.g. `/ask#q=When+is+settlement?`)
- [ ] The recent updates list shows mixed content types with the right colour dots
- [ ] Mobile collapses 2×2 grid to single column, hero countdown shrinks to fit, timeline pills wrap or scroll horizontally
