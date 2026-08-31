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
retired, guarded by probe17. `registers` is taken.

**THE WORD IS `hallway`.** Named by the captain, 31 Aug. The hall is the place;
a hallway is what runs between places and takes you to the right one — which is
precisely what the thing does. A question arrives and the hallway decides
whether it leads to the architecture, the library, or a soul. It collides with
nothing: `hall`, `hall.html`, `HALL.md`, `amenti-hall.js` and
`amenti-hall-box.js` are all distinct, and it reads as kin rather than as a new
vocabulary.

*One caution, worth knowing before it is in forty files: a grep for `hall` now
catches `hallway` too. On a ship that is read by grepping, that matters.*

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
documents are not 190 loose files — they are **8 sections**, already declared in
`SOURCES.json`:

```
the briefs                71        the surfaces          10
the instruments           46        the log                3
the book itself           29        the slipway            3
the registers             24        the gameroom           4
```

So what goes up front is not a list of leaves. **It is a list of doors.** And it
barely grows — adding a work to Caesar's room adds no door, adding a brief adds
no section.

### The rooms, priced from `LIBRARY.json` — 31 Aug

Not estimated. Built from the register and measured. Two forms:

```
52 rooms, name + work count            1,951 chars     37.5 per room
52 rooms + up to 3 section titles      5,395 chars    103.8 per room
```

**Pay for the rich form.** The section titles are the searchable substance:

```
· brutus — Brutus, 5 works: The disguise; The overthrow; The price
· bram-stoker — Bram Stoker, 7 works: Dracula (1897); Dracula's Guest (1914)
· akhenaten — Akhenaten, 6 works: The Great Hymn to the Aton; Boundary Stela
```

A question about betrayal reaches Brutus through *The overthrow* — not through
the word "Brutus". **That is exactly the semantic reach `find()` cannot do, and
the only reason the door list exists.** The bare form is a lookup; the rich form
is a search. The 3,444-char difference buys the whole point of the design.

### What the engine sends, per question — measured, not estimated

```
the meaning         scoped to the lane, not all of HALL.md      ~2,500
the counts          unchanged                                      599
the rules           unchanged                                    1,698
the doors           8 sections                                     480
                    52 rooms, rich form                          5,395
                    a note that 1,011 souls are name-searchable    120
what was retrieved  40 results at FULL 85-char gloss             3,400
                                                               ───────
                                                                14,192
wall                                                            20,000
LEFT FOR ACTUAL PASSAGES FROM THE WORKS                          5,808
```

**Roughly 968 words of primary source in every answer, worst case.** Slip #5
wanted 2,000 characters and could not afford them. Here it is change from the
budget.

Four combinations, all fitting, so the choice is about quality not survival:

```
bare rooms + full HALL.md      13,999    under by 6,001    ~1,000 words
bare rooms + scoped meaning    10,748    under by 9,252    ~1,542 words
RICH rooms + full HALL.md      17,443    under by 2,557    ~426 words
RICH rooms + scoped meaning    14,192    under by 5,808    ~968 words   <- take this
```

That is the worst case, a question touching every door. Most touch one or two.

### The library is the healthiest thing on the ship

From `LIBRARY.json`, and worth stating because everything else in this brief is
a fault: **52 manifests, 52 unlocked, 550 works present, 0 empty, 0 error,
30.9 MB.** Two rooms lack a card and two lack a terminal. The corpus this box is
being built to search is in good order. The engine in front of it is not.

### WHAT THE BOX ALREADY DOES — read 31 Aug, and it changes move B

`amenti-hall-box.js`, finally read. Three of its rulings are load-bearing here.

**SEARCH FIRST is already the free pass.** Names and fragments never reach the
model; only a genuine question spends, and only on Enter. `find()` runs on every
keystroke at no cost. **Finding ① below is not a proposal — half of it ships
today.** What is missing is only the semantic half.

**THE COVERAGE STATEMENT HAS A HOME.** The box already renders a `note` line
beneath the answer from two fields the engine returns: `drawn from: …` out of
`r.cited`, and `could not be read this turn: …` out of `r.degraded`. **Move D
needs no new surface** — it needs `searched / opened / not opened` added to what
the engine returns, and the note prints it. Considerably cheaper than assumed.

**AND THE ONE THAT COSTS SOMETHING — `linkMap` IS BUILT FROM THE CATALOGUE.**
The box turns cited ids into openable anchors, and *a citation the reader cannot
open is half a citation*. `linkMap()` walks the same flattened catalogue and maps
each id to a URL, skipping anything without a hyphen, underscore or dot.

> **THE DOOR LIST CHANGES WHAT THE MODEL CITES. IF `linkMap` STILL HOLDS ONLY
> DOCUMENT IDS, EVERY CITATION OF A ROOM OR A SECTION GOES DEAD ON THE PAGE —
> SILENTLY, BECAUSE AN UNMATCHED ID IS SIMPLY NOT LINKED.**

So move B is not one change. It is two that must land together: emit the doors,
and extend `linkMap` to cover rooms (`library/{key}.json` or the room's own
door) and sections. **Room keys pass `linkable()`?** `brutus` and `apollo` have
no hyphen and would be skipped; `augustus-caesar` and `bram-stoker` pass. That
rule was written to stop the word "hall" being linked in ordinary prose, and it
will now silently drop half the rooms. It needs revisiting in the same pass.

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

### AND A GAP IN THE GUARD, FOUND 31 AUG — THE REGISTER CANNOT SEE `recall`

`library.js` declares four work modes, and one of them breaks the rule above:

```
stored     fetch the .md body and render it        -- a real file
recall     RECONSTRUCT a public-domain passage
           VIA THE AI BRIDGE                       -- NO FILE. A MODEL.
link       external source, a button opens it
designed   an in-repo designed document
```

**A `recall` work has no text on disk.** Nothing is fetched, so the substring
guard has nothing to test against, and a passage arrives from a model wearing a
citation. That is the pre-Amenti framework already inside the library.

**Worse, the register cannot tell you which works those are.** `probe-library`
keeps only `title`, `section` and `source` — all 550 works, no exceptions. It
drops `mode`, `year`, `type` and `url`. So from `LIBRARY.json` a reconstructed
passage and a stored primary source are indistinguishable.

This is not a reason to stop; it is a thing to know before the guard is written,
and it is the sharpest instance of the principle in §4. Three moves fall out:

- **Count them.** How many of 550 are `recall`? Unknown, and unknowable from the
  aggregate. It may be zero, in which case this is a latent trap rather than a
  live one.
- **Carry `mode` into `LIBRARY.json`.** One field in `probe-library.mjs`, and the
  distinction becomes visible to every instrument.
- **Decide what the box does with a `recall` work.** Cite it and say plainly
  that the passage is reconstructed, or do not reach it at all. **That is a
  captain's decision, not the assistant's** — it is the boundary between what
  Amenti claims and what it does.

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

**A · Make the hall answer at all.** Slip #12. **Prefer B over the trim** — the
door list clears the wall on its own, so the trim is only needed if B is
deferred. Taking the trim first means editing the same line twice and degrading
190 glosses in between for no lasting gain.
- *Test:* open the hall, ask a question, get an answer — and
  `node probes/probe-hall-wall.mjs` exits 0.

**B · Build the door list — AND `linkMap` WITH IT.** 8 sections from
`SOURCES.json`, 52 rooms from `LIBRARY.json` in the rich form, a note that the
roster is name-searchable. `linkMap` must gain rooms and sections in the same
change, and `linkable()` must stop rejecting single-word room keys, or citations
die quietly on the page.
**Measured at 5,875 chars.** Build this INSTEAD of the trim in A, not after it —
it drops the prompt under the wall on its own, so the hall answers again and no
gloss is ever degraded. One change, nothing thrown away.
- *Test:* `probe-hall-wall` exits 0; the door list is under 6,000 chars; every
  section and all 52 rooms appear in it; and **ask a question that cites a
  single-word room — `brutus`, `apollo` — and confirm the citation is a working
  link, not plain text.**
- *Known cost:* for one release the hall knows the SHAPE of the corpus but not
  the individual documents — it can say what the briefs section covers, not
  which brief. That is why B and C belong in one push if the session allows.

**C · Two calls: choose the doors, then open them.** `find()` first, free, for
anything named.
- *Test:* a question naming a figure opens that room and no other. A question
  naming nothing still opens something, or says nothing aboard covers it.

**D · The coverage statement.** Built in from the first line. The surface exists
already — the box's `note` line prints `r.cited` and `r.degraded`. Add
`searched / opened / not opened` to what `ask()` returns.
- *Test:* every answer names how many entries were searched and how many opened.
  Ask something the corpus does not cover; the answer says so plainly.

**E · The substring guard.** A probe, not a promise.
- *Test:* plant a plausible but non-existent quotation in a test question; the
  answer does not reproduce it as a quote from the library.

**F · Scope the meaning to the lane.** The largest single saving — 3,251 chars.
- *Test:* a question about a figure does not carry the fleet's architecture
  doctrine in its prompt, and `probe-hall-wall` shows the drop.

**G · Carry `mode` into `LIBRARY.json`.** One field in `probe-library.mjs`.
Without it no instrument can tell a stored primary source from a passage
reconstructed by a model, and move E cannot be written correctly.
- *Test:* the register reports a mode for every work, and the count of `recall`
  works is a number rather than an unknown.

---

## 7 · WHAT THIS BRIEF DOES NOT KNOW

Stated so the next session does not mistake absence for absence of a problem.

- **`amenti-hall-box.js` HAS now been read** (31 Aug), and it resolved the
  mount question. Its own comment: *hall.html is the home; the others are
  contingencies, not plans.* It mounts to `#hall-main`, falls back to `#roster`,
  then to the top of `<body>` with a console warning. **So the engine's prompt
  is wrong** — it tells the model the visitor *has typed a question into ASK
  AMENTI on the arena page*, and the visitor is in the hall. One line, and the
  hall's whole ethic is not saying what it cannot stand behind.
- **The box has no case for `system_too_long`.** It special-cases 429 with a
  written sentence and prints everything else as *The hall could not answer just
  now: …*. So today's 413 reaches the visitor as a vague error rather than a
  hall saying something true. Worth a case of its own once #12 is understood.
- **The question log is an open item nobody has recorded.** The box keeps a
  local tally at `localStorage['amenti.hall.log']` and its header says a
  fleet-wide question register needs a Worker tube and is *deliberately NOT
  built here — recorded as an open item*. It is not on THE STANDING SLIP.
- **The box is STATELESS by ruling** — each ask stands alone, no conversation
  memory, *a visitor who wants a conversation has the souls for that*. Any
  follow-up behaviour in the new box reopens that ruling deliberately.
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

*Revised 31 Aug, same session: §3 repriced from `LIBRARY.json` rather than
estimated, the `recall` gap added to §4, and moves B and G rewritten. The door
list turned out cheaper and better than the estimate — build it instead of the
trim.*

*Opened 31 Aug 2026 for THE STANDING SLIP #13. Every number here was measured
against the live registers by an instrument that lifts the hall's own functions
rather than reimplementing them — because the first version of this measurement
was done by hand, looked authoritative, was never run against the real code, and
was wrong by 342 characters. If this brief and a register disagree, the register
is right and this has gone stale.*
