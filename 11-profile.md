# 10 · Ask taylored. (concierge)

**Path:** `/ask`
**Page type:** Custom (chat interface)
**Visibility:** Logged-in Owner
**Linked Airtable tables:** ConciergeConversations, ConciergeMessages, KnowledgeBase

---

## PROMPT

> Create an "Ask taylored." concierge chat page at `/ask` for the `taylored.HOME` portal.
>
> Regina asks the AI assistant questions about her home, settlement, documents, walkthrough, etc. The AI is branded as `taylored.` (the brand) — it never pretends to be Damien.
>
> **Page header:**
> - Lowercase `t.` avatar (citron full-stop) top-left, 56×56px
> - Headline: `Ask taylored.` (citron full-stop)
> - Sub: `I know your home, your settlement timeline, your documents, and your team. Plain English answers, anytime.`
>
> **Two-column layout (desktop):**
>
> *Left column (chat — 70%):*
>
> Chat history (scrolls vertically, newest at the bottom):
> - User messages: right-aligned, citron background, ink text, max-width 60% of column.
> - taylored. messages: left-aligned, white surface with 1px ink border, ink text. Each starts with the lowercase `t.` avatar.
> - System messages (rare): centred, mono small caps, light grey.
>
> When taylored. is composing: a typing indicator (3 animated citron dots).
>
> Input area (sticky bottom):
> - Plain text input, placeholder `Ask anything about your home or settlement…`
> - Send button (citron, ink text)
> - Above the input: a row of suggestion chips that change based on context:
>   - Default: `When is settlement?` · `What to bring on walkthrough day` · `Who is my lawyer?` · `Show my documents`
>   - If `?step=N` in URL: prepend a chip like `Tell me more about Step {N}`
>   - If `?doc={record_id}` in URL: prepend a chip like `Explain this document`
>
> *Right column (sidebar — 30%):*
> - Eyebrow `WHAT TAYLORED. KNOWS`
> - Three short paragraphs:
>   - "Your settlement date, your lot details, your team's contact info."
>   - "Every document in your portal, and what each one means."
>   - "All seven steps to settlement, what's done, what's coming."
> - Eyebrow `WHEN TO TALK TO A HUMAN INSTEAD`
> - Two short paragraphs:
>   - "If something's wrong with your build — call Simon."
>   - "If you have a legal or settlement question — call Tom or Damien."
> - Bottom CTA: `Open Contact →` linking to `/contact`.
>
> **URL state:** All chat is persisted to ConciergeMessages Airtable. The `?step=` and `?doc=` query params don't change the URL hash; they pre-fill the first user message.
>
> **Mobile:** Single column. Sidebar collapses into a "What I know" link at the top that opens an info sheet.

---

## Manual setup

1. **Chat backend choice — pick one:**
   - **Option A (Softr-native):** Use Softr's AI Chat block, set up with a knowledge base built from `KnowledgeBase` Airtable table. See `softr/copy/concierge-knowledge.md` for what to populate.
   - **Option B (custom embed):** Use `softr/custom-code/concierge-bubble.html` — embeds a chat that posts to your own backend (Claude, OpenAI, etc.). Brand-styled to match.

2. **Persisting messages** — If using Softr AI Chat: configure it to write each message to `ConciergeMessages` (Owner, Conversation, Role, Content, CreatedAt). If using Option B: backend writes via Airtable API.

3. **Pre-filled question** — On page load, read `?step=` and `?doc=` from URL. If present, render a system-style hint message at the top of the chat ("You're asking about Step 3 — Walkthrough booking.") and pre-fill the input.

4. **Suggestion chips** — Static for M1. For M2, swap to dynamic based on the user's lot state (e.g. if walkthrough not booked: "How do I book my walkthrough?").

5. **Tone of voice** — See `softr/copy/voice-and-tone.md` for the system prompt that should be sent to the AI on every conversation.

---

## Acceptance check

- [ ] Chat history persists across sessions (refresh = same messages)
- [ ] Suggestion chips work and pre-fill the input
- [ ] AI responses cite specific docs/steps when relevant ("see Settlement Letter 1 in your documents")
- [ ] AI does NOT pretend to be Damien — refers to "Damien" in third person
- [ ] On mobile, chat fills the screen and sidebar moves to a sheet
