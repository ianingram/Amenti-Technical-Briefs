# BRIEF — THE SIGNET

### Ingram Manor LLC · 4 September 2026 · a model updated, because the hall was still running the old one

A soul does not need a room to bear a mark.

That sentence is the whole of this brief. It was already written down —
THE STANDING SLIP #61, 2–3 Sep: *"a room is not the unit of existence; it is
the unit of DEPTH."* On 4 September the hall was asked **who is Odysseus?** and
answered:

> Odysseus is not on the roster here.

He is on the roster. Rank 0.47, a Hero, 1250–1170 BC, seated at Ithaca, and
present in `ROSTER-INDEX.json` under the key `odysseus`. So is Homer, whom the
same answer also declared absent.

**The principle had been retired on paper and was still running in the code.**

---

## 1 · WHAT A SIGNET IS

A signet is a seal: a small mark that stands for a thing without being the whole
of it. A soul in this constellation can bear several, at different depths, and
none of them is a room.

```
  a DATE        2,043 of 2,043     places them in time; catches citations
  a SEAT        864                a coordinate the record supports
  a TERRITORY   747                "somewhere in here", never a point
  an OFFICE     1,718              what they were — shared with everyone of it
  a PERSONAL    34                 this sign is theirs alone
  an EDGE       111                who named them, in what work
  a ROOM        ~55                the deepest mark, and the rarest
```

Every line above is a legitimate state. The old model recognised only the last
one and read the other six as a backlog of 1,990 failures. The constellation
model reads them as 2,043 working nodes at varying depth — and **the signet is
the visible form of that depth.**

---

## 2 · HOW THE OLD MODEL SURVIVED IN THE CODE

Not through carelessness. Through an argument list.

```js
buildAnswer(hall, state, opened, coverage, degraded, doors, ship)
```

The hall's answer path is handed `HALL.md`, the counts, the rooms it opened, and
a coverage statement. **The roster is not among its arguments.** It never was.
`probe-roster.mjs` carries the law that made this so, and the law is correct:

> NEVER send this to a model. It is 57 KB of names.

So the model knew the ~55 rooms and the 106 documents, and nothing else. The
coverage block it is required to pass on ends:

> NOT opened: every other room and every other work. You did not see them and
> must not describe them.

Given that, the answer about Odysseus was the only one available. **The hall
conflated "no reading room" with "not on the roster"** — which is precisely the
old model, stated as fact to a visitor.

### The part that makes this the worst kind of failure

The false claim arrived wearing the honesty language:

> Telling you he might be tucked somewhere aboard would be the one fault this
> place was built to refuse.

It refused a fault it was not committing, and committed a different one in the
same breath. A discipline can be performed correctly and still point the wrong
way. **Where a page is proud of its scruples, the scruples are where to look
for the error.**

---

## 3 · THE FIX, AND WHY IT IS NOT A LIST

The law against sending the roster stands. What goes to the model is the
**verdict of a lookup** — only for names the question actually contains, longest
match first, four-character minimum.

```
"who is Odysseus?"
  → Odysseus (Hero, 1250 BC to 1170 BC) — seat Ithaca, no room opened

"tell me about Homer and Plato"
  → Plato (Philosopher, 427–347 BC) — seat Athens, marked ✧, room open;
    Homer (Writer, 800–750 BC) — place unrecorded, marked ✒, no room

"what is a spell?"
  → no name in this question matches any of the 2,043 souls. Absence may be stated.

roster unreadable
  → do NOT say any figure is absent. Say the roster could not be read.
```

**432 characters worst case, against a `SYSTEM_CHARS` budget of 20,000.** Less
than one percent of the prompt to retire the model that told a visitor Homer
does not exist.

The verdict is placed AFTER the not-opened line in the coverage block,
deliberately: that sentence produced the false absence, so the correction is the
last thing read.

---

## 4 · WHAT THE HARVESTER LEARNED ABOUT MARKS

The geography work of 3–4 Sep is where the tiering discipline was earned, and it
transfers directly to the signet.

### A mark must never overstate its own precision

The most common `Location` value in the roster is **"Southern Europe" — 334
souls, a continent.** A naive pin-map lies from its most common case, and it
would be the DEFAULT lie, told most often. So place became three marks that
cannot be confused at a glance:

| mark | what it claims | count |
|---|---|---|
| a pin, small and hard | here | 864 |
| a wash, large and soft, never a point | somewhere in here | 747 |
| nothing | no honest place, and the number is stated | 432 |

The same rule now governs the office glyph. An office says *one of 217 popes*;
a personal mark says *this sign is his*. Drawn alike, the map would assert those
are the same kind of fact. They are drawn differently — the personal brighter
and ringed — for exactly the reason a wash is not a dot.

### A confident wrong mark is worse than no mark

**FOUND BY ATTACK, 4 Sep.** The gazetteer matcher kept the highest-population
city for each name. For a roster of the ancient and medieval world this is
catastrophic:

```
  Averroes    → Cordoba, ARGENTINA        (not Spain)
  Al-Ghazali  → "Tus" → TUCSON, ARIZONA
  John Cabot  → Venice, OHIO
  Cortes      → Medellin, COLOMBIA
  Moses       → Goshen, INDIANA
  Sparta      → Sparta, TURKEY
```

Measured against the roster's own `Region` column — a field independent of
`Location`, and therefore able to arbitrate — **119 of 899 pins, 13%, stood
outside the region the record assigns them.** Every count under the map was
correct while the map was wrong.

The fix was not a better guess. A candidate inside the soul's region wins;
population breaks ties only within it; and **when a region is known and nothing
of that name lies in it, the soul falls through to unplaced and is reported.**
13% → 1%. Pins fell from 901 to 864, unplaced rose from 191 to 228. That is the
honest cost of refusing to guess, and it is cheap.

### The register can supply its own scale

The map's apertures are not 10/50/200. They are the periods the sky register
actually contains, measured from the file:

```
  Jupiter due-east      6 y    830 events, gaps 5–7
  great conjunction    20 y    248 events, gaps 18–21
  Uranus               42 y    117 events, gaps 41–43
  Halley               76 y     48 events, gaps 62–79
```

Neptune's 82 was dropped — four years from Halley's 76, and two buttons doing
one job is a worse instrument. The outer-planet gathering's 179 was dropped
because it is a **median, not a period**: its gaps run 40 to 1367 years, and
offering it as an aperture would dress noise as a cycle.

### A mark may sit only where the record puts it

The sky is computed at Giza, so the Giza diamond is honest: it is the OBSERVER,
not the event, and the label says *computed at giza*. Halley is not, because
`EVENTS.csv` carries no place and a comet is seen from the whole earth — so
Halley sits in a band declared as not-the-earth. Jupiter's return line traces
Giza's own latitude and closes on the pyramids at each rising, and it is
labelled **"a count, not a position"**, because at a register whose resolution is
the year there is no honest longitude to draw.

---

## 5 · THE MODEL, UPDATED

THE STANDING SLIP #61 named the next move and marked it optional:

> make graph-enrichment a VISIBLE layer — a roomless soul, when opened, shows
> what the constellation knows instead of "no room yet."

**It is no longer optional.** On 4 Sep the absence of that layer caused the hall
to deny two souls it holds. The revision:

- **A soul is answerable at every depth.** Dated, seated, marked, cited, roomed
  — each is a state the hall can speak from. "No room yet" is not an answer; it
  is a refusal to read five registers that are already built.
- **The hall must be able to tell three states apart:** aboard with a room,
  aboard without one, and not aboard. Only the third licenses a claim of
  absence, and an unreadable roster licenses none.
- **The vocabulary matters.** "ABOARD, but NO room has been opened" is still the
  old model — an absence with an apology attached. The signet form names the
  depth a soul HAS: *a Hero of the Bronze Age, seated at Ithaca, marked ⚔, whose
  room is not yet built.*
- **Derived is not read.** A seat matched from a gazetteer and an office
  inferred from a title string must not arrive in the same voice as a quoted
  passage. The coverage block already separates opened from not-opened with
  care; the signet needs its own framing — *the register says*, not *the text
  says*.
- **The mention graph is thin and must say so.** 7 authors, 111 edges. It will
  fire rarely and unevenly, and a layer that is silent four times in five should
  announce its own coverage rather than let silence read as absence.

---

## 6 · WHAT WOULD HAVE CAUGHT IT

Nothing did, for as long as the hall existed. The conflation was invisible
because every prior test asked about a figure who HAD a room.

**A guard exists now** — `probes/probe-map.mjs`, 18 checks on the map's honesty,
including the Region tripwire that fails above 3%. It found two dead things on
its first run: a chronometer track whose draw call was never wired, and a footer
that said "seats" while counting souls.

The hall wants its equivalent: a probe that asks the answer path about a soul
with no room and fails if the reply contains the word *not*. One name would have
done it. **Odysseus would have done it.**

---

*A room is the deepest mark and the rarest. The other six are not its
antechamber — they are marks in their own right, and a hall that cannot read
them is a hall that will tell a visitor Homer never existed.*
