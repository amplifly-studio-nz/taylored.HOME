# Copy · 10 Ask taylored.

---

## Page header

**Avatar:** Lowercase `t.` with citron full-stop (use SVG from `assets/brand/avatar-taylored.svg`)

**Headline:**
```
Ask taylored.
```

**Sub:**
```
I know your home, your settlement timeline, your documents, and your team. Plain English answers, anytime.
```

---

## Default suggestion chips

(Shown above the input on first load; replaced/extended by context-aware chips when `?step=` or `?doc=` query params are present)

```
When is settlement?
What to bring on walkthrough day
Who is my lawyer?
Show my documents
```

---

## Context-aware chips (when ?step=N)

```
Tell me more about Step {N}
What do I need to do for this step?
Who's responsible for this?
```

---

## Context-aware chips (when ?doc=...)

```
Explain this document
What do I need to do?
When is this due?
```

---

## Input

**Placeholder:**
```
Ask anything about your home or settlement…
```

**Send button:**
```
Send
```

---

## Sidebar — What taylored. knows

**Eyebrow:**
```
WHAT TAYLORED. KNOWS
```

**Paragraphs:**

```
Your settlement date, your lot details, your team's contact info.
```

```
Every document in your portal, and what each one means.
```

```
All seven steps to settlement, what's done, what's coming.
```

---

## Sidebar — When to talk to a human

**Eyebrow:**
```
WHEN TO TALK TO A HUMAN INSTEAD
```

**Paragraphs:**

```
If something's wrong with your build — call Simon.
```

```
If you have a legal or settlement question — call Tom or Damien.
```

**CTA button:**
```
Open Contact →
```

---

## System message templates

**On opening with `?step=N`:**
```
You're asking about Step {N} — {StepTitle}. Here's what I know.
```

**On opening with `?doc=...`:**
```
You're asking about {DocumentName}. Want me to explain it, summarise it, or tell you what to do next?
```

**Mid-conversation, AI is composing:**
(typing indicator only — three citron dots)

**Empty state (first-time user):**
```
Hi {FirstName}. Ask me anything about your home or your settlement. If I can't help, I'll point you to the right person.
```

---

## Hand-off responses (when AI should escalate)

**On a build-quality question:**
```
That's one for Simon — he's onsite daily and will know exactly what's going on. His number is +64 21 ___ ____.
```

**On a legal/money question:**
```
Tom is your lawyer for this. Tom Goldsworthy at Buddle Findlay — +64 9 357 ____. He handles all the settlement money flow.
```

**On something time-sensitive:**
```
This sounds time-sensitive. Damien is your best person — call him directly: +64 21 333 3334.
```
