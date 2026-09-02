# BRIEF · ASK AMENTI
**The surface, and the three things it does that a chatbot does not · Ingram Manor LLC · 2 September 2026**

Written from the shipped `amenti-hall-box.js` (28,027 bytes), `amenti-hall.js`
and `amenti-timeline.js`. Where this brief and the code disagree, the code is
right and this has gone stale.

> **THE ENGINE FINDS THE WORDS. THE BOX DECIDES WHAT A READER IS ENTITLED TO
> BELIEVE ABOUT THEM.** That division is the whole design. `amenti-hall.js`
> opens rooms and returns an answer with passages attached; the box renders it,
> and on the way it does three things no chat surface does: it CHECKS every
> quotation against the text that was actually fetched, it PRINTS what was read
> and what was not, and it PLACES the reader in time. None of that is styling.
> Each one is a claim being made checkable at the last possible moment.

---

## 1 · WHAT IT IS

A single script, mounted into `hall.html`. It owns the input, the search, the
rendering and the verification. It owns no knowledge: every fact it shows comes
from a register or from the engine.

**SEARCH FIRST IS A SHIPPED RULING, NOT AN OPTIMISATION.** Typing searches the
registers with no model call. Only Enter, on something that reads as a question,
spends. A visitor who types `caesar` gets the roster; a visitor who types
`what did Caesar write about crossing the Rubicon` gets the hall. The cost of
the second is real, so the box refuses to incur it by accident.

**AND IT IS STATELESS BY RULING.** Each ask stands alone. There is no thread, no
memory of the last question, no accumulating context. That is a constraint the
box enforces rather than a feature it lacks.

---

## 2 · IT OWNS NONE OF ITS DATA

**EVERY FACT ASK AMENTI SHOWS BELONGS TO ANOTHER SURFACE.** That is the most
important structural thing about it and the easiest to miss, because the hall
looks like a self-contained page.

```
ROSTER-INDEX.json   written by probe-roster        — Page1's roster, and find()
LIBRARY.json        written by probe-library       — the reading room's shelf
library/{room}.json + the .md bodies               — the reading room's texts
SOURCES.json        written by the source walk     — the whole ship's index
HALL.md             authored by hand               — the ship's meaning
HALL-STATE.json     written by probe-hall          — every number it may state
EVENTS.csv          lifted out of Page2, 1 Sep     — the historical anchors
```

The box holds no history, no dates, no citations and no counts of its own. It
is a lens. **THAT IS WHY IT CAN BE TRUSTED**: there is no second copy to drift,
and anything it says wrongly is either a register that is wrong or a rule in the
prompt that is wrong — both of which are findable.

**And it is why it breaks in interesting ways.** Three of the faults found in
two days were not the hall's at all:

- Page2's gloss said *microphone* while the file held a double helix, so the
  hall said the site has no timeline. It reasoned correctly from what it had.
- The flagship's nav lived only in Page1's markup, so the hall sent a visitor
  to another repo instead of the tab beside them.
- Josephus was dated 37 BC in `names.csv` — a 137-year life — and the hall
  placed him beside Cleopatra, who died 67 years before he was born.

**A surface that answers from the ship's own registers is a continuous audit of
whether those registers are true.** It has no opinion and no memory; it simply
uses what is written, and when what is written is false the answer comes out
visibly strange. That is worth more than the feature.

---

## 3 · THE QUOTE GUARD

The largest thing built into the box, and the one that turns a promise into a
test.

### The promise, and why it was not enough

`buildAnswer` tells the model to quote, and to quote **only** from the text
handed over that turn. The reason is the citation policy exactly:

> The model knows famous passages from these authors in translations that are
> NOT the edition aboard. A remembered line printed under a real SOURCE line
> attaches a genuine citation to words the library does not contain. **That
> makes the edition a lie** — which is precisely what the citation campaign was
> fought to prevent, arriving through the front door.

Until 1 September nothing checked that the rule was obeyed. It was the only rule
on the ship with a sentence instead of an instrument.

### Three states, because two would be dishonest

```
verified    the span is verbatim in the TEXT fetched this turn
from note   verbatim in a LIBRARIAN'S NOTE instead — a real distinction
unmarked    no match. NOT branded false.
```

**THE THIRD STATE IS THE ONE THAT MATTERS.** A quote may be legitimately elided,
or drawn from something not returned to the surface. So an unmatched span gets
no colour and no accusation, and the tally reads *not matched to anything
fetched* — never *invented*.

**THE COLOUR IS EARNED, NEVER CLAIMED.** A false quotation painted as verified
would be worse than no colour at all, because the colour asserts provenance the
model cannot vouch for. The page only ever tints what it has matched itself.

The second state earns its place from a real event: on 31 August the hall wrote
*as the text puts it* about a line that was in the librarian's note and not in
the slice. True words, one layer removed, and nothing distinguished them.

### And the tally speaks even when nothing is wrong

`1 quotation · 1 checked against the text` prints on a clean answer. **A guard
that speaks only on failure leaves a reader unable to tell it ran.**

---

## 4 · TWO LIVE FALSE NEGATIVES, AND WHAT THEY TAUGHT

Both surfaced within two questions of the guard shipping. Both were correct
quotations reported as unmatched. Neither was the guard's logic.

### ① The footnote marker

The hall quoted Josephus — *the first of the twenty-four courses* — and it came
back unmatched. Whiston's edition carries an apparatus mark mid-phrase:

```
from the first of the twenty-four [1] courses
```

The hall quoted it cleanly, as any editor would.

### ② The terminal punctuation

```
source   ...descended all along from the priests; and as nobility
quoted   ...descended all along from the priests.
```

Every word identical. The source runs on with a semicolon; the hall closed the
clause with a full stop.

### The rule both produced

> **THE WORDS ARE THE AUTHOR'S. THE APPARATUS AND THE PUNCTUATION AT THE
> BOUNDARY ARE NOT.**

A bracketed number is the printer's. A closing full stop where the source has a
semicolon is the quoter's. Both are stripped before comparing, and **neither
loosens what counts as verbatim** — the interior must still match exactly. A
substituted word, an elision, or a remembered line still fails.

**And the guard behaved well both times.** Had it said *invented* rather than
*not matched*, a correct quotation of Josephus would have been branded a lie by
a semicolon. The three states were not caution; they were the difference
between a useful instrument and a libellous one.

Ten attacks stand behind the current version: verbatim, line-breaks, footnotes,
edited terminal punctuation and straight quotes all verify; elision, a
substituted word, a remembered line, a span of pure punctuation and an HTML
injection all fail, and the injection stays escaped.

---

## 5 · READ FROM — provenance in front of the reader

Beneath every answer: the works opened, their editions, and what was searched
and not read.

**NOT BEHIND A TAB.** Amenti's claim is that it SHOWS where the words came from.
A provenance a reader must click to see is one most readers never see. Present
beats available.

**NOT INLINE EITHER.** Livy's source line is 145 characters; one of those after
every quotation and the prose disappears. So the split scholarship settled on
long ago — a short marker in the sentence, the full edition beneath.

**A WORK OPENED AND NOT QUOTED IS STILL LISTED**, marked *in the room, not read
this turn*. The hall may read four works and use one; saying which is the
coverage principle at the scale of a single answer.

**And the register is a third kind of source.** Asked about the ship rather than
about history, the block reads *the ship's own register · the surfaces · 10
document descriptions · SOURCES.json, authored by hand*. That branch was
missing for a day, and the block said *none read* while ten descriptions had
just been shown — the coverage line contradicting what had happened, which is
the one failure it exists to prevent.

---

## 6 · WHERE THE READER IS IN TIME

The box builds the timeline **while the answer is being read** and never on the
click.

The hall has a second state: a click anywhere that is not a control hides the
reading and leaves the image. Because the timeline is already built, the click
REVEALS it rather than loading it — which says something a summoned panel
cannot: **the position was always true.** You were reading Josephus at AD 37–100
the whole time.

The first opened room wins; the router ranks by relevance, so room one is the
question's subject.

**A FIXED 200-YEAR WINDOW, CENTRED ON THE MIDPOINT** of the first opened room.
Fixed so the scale never changes: a reader learns what a century looks like once
and every answer afterwards reads against the same ruler, so Brutus at 509 BC
becomes directly comparable to Josephus at AD 37. Midpoint rather than birth,
because centring on birth shows everything AFTER a figure and nothing before —
losing the world they were born into, which is half of what makes it work.

**ORDERED BY DEATH YEAR, BECAUSE PAGE2 IS.** The helix computes
`anchorYear = !isNaN(effectiveDeath) ? effectiveDeath : birthYear`, and the
timeline matches it exactly, fallback included. Not because ordering by death
reads better — **because the two views must agree.** Scroll to a year here and
the same figures must sit where the helix puts them.

**Wireframe bars over a scrim**, because this sits on a photograph and solid
bars would be opaque blocks on it. Names inside the bar above ~130px, outside
below. Events from `EVENTS.csv` as ticks on the axis, never among the rows — a
moment is not a span, and in a row it would read as a very short life. Both axes
scroll: time across, population down, neither capped.

**Colour marks what is clickable**: the figure being read, then rooms, then
roster-only. A room's bar opens its reading room.

**AND IT FAILS COMPLETELY QUIETLY.** No rooms opened, an unplaceable key, a
register that will not load — the timeline simply is not there, and the bare
state is what it was before. *A timeline is a courtesy, never a dependency.*
Nothing about the reading depends on it.

---

## 7 · THE LINKS, AND ONE RULE THAT WAS WRONG TWICE

**THE WORK IS SPLIT, AND THE BRIEF SHOULD SAY SO.** `linkMap` is built by the
ENGINE (`amenti-hall.js`) and decides WHAT may be linked; `linkify` in the box
decides WHERE it appears in the prose. The rule below lives in the engine. It is
here because a dead citation is a surface fault to the reader whichever file
caused it, and because the rule has been wrong twice.

**IT REQUIRED PUNCTUATION** — a hyphen, underscore or dot — written after a test
render linked the word "hall" inside ordinary prose. Right for that question,
and it silently dropped `page2`. The hall named Page2 correctly and the citation
was dead text.

**THEN "MEMBERSHIP, NOT SHAPE" WAS SETTLED IN A BRIEF AND WAS ALSO WRONG.**
`hall`, `glossary`, `reader`, `readme` and `todo` are all genuine ids, so
membership admits every one and the original fault walks back in. **A settled
decision is only as good as the run that tests it.**

The rule is now BOTH: in the register, AND not shaped like an ordinary word. Of
51 bare ids aboard, every one worth linking carries a digit — `page1`, `page2`,
`game01`, `probe2` through `probe21` — and no ordinary word does.

Nav labels link UPPERCASE only, which is the same discipline: `INTERFACE` links,
*the interface was rebuilt* does not.

---

## 8 · WHAT THE BOX REFUSES TO DO

**It takes nothing from the URL.** `?q=` was built, tested nine ways and
reverted the same night. The captain's reason is the better one: **the visitor
must be the source.** A seeded question is the site speaking through their
hands, and a link that arrives already answering proves the demo works rather
than that the product does.

**It never renders the model's output as markup.** Everything is escaped, then
linked, then given emphasis, then verified — in that order, so the guard runs
last and on already-escaped text.

**And it makes no claim it has not checked.** Every tint, every count, every
line in the provenance block is computed from what the engine returned. The box
does not know any history.

---

---

## 9 · WHAT WATCHES IT

Two instruments, and each states plainly what it cannot see.

**`probe-hall-wall.mjs`** lifts the engine's own `doorsText`, `sectionText`,
`pickRooms` and `buildAnswer` out of the shipped file and measures every shape
of the prompt against the proxy's 20,000-character wall. It exists because the
hall was silent on every question for an unknown period: the Worker refuses an
overrun with a 413, not a shorter answer. See
`BRIEF-THE-WALL-AND-THE-PROMPT.md`.

**`probes/probe-timeline.mjs`** asks the claim rather than the implementation —
*can a reader be placed in time?* — in the four places it can quietly stop being
true: every room placeable, the alias join holding, the registers the shape the
surface expects, and the renderer still handling the eternals and the living.
It runs in `hall.yml` immediately after `probe-roster` writes what it reads.

**NEITHER CAN SEE THE PAGE.** No browser, so neither can tell you whether the
axis stays put while the rows scroll, whether a label survives the pyramid's lit
face, or whether a quotation reads well. Both say so in their own output. **The
two live false negatives in §4 were found by asking the hall a real question**,
which is the half no probe can do.

---

## 10 · WHAT IS OPEN

**`SKY.csv` IS NOT READ.** 1,342 planetary alignments were computed from JPL's
DE422 at Giza on 1 Sep, verified against orbital theory and described in the
register — and `amenti-timeline.js` fetches the roster and `EVENTS.csv` only.
The anchors exist and nothing draws them.

**The timeline has never been seen.** Built, probed and landed; no eye has
looked at it in a browser. `probe-timeline` says the data supports the drawing
and states plainly that it cannot see the drawing. The axis is a separate
scrolling layer kept in step by a transform, and that is where a fault is most
likely.

**The verified colour is not yet distinguished by anything but hue.** A reader
who cannot see colour gets the tooltip and the tally and no tint.

**And `?v=1` is cache-busting that never busts.** The header is GitHub's
`max-age=600`; the query string never changes so it does nothing. A probe
comparing each `<script src="...?v=N">` against the file's git hash is the only
thing that ends it. THE STANDING SLIP #26.

---

## 11 · THE SHORT VERSION

- The engine finds the words; the box decides what a reader may believe.
- Search first: only a genuine question spends.
- **Quote only from the text handed over — and now something checks.**
- Three states, because branding a correct quotation false is the worse error.
- The words are the author's; the apparatus and the boundary punctuation are
  not.
- Provenance beneath the answer, never behind a tab.
- A work opened and not quoted is still listed.
- The timeline is built while you read and revealed when you click.
- The visitor is the only source.

---

**Companion briefs.** `BRIEF-THE-WALL-AND-THE-PROMPT.md` — how the engine
assembles what it sends, and why. `BRIEF-WHAT-A-SOURCE-MUST-BE.md` — the
citation policy the quote guard enforces. `BUILD-THE-TIMELINE.md` — the
timeline's specification and the four things the roster's data does to a naive
drawing. `BRIEF-THE-DESCRIPTION-STAYS-WHERE-THE-TRUTH-WAS.md` — the fault §2
describes this surface exposing.

---

*Written 2 Sep 2026, two days after the box could not answer at all. Every
behaviour described was tested against the shipped file; the two false negatives
in §3 were found by asking the live hall a real question, which is the half no
probe can do.*
