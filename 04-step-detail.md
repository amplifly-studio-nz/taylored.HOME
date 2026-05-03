# 03 · Steps to settlement

**Path:** `/steps`
**Page type:** List (vertical timeline)
**Visibility:** Logged-in Owner
**Linked Airtable table:** Steps (filtered by Owner = current user, sorted by StepOrder ASC)

---

## PROMPT

> Create a "Steps to settlement" page at `/steps`. It is a vertical timeline of seven labelled steps. The current step is highlighted; completed steps are subdued; upcoming steps are even lighter.
>
> **Page header (above the list):**
> - Eyebrow: `YOUR PATH TO SETTLEMENT · LOT 11`
> - Headline: `Seven steps. We'll walk you through.` (`Seven steps` in The Seasons script, citron full-stops)
> - Sub: `Tap any step to see what's involved, who's responsible, and what's expected of you.`
>
> **List block** — vertical, full-width within a max-width 1080px container.
>
> Each step row is a card with:
> - **Left column (96px wide):** A large numeric badge (1–7) using the assets in `softr/assets/brand/numbers/` (PNG, citron circle behind ink digit). For done steps, the badge desaturates; for upcoming steps, it's outlined only.
> - **Middle column (flex):** Step title (Mansfield Bold 22px), one-line plain-English description, due date pill, and a "STATUS" pill: `Done` (olive), `In progress` (citron), `Upcoming` (light grey).
> - **Right column:** Disclosure caret. Clicking the row reveals the step detail panel inline (no page change).
>
> **The 7 steps (from Airtable Steps table):**
> 1. Welcome &amp; agreement
> 2. Settlement Letter 1 — title insurance
> 3. Walkthrough booking opens
> 4. Walkthrough day
> 5. 10-day call &amp; titles in
> 6. Settlement Letter 2 &amp; final invoice
> 7. Settlement day
>
> **Inline detail panel** (revealed on row click):
> - 3-column grid: `What's involved`, `Who's responsible`, `What we need from you`
> - Each column header in citron mono caps, body 14px
> - At the bottom: any related documents (linked from `Steps.RelatedDocuments`) as small chips, and a "Have a question? Ask taylored." button → opens `/ask` with the step pre-filled as context.
>
> **Sticky right rail (desktop only):** A mini contact card with Damien's photo, name, role, and a `Call · Text · Email` row. Sits at top-right and stays visible as the user scrolls the timeline.

---

## Manual setup

1. **Number badges** — Softr Image field on Steps table. Add a `BadgeImage` field that is a single attachment, then upload `softr/assets/brand/numbers/01.png` through `07.png` to each step row. (Or use a formula field that returns `{StepOrder}.png` and a Softr lookup that joins to a "BadgeAssets" table.)

2. **Status pill colours** — Conditional formatting in the List block, based on `Steps.Status`:
   - `Done` → olive `#898F64`
   - `In Progress` → citron `#CEFF35`, dark text
   - `Upcoming` → light grey `#E5E1D7`, ink text

3. **Inline expansion** — Softr's List block doesn't natively expand-in-place. Two options:
   - **Easier**: Make each row link to `/steps/{record_id}` (Step detail page) — see `prompts/04-step-detail.md`.
   - **Custom**: Use a Custom Code block with the steps data wired in via Softr dynamic tags. Snippet skeleton in `softr/custom-code/steps-expandable.html` (optional; build only if the link-out flow feels too heavy).

4. **Sticky contact card** — Position-relative wrapper. Use a 2-column List block with the right column being a "single-record details" pull from `Owners.AssignedDamien` lookup. Set the right column to `position: sticky` via Custom Code block for the column.

---

## Acceptance check

- [ ] All 7 steps render in the right order with the correct number badges
- [ ] The current step (StepOrder = currentStep) is visibly highlighted (citron pill)
- [ ] Tapping a step either expands inline or routes to the step detail page
- [ ] The right-rail Damien card is sticky and links call, sms, mailto correctly
- [ ] On mobile, the right rail stacks below the list (not floating)
