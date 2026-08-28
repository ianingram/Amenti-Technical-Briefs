# BUILD — THE WAY IN
### Ingram Manor LLC · 28 August 2026 · a door for a stranger who wants something

**Amenti opens on a roster of names.** A catalogue asks who you have heard of. It
should ask what you want.

*Need a tutor. Need a counsellor. Enter the conversation.*

This is the build document for that page. It is written to be built from, so
what is decided is stated and what is the captain's is marked — nothing here
should be settled by drafting.

---

## 1 · THE TAXONOMY ALREADY EXISTS, AND IT HAS THE FLAW

The most important finding, and it changes the shape of the work.

`Page1.html` already carries **thirteen groups**, keyword-matched against a
figure's title, powering both the card enrichment and the Browse chips:

```
  faith · science · healers · warriors · rulers · founders · explorers
  stage · music · artists · writers · thinkers · legends
```

Good categories, already built, already styled with a glyph and an accent each.
**They are not the problem.** The problem is one line in their own comment:

> *Order = match priority (**first keyword hit wins**).*

**A figure gets ONE group, and it is whichever keyword appears earliest in the
list.** Run against real titles on 28 Aug:

| title | lands in | matched on |
|---|---|---|
| Roman General and Dictator | `warriors` | "general" |
| Emperor of Rome | `rulers` | "emperor" |
| **Pontifex Maximus** | **`legends`** | nothing — the catch-all |

**Caesar is a warrior and nothing else.** He held the highest priesthood in Rome
from 63 BC for the rest of his life, and the taxonomy cannot see it, because
`general` sits earlier in his title than anything else does. And *Pontifex
Maximus* on its own falls through entirely: `priest` is a `faith` keyword;
`pontifex` is not.

> **THE CATEGORIES ARE NOT MISSING. THEY ARE SINGLE-VALUED.**

That is the whole build. Not thirteen new categories — **a second value per
figure**, so the roster can answer *who should I ask about faith and power* with
a man nobody would have clicked.

---

## 2 · WHAT A TAG IS

**A tag is what a figure can SPEAK TO. Not what they were.**

The same distinction the eighteen-term type vocabulary drew for the works, and
the same discipline: the vocabulary is a contract, the list is closed, and the
ordering is the decision.

**The existing thirteen ARE the vocabulary.** Do not invent a second set. A
figure's group stays exactly as it is — it drives the card glyph and the Browse
chip and nothing about that should move. What is added is a short list of
**other groups the figure can genuinely speak to**:

```json
"caesar": { "group": "warriors", "speaks": ["faith", "rulers"] }
```

### The rule that keeps this honest

**A tag must be TRUE, and defensible from the record.**

- Caesar on Roman religion: **grounded.** He ran it.
- Caesar on faith in general: **a figure stretched to fill a slot.**

The second is precisely what the primary-source moat exists to refuse, and the
prospectus sells the difference by name — *"ungrounded; invent quotes"* against
*"verified primary-source grounding."* **A surprising tag is the whole value of
this feature and a false one is the whole risk.**

### Where the tags come from — CAPTAIN'S DECISION

Three ways, and they are not equal:

1. **By hand, on the sheet.** A `Speaks` column beside `Title`. Honest, slow,
   1,011 rows. Start with the 52 who have rooms.
2. **Derived from the biography**, by keyword — the same mechanism as the group,
   run against `Biography` instead of `Title`. Free, immediate, and it will be
   wrong sometimes in a way nobody notices.
3. **Proposed by a model, confirmed by hand.** One pass over the roster
   suggesting tags with a one-line justification; the captain accepts or
   refuses. ~$10 for the whole roster, and every tag arrives with a reason
   attached.

**The third is the assistant's recommendation** — it produces the surprises that
make the feature worth having, and the confirmation step is what keeps a
surprise from becoming an invention. **But it is the captain's call**, and it
should be made before anything is built, because the page's whole promise rests
on it.

---

## 3 · THE PAGE

A reader arrives wanting something. The page asks what, and answers with faces.

```
        WHAT DO YOU NEED?

   [ a tutor ]  [ a counsellor ]  [ an adversary ]  [ a witness ]

        ┌──────────┐  ┌──────────┐  ┌──────────┐
        │  NEWTON  │  │ GALILEO  │  │  CAESAR  │
        │  plate   │  │  plate   │  │  plate   │
        └──────────┘  └──────────┘  └──────────┘
             enter the conversation
```

### The intents, and how they differ from the groups — CAPTAIN'S DECISION

**Group and intent are different axes and must not be merged.** A group is a
kind of person; an intent is a kind of conversation. `warriors` is a group;
*adversary* is an intent. The page asks for the intent and uses groups to fill it.

Candidates, and they are not equal:

| intent | what it means | machinery |
|---|---|---|
| **a tutor** | teach me something | the terminal, character mode |
| **a counsellor** | help me with my life | **counsel mode already exists** |
| **an adversary** | argue with me | the docket and the court are already this |
| **a witness** | you were there — what was it like | character mode, a different framing |
| *company* | I just want to talk to someone interesting | *probably what most people want, and the hardest to put on a card without sounding lonely* |

**Two of these already have machinery.** Counsel is a mode with its own prompt
branch; the adversary has the whole Cosmic Courtroom behind it. That argues for
starting with those two rather than the ones that need new staging.

### THE CARDS COME FROM THE ROSTER, NEVER TYPED

A page hardcoding six figures goes stale the day a seventh belongs there. Every
card is drawn from `AMENTI_CHARS` and the plate register at open, exactly as the
Codex does — the same discipline as every pane: **a reflection, not a document.**

Which also means the page needs no maintenance when the roster grows, and cannot
be edited into a lie, because there is nothing to edit.

---

## 4 · WHERE IT SITS — CAPTAIN'S DECISION

Two answers, and they are different builds:

**A landing page** — its own file, what a stranger meets *before* the flagship.
The ad links here. The arena currently plays this role and would need to yield.

**A pane inside Page1** — a `data-page` section beside Browse and the Codex.
Cheaper, and it competes with two surfaces that already do something similar.

**The assistant's read: its own file.** The ad needs somewhere to land that is
not 525 KB, and a stranger arriving from Facebook should not be met by the whole
application at once. It also keeps the flagship untouched, which for a file this
sensitive is worth something on its own.

---

## 5 · EVERY BUTTON IS A SURFACE

Per `SPEC-SURFACES.md`: a surface is a user interface point. This page carries
several — one per intent, plus the cards.

**Each intent chip should carry its own `?via=`.**

```
  hall.html?via=intent-tutor
  Page1.html?char=caesar&via=intent-adversary
```

`amenti-visits.js` already captures `via` and remembers it for the session;
`GET /visits` already breaks arrivals down by channel. **So the page answers a
question nothing currently can: which kind of question brings people in.**

That is the retention number the prospectus asserts and has never had — and it
costs one attribute per link.

**And every surface on this page needs an entry in `SURFACES.semantics.json`** in
the same commit that builds it. The register is one day old; letting it go stale
on the first new page would be the fault it was built to catch.

---

## 6 · THE AD IS A SLICE OF THIS PAGE

Facebook and YouTube do not take embedded HTML. **An ad there is artwork plus a
line plus a link** — so the ad is a card cropped from this page, and the page is
where it lands.

Built in that order the ad cannot promise what the site does not deliver, and
neither goes stale when the roster changes.

**Tag lines, from the conversation that produced this document:**

> **Enter the conversation.** — describes the thing rather than naming a figure,
> and works under any plate.
>
> **Join the debate.** — the sharper sibling, if the image is two figures.
>
> **Ask Caesar about God.** — arresting, true, and it teaches what the site is in
> four words. *This one only works once the tags exist.*

**A true embeddable widget** — real HTML on a third-party site — is a later and
different thing. When it comes, **it calls NOTHING**: cards and a link out. The
proxy's allowlist exists to stop a hostile site spending the keys from a
visitor's browser, and for an ad unit calling nothing is the correct answer
anyway. The conversation happens on Amenti's ground.

---

## 7 · THE ORDER OF WORK

1. **Decide where the tags come from** (§2). Everything else waits on it.
2. **Decide the intents** (§3). Two of them already have machinery.
3. **Tag the 52 who have rooms.** Not 1,011. The page can open on the souls the
   library can actually support.
4. **Build the page**, cards from the roster, `?via=` on every link.
5. **Enter its surfaces in `SURFACES.semantics.json`**, same commit.
6. **Cut the ad** from a card on it.

**And before any of it: test the second voice** (SLIP-ADDENDUM-THE-SECOND-VOICE).
Two figures, one question, by hand, about two dollars. If a scene is better than
a single figure, this page is advertising *enter the conversation* rather than
*talk to Newton* — and that changes what the cards are.

---

## 8 · ACCEPTANCE

**Open it cold, pick an intent, and land in a conversation without having typed
a name.** Then `GET /visits` shows the intent in `via`.

And the one that matters more: **a reader arrives wanting to understand faith and
power, and is offered Caesar.** If the page cannot do that, it is the roster with
better typography.

---

*Written 28 Aug 2026. §1 is measured against Page1.html — the thirteen groups,
the first-hit rule, and Caesar landing in `warriors` are read from the file, not
assumed. The three decisions marked CAPTAIN'S are load-bearing and none should
be made by drafting.*
