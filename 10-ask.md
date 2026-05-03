# 09 · Contact

**Path:** `/contact`
**Page type:** List (people cards) + form
**Visibility:** Logged-in Owner
**Linked Airtable tables:** People, Owners.AssignedTeam

---

## PROMPT

> Create a "Contact" page at `/contact` for the `taylored.HOME` portal.
>
> The opposite of a help-desk ticket form — this page surfaces real people with real numbers.
>
> **Page header:**
> - Eyebrow: `YOUR TEAM`
> - Headline: `Talk to a real person.` (script accent on "real")
> - Sub: `These are the people building your home. Call any of them. We don't have a ticket system.`
>
> **People cards — 3-column grid:**
>
> Each card:
> - Avatar (large, 96×96px)
> - Name (Mansfield Bold 22px)
> - Role (eyebrow mono)
> - One-paragraph bio
> - Action row: `Call · Text · Email` (each with the actual phone/email; tap-through directly)
> - For Damien specifically: also a `Book a 15-min call` button → opens a Calendly-style scheduler (or Softr Form that emails Damien).
>
> **The three people:**
> - **Damien Taylor** — Founder, Taylored Group. Your main contact.
> - **Simon Tate** — Site manager. Day-to-day on the build.
> - **Tom Goldsworthy** — Lawyer (Buddle Findlay). For settlement &amp; legal questions.
>
> **Below the cards: Quick message form.**
> Heading: `Or send a message.`
> Sub: `Goes to Damien. He'll forward it if it's better answered by Simon or Tom.`
> Fields:
> - Name (pre-filled with current user's name, read-only)
> - Email (pre-filled, read-only)
> - Subject (text)
> - Message (textarea, 6 rows)
> - Submit button: `Send message`
>
> Form submission → creates a row in `Messages` Airtable table, sends Damien an email notification.

---

## Manual setup

1. **People data:** People Airtable table with columns: Name, Role, Bio, Avatar (attachment), Phone, Email, IsAssignedTo (linked to Owners).
2. **Filter to assigned team:** The 3-column grid pulls from `People` filtered to `IsAssignedTo includes current user`. For M1, hard-code the three people; later, the assignment can vary by lot.
3. **Tap-through actions:**
   - Call: `<a href="tel:{Phone}">`
   - Text: `<a href="sms:{Phone}">`
   - Email: `<a href="mailto:{Email}">`
4. **Book a 15-min call** — Softr supports Calendly embeds; or build a Form that creates a Meeting record and emails Damien.
5. **Message form** — Softr Form block, action: Create record in Messages, then trigger Airtable automation that emails Damien.

---

## Acceptance check

- [ ] All 3 people render with correct avatars and bios
- [ ] Call/Text/Email buttons trigger the right native handlers on phone
- [ ] Damien's "Book a 15-min call" routes to a working scheduler
- [ ] Message form creates an Airtable row and emails Damien
- [ ] On mobile, cards stack to single column
