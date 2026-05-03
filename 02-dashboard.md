# 01 · Sign in

**Path:** `/` (root)
**Page type:** Custom (Auth block + brand panel)
**Visibility:** Public
**Data source:** N/A — uses Softr's magic-link auth
**Linked Airtable table:** Users / Owners

---

## PROMPT

> Create a sign-in page at `/` for the `taylored.HOME` portal.
>
> **Layout — desktop:** Two columns, 50/50. Left column: a full-bleed image (use `assets/brand/seaview-rise.png`). Right column: a centred white card with the sign-in form, max-width 480px, padding 64px.
>
> **Right column content, top to bottom:**
> 1. **Wordmark**, large: `taylored.HOME` — both `taylored` and `HOME` end with citron full-stops (`#CEFF35`). 36px Mansfield Bold.
> 2. **Eyebrow**, mono small caps: `OWNER PORTAL · LOT 11 · SEAVIEW RISE`
> 3. **Headline:** `Welcome home, Regina.` — 32px Mansfield Bold, with the `Welcome home` rendered in The Seasons Light script as an accent. Citron full-stop.
> 4. **Subhead:** `Sign in to follow your build, see your documents, and book your final walkthrough.` — 17px Inter regular, line-height 1.5, max-width 44ch.
> 5. **Email field**, label `Email address`, placeholder `you@example.co.nz`, with magic-link sign-in.
> 6. **Primary button**: `Send me a sign-in link` — full-width, `#2B2B2B` background, white text, citron right-side dot. After click → success state below.
> 7. **Success state** (replaces button after submit): `Check your inbox — link expires in 15 minutes.` Citron tick icon left.
> 8. **Tertiary link**: `Need help signing in? Email Damien.` (mailto:damien@taylored.co.nz)
>
> **Layout — mobile:** Single column. Image becomes a 280px-tall hero at the top. Form sits underneath, full-width with 24px gutters.
>
> **Footer:** Two lines, plain text, centred bottom:
> `taylored.HOME · Built by Taylored Group`
> `Auckland · Aotearoa New Zealand`

---

## Manual setup

1. **Add an Auth block** → Magic link mode → wire to your Airtable Users table (or Softr Users; see `airtable/schema.md`).
2. The hero image on the left needs to be **full-bleed** (no card, no padding). Use a Hero block with `Layout: Image left, content right` and turn off the inner padding.
3. **Wordmark with citron dots** — see `00-app-setup.md` step 1.
4. **Headline with script accent** — Softr's Heading block doesn't allow inline mixed fonts. Use a **Custom Code block** here:

```html
<h1 class="t-headline">
  <span class="script">Welcome</span> home<span class="dot">.</span>
</h1>
<style>
  .t-headline {
    font-family: "Mansfield", "Inter Black", sans-serif;
    font-weight: 900;
    font-size: 32px;
    letter-spacing: -0.025em;
    line-height: 1.05;
    color: var(--t-ink, #2B2B2B);
    margin: 0 0 12px;
  }
  .t-headline .script {
    font-family: "The Seasons", serif;
    font-weight: 300;
    letter-spacing: 0;
    font-size: 1.05em;
  }
  .t-headline .dot { color: #CEFF35; }
</style>
```

5. **Magic-link email body** — see `softr/copy/01-signin.md`.

---

## Acceptance check

- [ ] Page route is `/` and is Public
- [ ] The image on the left fills its column (no white border)
- [ ] The wordmark and headline both show citron full-stops
- [ ] `Welcome` is in script font, rest is in Mansfield Bold
- [ ] Submitting the form sends a magic-link email and shows the success state
- [ ] Mobile collapses to single column with image-on-top
