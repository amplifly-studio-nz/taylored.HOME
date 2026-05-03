# Copy · 01 Sign in

Every line of copy on the sign-in page, ready to paste into Softr blocks.

---

## Page

**Eyebrow:**
```
OWNER PORTAL · LOT 11 · SEAVIEW RISE
```

**Headline:**
```
Welcome home, Regina.
```
(Render `Welcome` in The Seasons script. Citron full-stop after `Regina`.)

**Subhead:**
```
Sign in to follow your build, see your documents, and book your final walkthrough.
```

**Email field label:**
```
Email address
```

**Email field placeholder:**
```
you@example.co.nz
```

**Primary button:**
```
Send me a sign-in link
```

**Success state (after submit):**
```
Check your inbox — link expires in 15 minutes.
```

**Help link:**
```
Need help signing in? Email Damien.
```
(mailto: damien@taylored.co.nz)

**Footer:**
```
taylored.HOME · Built by Taylored Group
Auckland · Aotearoa New Zealand
```

---

## Magic-link email (sent by Softr Auth)

**From name:** `Damien from taylored.HOME`
**From email:** `damien@taylored.co.nz`
**Reply-to:** `damien@taylored.co.nz`
**Subject:** `Your taylored.HOME sign-in link`

**Body (HTML or markdown — Softr supports both):**
```
Hi {{first_name}},

Tap the link below to sign in to your owner portal.

[Sign in to taylored.HOME]({{magic_link}})

The link works once and expires in 15 minutes. If you didn't ask for it, ignore this email.

Anything else, just reply.

Damien
+64 21 333 3334
```

---

## Error states

**Email not recognised:**
```
We don't have that email on file. Email Damien if you think this is a mistake.
```

**Link expired:**
```
That link's expired. Tap "Send me a sign-in link" again.
```

**Link already used:**
```
That link's already been used. If it wasn't you, email Damien.
```
