# BRIEF · THE BOX THAT CONTAINS SEVERAL
**What replaces declare-everything in the hall · Ingram Manor LLC · opened 31 August 2026**

For THE STANDING SLIP #13. Written the night the hall was found silent, from
measurements taken against the live registers, not from memory of them.

> **THE HALL SENDS EVERY DOCUMENT ON EVERY QUESTION, SO THAT NOTHING CAN BE
> MISSED IN SILENCE. THAT PRINCIPLE IS RIGHT AND THIS BRIEF DOES NOT ARGUE WITH
> IT. IT ARGUES THAT THE PRINCIPLE MUST NOW BE KEPT BY A DIFFERENT MEANS.**

---

## 0 · WHAT THE CAPTAIN DECIDED, RECORDED BEFORE IT IS LOST AGAIN

Stated on 31 Aug, and written down here because the last version of this
decision was made in an earlier session, existed in no file, and survived only
because the captain remembered it and said so.

**Ask Amenti becomes one box containing several.** A single surface that answers
about the architecture, about history, and about a person — so a visitor need
not already know which chat surface answers which kind of question. Today they
must: the terminal speaks AS a figure, the hall speaks ABOUT the ship, and
knowing that is the visitor's problem.

**Mostly inward-facing, because the primary-source library is the point.** The
works are called and cited. Next they must be searched and worked with.

**And it is a search engine for the site, not a router.** It answers. It does
not hand the visitor off to somewhere else and stop.

### The layering, in the captain's terms
```
the hall     the place — a page with an image and a box on it
the box      where a visitor types
the engine   amenti-hall.js — what answers. This is the part that is broken.
```
The hall as a place is unaffected by anything below. Only the answering fails.

### A NAMING CAUTION, PAID FOR IN THIS SESSION
`modes` is taken — the terminal's five ways a figure speaks, with a control on
the page and `setMode` behind it. `throttle` is taken — `amenti-throttle.js`,
retired, guarded by probe17. `registers` is taken. The lane-selector below needs
a free word and this brief deliberately does not spend one.

---

## 1 · THE MEASUREMENT THAT FORCES THE DECISION

Taken 31 Aug by `probes/probe-hall-wall.mjs`, which lifts and runs the hall's
own `catalogueText` and `buildSystem` rather than a copy of them.

```
HALL.md          5,751
the counts         599
the catalogue   16,160     190 entries, 85.1 chars each
the rest         1,698     preamble and the nine rules
SYSTEM PROMPT   24,208     wall 20,000 — OVER by 4,208
```

The Worker refuses this with `system_too_long` — a 413 with a named reason in
the body, not a shorter answer. **An overrun is not a degraded hall. It is a
silent one.**

### The trim is a stopgap and must not be mistaken for a fix

`amenti-hall.js` line 115 trims each gloss to 90 characters. Lower it and the
prompt fits:

```
trim   docs that fit   headroom vs 190   what it buys
  90        139             -51          already over
  60        180             -10          already over
  50        202             +12          ~1 week
  40        232             +42          ~3 weeks
  30        271             +81          ~6 weeks
  24        301            +111          ~8 weeks
```

The week figures assume ~14 documents a week, inferred from 106 documents when
the catalogue was sized to 190 today. **THAT DENOMINATOR IS A GUESS** — the 106
comes from an undated comment in the source, and document growth is lumpy, not
steady. The measured part is the headroom, not the weeks. The probe recomputes
it every six hours.

### And the ceiling is hard

Each catalogue line costs about 21 characters before any description: the id
averages 14.8, the separators and newline take 6. So even with every gloss
deleted the absolute maximum is around 560 documents — and a catalogue of bare
ids is the `[undescribed]` failure the code already warns about, where the
entries that said nothing were invisible and a vendor-risk PDF became the
authority on who owns Amenti. **The USEFUL ceiling is nearer 250.**

---

## 2 · WHY DECLARE-EVERYTHING CANNOT SURVIVE THE BOX

The box the captain described must reach three bodies, not one.

```
the architecture     190 documents      SOURCES.json
the library          550 works          LIBRARY.json, 52 rooms
the roster         1,011 souls          names.csv / ROSTER-INDEX.json
                   ─────
                   1,751 entries

at today's gloss   148,835 chars     7.4x the whole wall
at a hard trim      87,550           4.4x
at bare ids          36,771          1.8x the wall — and 3.1x the space free
```

**Bare ids, every description deleted, still overruns three times.** There is no
trim, no compression and no encoding that reaches it. This is not a tight fit
that better engineering could win. The design is finished.

---

## 3 · THE ROAD: DOORS, THEN RETRIEVAL

### The insight the corpus hands us for free

The library is not 550 loose works — it is **52 rooms**, one per figure. The
documents are not 190 loose files — they are **8 sections**, and they are already
declared in `SOURCES.json`:

```
the briefs                71        the surfaces          10
the instruments           46        the log                3
the book itself           29        the slipway            3
the registers             24        the gameroom           4
```

So what goes up front is not a list of leaves. **It is a list of doors.** About
sixty lines, and it barely grows — adding a work to Caesar's room adds no door,
and adding a brief adds no section.

### What the engine sends, per question

```
the meaning         scoped to the lane, not all of HALL.md      ~2,500
the counts          unchanged                                      599
the rules           unchanged                                    1,698
the doors           8 sections + 52 rooms + a note on the roster ~2,940
what was retrieved  40 results at FULL 85-char gloss             3,400
                                                               ───────
                                                                11,137
wall                                                            20,000
LEFT FOR ACTUAL PASSAGES FROM THE WORKS                          8,863
```

**Eight thousand characters — roughly 1,477 words of primary source, in every
answer.** Slip #5 wanted 2,000 and could not afford it. Under this design it is
not a feature to schedule; it is change from the budget.

That is the worst case — a question touching every door. Most questions touch
one or two and cost far less.

### The three findings that shape the build

**① THE ROUTING IS ALREADY BUILT AND UNUSED.** `AmentiHall.find()` searches
`SOURCES.json` and `ROSTER-INDEX.json` by fragment, **with no model call and no
cost**, and it ships today. It is exported on `window.AmentiHall`. It handles
every question that names something. What it cannot do is semantic reach —
*who wrote about strategy* will not fragment-match `sun-tzu` — and that is
precisely what the door list is for. **Read `find()` before building anything
(SERVES).**

**② TOOL USE IS NOT A GATE.** Whether the proxy passes a `tools` array and
returns `tool_use` blocks is a property of the Worker, which is private and
unread. It does not matter. Retrieval works in two ordinary calls through the
door that exists: ask which doors the question opens, then send what is behind
them. Tool use would make it one call and cleaner. It is an optimisation, not a
prerequisite, and this brief was nearly written as though it were the other way
round.

**③ THE FIXED COST IS THE WRONG CONTENT FOR MOST QUESTIONS.** `HALL.md` is 5,751
characters — 29% of the wall — and it is the ship's meaning. Exactly right for
*ask the architecture*. Largely wasted on *what did Caesar write*. **A box with
lanes should choose what MEANING to carry, not only what to retrieve.** That is
the single largest saving available and it is invisible until the box has lanes.

---

## 4 · THE RULE THAT MUST BE IN THE FIRST LINE, NOT ADDED LATER

The reason the hall declares everything is that a retrieval pass can miss and
never say it missed. **The objection is to SILENCE, not to retrieval.**

A pass that declares its own coverage keeps the ethic exactly:

> **SEARCHED 1,751. OPENED 12. HERE IS WHAT WAS NOT OPENED.**

A search engine does this natively. It finds, it shows what it found, and it is
honest about the edges. *Nothing aboard covers that* remains a true and valuable
answer — from a library of primary sources it tells the visitor something real
about the corpus, and almost no product will say it.

**If this is added after the retrieval works, it will not be added.** It is the
whole claim, not a safeguard on it.

### And the harder rule, which follows from what Amenti is FOR

The captain's framing, and it corrects an earlier draft of this brief:

> **RELYING ON THE MODEL'S MEMORY FOR HISTORICAL PERSONS IS THE PRE-AMENTI
> FRAMEWORK. THE AMENTI MODEL IS SUPERIOR BECAUSE IT CRAWLS ONLY THE PRIMARY
> SOURCES.**

What a model has on Caesar is secondary text about him, absorbed at a remove,
unattributable and unauditable. What the library has is what he wrote, in a
named edition, traceable. These are not two grades of one thing. **One can be
checked.**

So the rule is not *mark which is which*. It is: **the answer comes from what
was opened, or it does not come.** A box that quietly fills gaps from training
is an ordinary chatbot with a citation habit, and it would undo the campaign
that produced 550 works, 495 cited, EMPTY at zero, and a `citations.yml` that
fails the build on an empty source.

The hall's existing rules already say this for the architecture — *cite only
documents in the catalogue*, and *do NOT describe Amenti from your own training
— you would be inventing a project that is not this one.* This extends the same
principle to the history, for the same reason.

**Where the model's own knowledge still works, invisibly:** understanding the
question. Knowing that *strategy* should open Sun Tzu's room, that the Rubicon
is a Caesar question. That is comprehension, it decides what to OPEN, and then
it gets out of the way. It never asserts.

### THE GUARD, BECAUSE A RULE WITHOUT AN INSTRUMENT IS A HOPE

> **A VERBATIM QUOTE MUST BE A SUBSTRING OF THE TEXT FETCHED THIS TURN.**

Mechanically checkable. If it is not a substring, it does not ship. This matters
more here than anywhere else on the ship: the model knows famous passages from
Caesar and Sun Tzu, but in SOME translation absorbed from everywhere — not the
edition in the library. **A remembered quote under a real citation makes the
edition a lie**, which is precisely what the citation campaign was fought to
prevent, arriving through the front door.

---

## 5 · WHAT IS NOT DECIDED HERE

This brief lays out one road and prices it. The captain picks. The alternatives,
honestly stated:

- **Purpose-built short glosses.** A `short` field authored for the catalogue
  rather than truncating prose mid-sentence. Better quality than the trim AND
  smaller. Buys months. Still linear, so it postpones §2 rather than answering
  it. **Worth doing anyway** — it improves the doors too.
- **Attack the fixed 40%.** Independent of everything else, one-off, ~60
  documents' worth.
- **Raise the wall deliberately.** The Worker's policy is *if a surface 413s
  here, CHUNK THE SURFACE*, written after a real overrun. But 20,000 was chosen
  for a smaller corpus. Changing it should be a decision taken in daylight, not
  a patch taken at night — and it does not survive §2 either way.

**The assistant measures, lays out the roads, and writes the choice down. The
captain picks the road.** (THE STANDING SLIP, decisions the assistant should not
make alone.)

---

## 6 · THE MOVES, WITH TESTS THE CAPTAIN CAN PERFORM BY OPENING SOMETHING

**A · Make the hall answer at all.** The trim, or whatever stopgap is chosen.
- *Test:* open the hall, ask a question, get an answer — and
  `node probes/probe-hall-wall.mjs` exits 0. Slip #12.

**B · Build the door list.** Sections from `SOURCES.json`, rooms from
`LIBRARY.json`, a note that the roster is searchable by name.
- *Test:* the door list is under ~3,000 chars and every section and room in the
  registers appears in it.

**C · Two calls: choose the doors, then open them.** `find()` first, free, for
anything named.
- *Test:* a question naming a figure opens that room and no other. A question
  naming nothing still opens something, or says nothing aboard covers it.

**D · The coverage statement.** Built in from the first line.
- *Test:* every answer names how many entries were searched and how many opened.
  Ask something the corpus does not cover; the answer says so plainly.

**E · The substring guard.** A probe, not a promise.
- *Test:* plant a plausible but non-existent quotation in a test question; the
  answer does not reproduce it as a quote from the library.

**F · Scope the meaning to the lane.** The largest single saving.
- *Test:* a question about a figure does not carry the fleet's architecture
  doctrine in its prompt, and `probe-hall-wall` shows the drop.

---

## 7 · WHAT THIS BRIEF DOES NOT KNOW

Stated so the next session does not mistake absence for absence of a problem.

- **`amenti-hall-box.js` has never been read** by the assistant. It is the box —
  the interactive surface — and every measurement here is of the engine beneath
  it.
- **Whether the box appears on Page1 as well as `hall.html`** is unconfirmed.
  The engine's own prompt tells the model the visitor is *on the arena page*,
  while the box is loaded by `hall.html`. One of those is wrong.
- **The proxy is private.** `SYSTEM_CHARS`, the cache key composition, and
  whether tools are supported are all unread. The wall is DECLARED at 20,000 in
  the hall's comments and measured against, never observed.
- **Gemini's role.** The captain states, as builder, that Gemini speaks and that
  is its only job — *as far as I know*. `VOICE.json` confirms the speech path
  and explicitly declines the question: *intent, doctrine, register choice —
  those are authored and live in the briefs.* Worth making a reading rather than
  a recollection; `probe-voice` already walks every `/speak` site and a sibling
  could name every model call and its provider.

---

*Opened 31 Aug 2026 for THE STANDING SLIP #13. Every number here was measured
against the live registers by an instrument that lifts the hall's own functions
rather than reimplementing them — because the first version of this measurement
was done by hand, looked authoritative, was never run against the real code, and
was wrong by 342 characters. If this brief and a register disagree, the register
is right and this has gone stale.*
