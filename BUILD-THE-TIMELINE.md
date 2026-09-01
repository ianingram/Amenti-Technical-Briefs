# BUILD · THE TIMELINE
**Where a reader stands in time, and what stood beside them · Ingram Manor LLC · 1 September 2026**

A build document, not a brief. Every number below was read from
`ROSTER-INDEX.json` at `2026-09-01T07:59:29Z` and `LIBRARY.json` on the same
day. Where this and a register disagree, the register is right and this has gone
stale.

> **THE CAPTAIN'S REASON, AND IT IS THE WHOLE SPECIFICATION:** *you would be
> surprised how lost most people are in time.* They have no clear sense of where
> Lincoln stands against Caesar against Henry II. The site already fixes that
> for anyone who reaches Page2's helix. **Nothing fixes it for a reader in the
> middle of an answer**, which is the moment they most need it.

---

## 0 · WHAT IS ALREADY TRUE

**This is not a data-collection project.** Everything it needs exists.

```
souls on the roster                        1,011
placeable — BOTH a birth and a death year  1,011      100%
with only one date                             0
rooms in the library                          52
rooms that join to a soul                     52      100%
earliest                                 -10,000
latest                                     2,026
```

Two things were fixed on 1 Sep to get here, and both are done:

**The dates reached the index.** `names.csv` holds them and is 548 KB, which no
surface may load. `probe-roster.mjs` now writes `b` and `d` into
`ROSTER-INDEX.json` — two integers a soul, negative for BC so they sort with no
parsing. The index went from 58 KB to 77 KB and the browser already holds it.

**The join was never broken.** It was reported as twelve unmatched rooms on
1 Sep by checking only the primary key. `KEYS.json` carries alternates and
`probe-roster` already writes them — `lincoln` alongside `abraham-lincoln`,
`einstein-albert` alongside `albert-einstein`. **All 52 rooms resolve.** No work
was needed and none should be done.

---

## 1 · WHAT IT IS

Two things, and they must not be conflated. Only the second is the reason to
build.

**A BROWSABLE TIMELINE** — an object a reader can move through. Useful. It is
also what everybody means by "a timeline", and it is the version that will get
built by default if nobody says otherwise.

**A POSITION** — *you are here*. It appears with an answer. The hall opens
Brutus's room; the timeline moves to 509 BC and shows who else was alive that
year. **This is the one that teaches**, and it is the one the captain described.

The same component does both. Only the second needs the engine to hand it
anything, and that hand-off already exists: `ask()` returns `opened`, which
carries the room key, and the room key resolves to a soul with dates.

**Where it lives:** a shared script in the shape of `library.js` — *not a page,
never visited directly, mounted by whatever page includes it*. It surfaces
first in the hall because that is where the answers are. Building it into
`hall.html` would prevent it from ever appearing in the reading room, which is
arguably where a reader deep in Livy most needs it.

---

## 2 · THE READING IT PRODUCES

Computed live, not illustrative:

```
509 BC — the year Brutus expelled the Tarquins

   Gautama Buddha    -563 to -483
   Confucius         -551 to -479
   Brutus            -545 to -509
   Sun Tzu           -544 to -496
   Leonidas          -540 to -480
   Heraclitus        -535 to -475
   Aeschylus         -525 to -456
```

**That is the product.** A reader who has just watched Brutus take the knife
from Lucretia's wound, and now sees that the Buddha and Confucius were alive
that year, has had a period reorganised in one glance. It cannot be got from
reading Livy, and it needs no citation — it is a fact about the ship's own
roster.

---

## 3 · THE FOUR THINGS THE DATA WILL DO TO A NAIVE BUILD

Each of these is measured, and each will produce a visibly wrong screen if it is
not handled.

### ① The density spans two orders of magnitude

```
-1000     1 alive          1453    11
 -509    11               1776    38
  -44     7               1865   100
  476     4               1945   325
 1000     1               2000   298
```

**A linear axis is unusable.** One soul at 1000 AD against 325 in 1945 means
antiquity is a sliver and the twentieth century is the chart. And a chart sized
for antiquity is four dots in an acre of white.

**The display must change behaviour with density: NAME THEM WHEN THEY ARE FEW,
COUNT THEM WHEN THEY ARE MANY.** At 509 BC, seven names that rearrange a
reader's head. At 1945, *325 souls, 156 in North America* — because listing them
teaches nothing.

### ② A death year of 2026 means LIVING

**200 souls of 1,011 carry `d: 2026`.** Stallone, Putin, Spielberg, Steinem.
That is not a death date; it is the roster's way of saying *still here*.

**A timeline that draws a death mark at 2026 states something false about a
fifth of the roster**, including people who could object. Treat `d === 2026` —
or better, `d >= current year` — as an open span, drawn differently and never
labelled as an end.

### ③ Forty-five souls are eternal

`b: -10000, d: -3000` — Apollo, Isis, Prometheus, Enki, Minerva, Mars. **A
7,000-year span** that will dominate any axis it is drawn on.

They are not misdated. They are a different KIND of entry, and a timeline that
treats a god as a person with a very long life is making a category error the
roster did not make. Either give them their own band or leave them off the time
axis entirely — but decide, do not let the renderer decide by accident.

### ④ Duplicate souls will appear twice at the same point

`Gautama Buddha` and `Buddha`, both `-563 to -483`. `Augustine of Hippo` and
`Saint Augustine`, both 354. **Invisible in a list, glaring on a chart** — two
marks at one point, and a reader will ask which is which.

Seventy-six date-pairs are shared by two or more souls. Most are legitimate
contemporaries; a handful are the same person entered twice. **The dedupe
belongs in `probe-roster`, not the renderer**, which already reports colliding
slugs and would only need to report identical name-and-date pairs beside it.

---

## 3b · THE FORM, DECIDED 1 SEPTEMBER

Settled with the captain after two mockups. Recorded because §6 used to say
strip-or-overlay was undecided — it is decided, and by something better than
either.

### It is already there. The click only takes the reading away.

The hall has a second state: clicking anywhere that is not a control, a drag or
a text selection toggles `body.scene-bare`, which hides `#hall-main` and shows
a hint — *click anywhere to bring the hall back*. Escape restores it, and so
does focusing a field.

**THE TIMELINE BUILDS BEHIND THE READING, WHILE YOU READ.** It is not summoned
and it does not load on click. When the reading goes, the timeline is revealed,
which says something a summoned panel cannot: **the position was always true.**
You were reading Josephus at AD 37–100 the whole time.

Because `scene-bare` hides `#hall-main` entirely, the timeline CANNOT live
inside it. It mounts as a sibling and appears the way `#scene-hint` does.

### A fixed 200-year window, centred on the midpoint

**FIXED, so the scale never changes.** A reader learns what a century looks
like on that screen once, and every answer afterwards reads against the same
ruler — Brutus at 509 BC and Josephus at AD 37 become directly comparable,
which is the whole point and which a window sized to each figure would quietly
destroy.

**CENTRED ON THE MIDPOINT of the first opened room**, not on birth. Josephus
centred on his midpoint runs roughly −32 to 168: Actium and Cleopatra at the
left edge, Tacitus and Plutarch at the right. Centred on BIRTH it would run
37–237 — everything after him and nothing before, losing the world he was born
into, which is half of what makes the reading work.

**The first opened room, when several open.** The router ranks by relevance, so
room one is the answer's subject. Rooms in other centuries fall off-screen, and
that is honest — the coverage line already states which were opened.

### Ordered by DEATH year — the ship's convention, and it is enforced

Page2 computes `const anchorYear = !isNaN(effectiveDeath) ? effectiveDeath :
birthYear;` — death, falling back to birth only when there is none.

**MATCH IT EXACTLY, including the fallback.** Not because ordering by death
reads better, but because **the two views must agree**: scroll to a year here
and the same figures must sit at the same place on the helix. Order by birth
and they diverge subtly, which is the drift this yard spends its time removing.
The roster has zero souls without a death year today; use the fallback anyway,
so the day one appears the two views still agree.

Ordering by death makes the staircase run by ENDING, with long lives reaching
backwards — a different picture from ordering by birth, and the true one.

### Wireframe bars, names inside

Outlined rectangles, not filled. **This sits over a photograph**: solid bars
would be opaque blocks on the image, outlines let it through. Hierarchy comes
from stroke — the figure being read heaviest, rooms next, roster-only thinnest.

The name sits INSIDE the bar, so the bar is its own label and the row reads as
one object. Dates at the trailing end where there is room.

- **Below roughly 130px the name goes outside.** A twenty-year life in a
  200-year window is about 60px and will not hold "Alexander the Great". Two
  treatments in one view, which reads fine if the outside labels sit at a
  consistent distance.
- **Text over an image needs a scrim.** Outlined bars put their labels straight
  onto the photograph; over a dark sky that is fine, over a lit pyramid it is
  not. `hall.html` already has a `.veil` element — use it rather than adding
  a plate behind every row.

### Events on the axis, people in the rows

The 488 anchors in `EVENTS.csv` sit as tick marks along the time axis, NOT among
the bars. They are a different kind of thing — a moment, not a span — and
mixing them into the rows makes them read as short lives.

### BOTH AXES SCROLL

**Horizontally is time.** The window stays 200 years wide and moves; that is
what makes the fixed span pay off, because everything you slide past stays
comparable to everything you have seen.

**Vertically is population, and it is not capped.** This RETIRES the compromise
in §3① — "name them when they are few, count them when they are many" was
forced by a fixed frame. With vertical scroll, 1945 gives 325 rows and the
reader scrolls them. **The crowding becomes the information.**

Four things fall out of scrolling, and they are the ones discovered halfway
through a build if they are not decided first:

- **The axis must stay put.** Scroll down through 300 people and the years must
  remain visible, or the reader is looking at bars with no idea when. A sticky
  header — which means the axis cannot simply be another row in the SVG.
- **The anchor can be scrolled away from.** Drag three centuries off and the
  figure being read is gone with nothing to return to. Either pin its bar to
  an edge when it leaves the window, or give a way back.
- **The two scrolls interact.** Sliding sideways changes the population, so the
  vertical extent changes underneath the reader. Someone at row 200 in a
  crowded century, sliding into a thin one, has scrolled off the end.
  **Clamp, do not blank.**
- **The whole roster is −10000 to 2026.** At mockup scale that is roughly
  145,000px of rail — a great deal of dragging to cross an empty millennium.
  A jump (decade, century, era) probably matters more than smooth scroll for
  distance, with the drag for reading.

### The window readout is load-bearing

The mockup carried a line reading *ad 6 — ad 206 · 200 years*. Without it,
sliding through twelve thousand years is disorienting. It is not decoration.

---

## 4 · THE MOVES

**A · The position, in the hall.** With an answer, show where the opened rooms
sit and who else was alive. `ROSTER-INDEX.json` is already loaded for `find()`;
`EVENTS.csv` is a second small fetch. Built while the answer renders, revealed
by the click — never loaded on click. See §3b for the form.
- *Test:* ask about Brutus; click the background; the window is centred on his
  midpoint and names the Buddha, Confucius and Sun Tzu, with the events of that
  span on the axis.

**B · Handle the four of §3.** Density-dependent display, the living, the
eternals, the duplicates.
- *Test:* the same component renders 509 BC and 1945 without either being
  unreadable; no death mark is drawn for a living soul; no god sits on the
  person axis; no soul appears twice at one point.

**C · Dedupe in `probe-roster`.** Report souls sharing a name-stem and an exact
date pair, the way it already reports colliding slugs.
- *Test:* the probe names `Buddha`/`Gautama Buddha` and
  `Augustine of Hippo`/`Saint Augustine` without being told to look for them.

**D · The browsable form.** Only after A. It is the easier build and the less
useful one, and doing it first would make the position an afterthought on it.
- *Test:* a reader who knows no names can move through time and arrive
  somewhere.

**E · The mount, done properly.** A shared script, not a section of
`hall.html` — so the reading room can carry it later without a rewrite.
- *Test:* it renders in the hall and in one other surface with no change to the
  component.

---

## 5 · WHAT THIS DOES NOT DO

**It is not an events timeline.** Babylon falling, Constantinople, the
destruction of Jerusalem. Those need witnesses aboard to be citable, and 52
rooms of 1,011 souls is 5% — three of four test events had a witness with a
room, which is the *good* case. **An events strand is downstream of the library,
not parallel to it.** The move that unblocks it is more rooms. THE STANDING SLIP
#32.

**It is not Page2's helix, and must not compete with it.** Page2 already draws
time as a spiral with two strands, and it is the better object. This is the
*locator* — a small, honest statement of where a reader currently stands, which
should point AT the helix rather than reimplement it. `INTERFACE` is the label,
and the hall already knows it.

**And it makes no claim it cannot source.** Every figure it places is placed
from the ship's own roster. It states no fact about history it did not read from
a register.

---

## 6 · SETTLED — it was neither strip nor overlay

This section asked strip-or-overlay and said it could not be decided from the
data. Correct, and it was decided on 1 Sep by the captain describing what he
wanted to see: **the timeline is already there, behind the reading, and the
click takes the reading away.**

Neither answer was right. A strip would be visible while reading and become
furniture; an overlay would have to be summoned and would mostly not be. What
was wanted was a THIRD thing — part of the scene rather than part of the
reading. See §3b.

**What is still open**, and both are build decisions rather than design ones:
whether distance is crossed by dragging or by a jump control, and where the
anchor goes when the reader scrolls away from it.

---

*Written 1 Sep 2026 from `ROSTER-INDEX.json` generated the same morning — the
first version of that file able to place a figure in time, and the reason this
document is a build rather than a proposal.*
