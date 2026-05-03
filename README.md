taylored.HOME → Softr handoff package
For: Damien Taylor & whoever builds this in Softr.
Why this folder exists: Softr won't import HTML or Figma files and recreate them as blocks. It builds from prompts (AI Co-Builder) or visual block editing. This folder turns the portal designs into something Softr can actually consume.
---
What's in here
```
softr/
├── README.md                    ← you are here
├── prompts/                     ← paste these into Softr AI Co-Builder, one per page
│   ├── 00-app-setup.md          ← brand setup: colours, fonts, navigation
│   ├── 01-signin.md
│   ├── 02-dashboard.md
│   ├── 03-steps.md
│   ├── 04-step-detail.md
│   ├── 05-documents.md
│   ├── 06-document-viewer.md
│   ├── 07-walkthrough.md
│   ├── 08-walkthrough-confirmed.md
│   ├── 09-contact.md
│   ├── 10-ask.md
│   ├── 11-profile.md
│   ├── 12-letter-outbox.md      ← admin
│   └── 13-slot-manager.md       ← admin
│
├── copy/                        ← every headline, subhead, button label, ready to paste
│   ├── 01-signin.md
│   ├── 02-dashboard.md
│   ├── 03-steps.md
│   ├── ...
│   └── voice-and-tone.md
│
├── custom-code/                 ← drop into Softr Custom Code blocks
│   ├── countdown.html           ← 28 DAYS · X HOURS settlement countdown
│   ├── steps-timeline.html      ← horizontal 7-step pill timeline w/ states
│   ├── concierge-bubble.html    ← bottom-right bubble that opens a chat window
│   ├── _shared.css              ← brand variables (paste into App settings → Custom code → Header)
│   └── README.md
│
├── airtable/                    ← Airtable schema as Softr expects to wire it up
│   └── schema.md
│
└── assets/                      ← upload these to Softr Files
    ├── brand/
    │   ├── palette.csv          ← hex codes per Softr slot
    │   ├── logo-wordmark.png
    │   ├── logo-icon.png
    │   └── persona-* / number-* / etc.
    └── design-references/       ← PNGs of every page, for the admin-only "Design system" page
        ├── 01-signin-desktop.png
        ├── 02-dashboard-desktop.png
        └── ...
```
---
How to use this — three-step recipe
Step 1 — Set up the app shell
Paste `prompts/00-app-setup.md` into Softr's AI Co-Builder. This sets brand colours, fonts, the sidebar/topbar nav, the bottom tab bar (mobile), and the auth flow (email-link).
After Co-Builder generates, go to App settings → Branding and paste in the seven brand colours from `assets/brand/palette.csv`. Verify the typography matches `prompts/00-app-setup.md`.
Step 2 — Build pages one at a time
Open Softr's left rail → App Pages → + New page. For each page:
Open the matching `prompts/NN-pagename.md` file.
Paste the `PROMPT` block into Co-Builder.
Wire the data source as specified at the top of each file.
Set visibility role as specified (Public · Logged-in Owner · Logged-in Admin).
Replace any AI-generated copy with the verbatim copy from `copy/NN-pagename.md`.
For pages that need bespoke layout (Dashboard, Steps), open `custom-code/*.html` and paste those snippets into Custom Code blocks where indicated.
Step 3 — Cross-check against design references
Upload everything in `assets/design-references/` to Softr Files, create an admin-only page called "Design system" with an Image Gallery block sourced from those files. Anyone editing the portal in Softr can compare what they see in the editor to the intended design.
---
What Softr will get right vs. what you'll need to tweak
Co-Builder usually nails:
Page structure, block selection, data wiring, list/details/form binding, visibility rules, navigation.
You'll need to tweak by hand:
The signature citron full-stop dot at the end of `taylored.` and `HOME.` — Softr uses solid colour buttons; achieve the dot by either splitting the wordmark into two text blocks or pasting the SVG wordmark from `assets/brand/`.
Display typography — Softr's font picker has Mansfield Bold and Anonymous Pro on its Google Fonts catalogue, but won't load The Seasons Script. Upload `fonts/TheSeasons-Light.otf` (in `assets/brand/fonts/`) via App settings → Custom code → Header.
The countdown ("28 DAYS · X HOURS") and steps-timeline pill row — these are bespoke; use `custom-code/countdown.html` and `custom-code/steps-timeline.html`.
The concierge bubble in the bottom-right — use `custom-code/concierge-bubble.html` in the App settings footer custom code so it appears on every page.
---
What lives in Airtable, what lives in Softr
Airtable holds all the data: Owners, Lots, Documents, Steps, Walkthrough Slots, Bookings, Concierge Conversations, Concierge Messages.
Softr is the front door. Pages read from Airtable views, write back via forms.
See `airtable/schema.md` for the full table list and field types.
---
Open questions for Damien
Will the AI Concierge (`prompts/10-ask.md`) use Softr's built-in AI Chat block, or be embedded from a separate service via `custom-code/concierge-bubble.html`? The prompt assumes Softr AI Chat; flip to embed mode if you want Claude or another model on the back end.
Do letter outbox and slot manager (`12`, `13`) need to be in Softr now, or stay in Airtable for M1 and migrate post-launch? The prompts are written assuming Softr; comment out those pages in Co-Builder if you'd rather defer.
---
This package was generated to accompany `design/portal.html`.
Last updated: May 2026, M1 handoff.
