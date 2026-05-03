# 00 · App setup — brand, navigation, auth

**Paste-target:** Softr AI Co-Builder (initial prompt — generates the app shell before any pages)
**Visibility:** N/A (sets app-level config)
**Data source:** None for shell; wire Airtable in pages.

---

## PROMPT

> Create a new Softr app called **`taylored.HOME`**. It is a private owner portal for buyers of new-build homes by Taylored Group.
>
> **Brand:**
> - Primary text colour: `#2B2B2B` (deep ink)
> - Background: `#F0EEE9` (warm cream)
> - Surface (cards): `#FFFFFF` (paper)
> - Accent / success / "go": `#CEFF35` (citron yellow-green)
> - Secondary accent: `#A6CFE0` (sky blue)
> - Tertiary accent: `#898F64` (olive)
> - Warning: `#E0A85B` (warm amber)
> - Danger: `#C84A3F` (clay red)
>
> **Typography:**
> - Display headings: **Mansfield Bold** (Google Fonts, fallback to `Inter Black`)
> - Body: **Inter** (regular 400, medium 500, semibold 600)
> - Mono / labels / eyebrows: **Anonymous Pro** (Google Fonts), uppercase, letter-spacing 0.18em
> - Display script accent: **The Seasons Light** (custom upload — see app footer custom code)
>
> **Tone of voice:** Plain English, warm, no construction jargon. Always end the wordmark `taylored.` with a citron full-stop. Address the user by first name. Speak as Damien would.
>
> **Navigation (logged-in owner):**
> - Sidebar (desktop) with these items, in this order: Dashboard · Steps to settlement · Documents · Walkthrough · Contact · Ask taylored. · Profile
> - Bottom tab bar (mobile, ≤768px) with Dashboard, Steps, Documents, Walkthrough, Contact (5 tabs)
> - Top bar (mobile) with the wordmark `taylored.HOME` left, lot identifier right ("LOT 11 · SEAVIEW RISE")
>
> **Authentication:** Email magic-link sign-in only. No passwords. Each user is linked to one or more Airtable Owners records. Logged-in owners see only their own lot's data.
>
> **Roles:**
> - `Logged-in Owner` — sees Dashboard, Steps, Documents, Walkthrough, Contact, Ask, Profile
> - `Logged-in Admin` — additionally sees Letter outbox, Slot manager
> - `Public` — sees only Sign in
>
> **Footer:** Plain text, two lines:
> Line 1: `taylored.HOME · Built by Taylored Group · Auckland, NZ`
> Line 2: `Need help? Email damien@taylored.co.nz · Call +64 21 333 3334`

---

## After Co-Builder generates: do this manually

### 1. Add the citron dot to the wordmark
The wordmark `taylored.HOME` has two citron full-stops — after `taylored` and after `HOME`. Softr's Header block uses a single text field, so do this:

**Option A (text only, fastest):**
- App settings → Branding → Logo → Text mode
- Logo text: `taylored.HOME`
- Logo subtitle: leave blank
- Then in App settings → Custom code → Header, paste `_shared.css` from `softr/custom-code/` — it includes `.app-logo` styling that colours the dots.

**Option B (custom SVG, prettiest):**
- Upload `softr/assets/brand/logo-wordmark.svg` to Files
- App settings → Branding → Logo → Image mode → select that file

### 2. Upload The Seasons Script font
- App settings → Custom code → Header
- Paste:
```html
<style>
@font-face {
  font-family: "The Seasons";
  src: url("https://YOUR-SOFTR-FILES-URL/TheSeasons-Light.otf") format("opentype");
  font-weight: 300;
  font-display: swap;
}
.script { font-family: "The Seasons", serif; font-weight: 300; letter-spacing: 0; }
</style>
```
- (Replace the URL with the actual file URL after upload.)

### 3. Paste the brand variables
Same custom code block, append the contents of `softr/custom-code/_shared.css`. This makes brand variables (`--t-citron`, `--t-ink`, `--t-paper` etc.) available to every Custom Code block in the app.

### 4. Configure the email-link sign-in
- App settings → Authentication → Magic link → On
- Sender name: `Damien from taylored.HOME`
- Sender email: `damien@taylored.co.nz`
- Email subject: `Your taylored.HOME sign-in link`
- Email body: see `softr/copy/01-signin.md` (magic-link email body)

### 5. Bottom tab bar (mobile)
Softr doesn't ship a bottom tab bar by default. Either:
- Use a Navigation block set to "stick to bottom on mobile" with five items
- Or paste `softr/custom-code/mobile-tabbar.html` into App settings → Custom code → Footer (it will only render at &lt;768px)

---

## Acceptance check — when this step is done

- [ ] Brand colours visible in App settings → Branding (matches palette.csv)
- [ ] Sign-in page exists and uses magic-link auth
- [ ] Sidebar shows the 7 owner items in the right order
- [ ] Mobile tab bar shows the 5 items at &lt;768px
- [ ] Footer reads correctly with damien@taylored.co.nz and the phone number
- [ ] The wordmark renders as `taylored.HOME` with two citron full-stops
