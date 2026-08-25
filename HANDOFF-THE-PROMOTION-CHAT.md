# AMENTI — HANDOFF: THE PROMOTION CHAT
**Ingram Manor LLC · 24 August 2026 · a handoff, not a plan**

## WHAT THIS IS

A cold-start brief for a session whose job is **promoting Amenti**. It assumes
no memory of the build. It gives the next chat: what Amenti is, what is
promotable *right now* versus not, the five questions the captain must answer
before real work begins, structural promotion ideas to react to, and the exact
files and URLs to read first.

**Read the five questions in §4 first.** Do not write a campaign before they are
answered — a promotion plan built on guesses about goal and audience is the
marketing version of a register that is a memory. Ask, then build.

---

## 1 · WHAT AMENTI IS (say this in one breath)

Amenti is a **library of the dead you can talk to** — a web library of history's
great figures, each with a page, many with a face and a reading room, and many
who **answer in their own voice** when asked. It is built by one person under
Ingram Manor LLC, on a stack of static files, Cloudflare Workers, and Supabase.

The single sharpest promotional fact: **it demonstrates itself.** Most products
must *describe* their value; Amenti's front-facing surface, the hall, lets a
stranger type a question and get an answer immediately. You are not selling "you
can talk to history" — you can just let people do it.

Numbers, read this hour (do not quote from memory — read `HALL-STATE.json`):
**1,011 souls · 51 with portraits · 52 with reading rooms · ~129 documents
indexed.**

---

## 2 · WHAT IS PROMOTABLE RIGHT NOW

Be honest about this; promoting a paused surface burns trust.

**Ready — promote these:**
- **The hall / Ask Amenti** — `https://ianingram.github.io/Amenti.live/hall.html`
  — live, striking, self-demonstrating. THE strongest asset. A doorway that
  answers.
- **The library itself (Page1)** —
  `https://ianingram.github.io/Amenti.live/Page1.html` — the flagship: the
  pyramid gateway, the roster, the figures. Visually arresting.
- **The figures you can converse with** — the actual product magic. Talking to a
  specific soul is the thing people will screenshot and share.

**NOT ready — do not lead with these:**
- **The fleet (Atlantica, THE WEEK, the Dispatch, the podcast)** — mostly
  **paused**, not broken. Atlantica dark since early August; THE WEEK has never
  fired. See `fleet-status.html` for live state. Promoting a "weekly dispatch"
  that is not currently firing would be a promise the ship is not keeping. When
  the presses resume (a deliberate future step), they become promotable.
- **The contributor surface** — architected, not built. Do not advertise "come
  help" until the slip pane exists.

**The honest posture:** promote the *library and the conversation*, which are
real and live. Hold the *publications* until they resume.

---

## 3 · KNOWN ISSUES A PROMOTER SHOULD KNOW (so a demo doesn't break)

- The hall's footer link "The Separation of Power" points at
  `Amenti_Separation_of_Power.html`, which is **404 on the live site** — that
  brief lives in the *Amenti-Technical-Briefs* repo, not `Amenti.live`. A
  visitor clicking it hits nothing. **Fix before any demo drives traffic:**
  either copy the file into `Amenti.live` or repoint the link.
- Several deck cards crop too tight (Bram Stoker, Helen Keller, Seneca). Cosmetic
  but visible in screenshots.
- The hall spends model tokens per question. Traffic costs money. The proxy has
  hard caps and an origin allow-list (only approved domains can call it), so a
  viral spike is bounded, not catastrophic — but **know that promotion has a
  per-visitor cost**, and the lanes work (see the outward-probe briefs) is what
  would make paid promotion safe at scale.

---

## 4 · THE FIVE QUESTIONS — answer before building anything

These shape everything. A promotion chat should ask them first and refuse to
write a campaign until they are answered.

1. **What is the goal?** Traffic to the hall · sign-ups · awareness that Amenti
   exists · revenue · building a contributor community. "Promote" means
   different work for each. Pick one primary.

2. **Who is the audience?** History enthusiasts · the AI-curious · educators &
   students · developers · the general public. Amenti reads completely
   differently to each. Pick a first beachhead, not "everyone."

3. **What is promoted — live surfaces only, or wait for the presses?** Per §2,
   the recommendation is: promote the library and the conversation now; hold the
   publications until they resume. Confirm or override.

4. **What channels exist?** Existing social accounts · a mailing list ·
   communities the captain belongs to · nothing yet. This decides whether the
   first move is "post to what you have" or "establish a presence."

5. **What is the constraint?** Assume solo operator, minimal time, near-zero
   budget unless told otherwise. This rules most tactics in or out — favor
   organic, self-demonstrating, low-maintenance over paid or high-touch.

---

## 5 · STRUCTURAL PROMOTION IDEAS (to react to, not a plan)

Organized by the principle that fits Amenti best: **let the thing demonstrate
itself.** These are starting points for the captain to accept, reject, or
reshape once the five questions are answered.

### A · The hall as the hook, everywhere
The hall answers questions. Every promotional artifact can *be* a question and
its answer. A post is not "check out my history site" — it is a screenshot of a
figure answering something surprising, with the URL. The product is the ad.
- Screenshots/clips of specific figures answering pointed, funny, or profound
  questions.
- "Ask a dead genius" framing — pick a figure, pose a question people are
  curious about, show the answer.

### B · The figure-of-the-day / conversation snippet
Even with the *automated* presses paused, a human can post one striking
exchange a day by hand — no infrastructure needed. This is promotion that
doubles as content, and it seeds the eventual automated Atlantica.

### C · The visual asset is unusually strong
The pyramid gateway, the gold-and-black aesthetic, the reading rooms — Amenti is
*beautiful* in a way most web projects are not. Visual-first platforms
(where images and short video carry) suit it. Lead with the look, let the
concept follow.

### D · The premise is inherently shareable
"A library of the dead you can talk to" is a one-line hook that travels. It
provokes the immediate reaction *wait, can you really?* — and the answer is
yes, here, try it. The gap between the claim and the instant proof is the
share.

### E · Meet audiences where curiosity already lives
Communities built around history, philosophy, specific figures, AI
experimentation, worldbuilding, and beautiful web design are natural first
homes. The beachhead question (§4.2) decides which.

### F · The embed, later — the outward probe
Architected but not built (see `BUILD-ORDER-THE-OUTWARD-PROBE`): a search-only
or ask-enabled embed of the hall that can live on *other* sites. This is
promotion as *distribution* — the doorway placed in other people's walls. It
requires the proxy's lane work first (safety and cost control). A real future
lever; note it, don't lead with it.

### The through-line
Amenti's promotion should never feel like marketing bolted on. The library
*is* the pitch; the conversation *is* the demo. The job is to remove every step
between "a stranger hears about this" and "a stranger is talking to Caesar."

---

## 6 · FILES & URLS TO READ FIRST

**Live surfaces (open these — they are the product):**
- Hall: `https://ianingram.github.io/Amenti.live/hall.html`
- Library / flagship: `https://ianingram.github.io/Amenti.live/Page1.html`
- Fleet status (to see what is live vs paused):
  `https://ianingram.github.io/Amenti.live/fleet-status.html`

**Registers, for real numbers (read, never quote from memory):**
- `HALL-STATE.json` — the counts the hall may state
- `fleet.json` + `fleet-dispatch.json` — what is meant to fire vs what did
- `SOURCES.json` — the full document index

**Briefs, for context (in `Amenti-Technical-Briefs`):**
- `Amenti_Separation_of_Power.html` — the constitution; what Amenti *is*, deeply
- `BRIEF-ASK-AMENTI` — the hall's spec and philosophy
- `BUILD-ORDER-THE-OUTWARD-PROBE` — the embed/distribution plan (future lever)
- `ARCHITECTURE-THE-CONTRIBUTOR-SURFACE` — the "come help" surface (not built)
- `THE-STANDING-SLIP` — the open-work backlog

**Doctrine to respect in any promotional copy:**
- Amenti does not pretend to be a séance. The voices are performances built with
  care from the historical record — "a reading room with very good acoustics,"
  not a claim of contact with the dead. Promotional language should keep that
  honesty; it is part of the brand's integrity and its legal safety.
- The figures are the destination; the hall is the doorway. Copy should point
  *inward*, toward the souls, not dwell on the machinery.

---

## 7 · FIRST MOVE FOR THE PROMOTION CHAT

1. Ask the five questions (§4). Get at least goal + audience + constraint.
2. Fix the broken "Separation of Power" link (§3) if any promotion will drive
   traffic — a dead link on the front surface undercuts everything.
3. From the answers, pick ONE beachhead and ONE first artifact (most likely: a
   single striking hall exchange, posted where the chosen audience already is).
4. Do not build a multi-channel plan on day one. One audience, one hook, one
   proof-by-demonstration. Measure, then widen.

> The library is the pitch. The conversation is the demo. Remove every step
> between hearing about Amenti and talking to the dead.
