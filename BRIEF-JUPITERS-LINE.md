# BRIEF — JUPITER'S LINE

### Ingram Manor LLC · 5 September 2026 · one mark, three failures, and a rule about permanence

There is a dashed amber line across the map at **29.98°N**, Giza's own
latitude, running the full width of the world. A ♃ travels it. Every five to
seven years the sign reaches the pyramids, turns white, and the ring closes:
Jupiter has risen due east over Giza again.

It is the smallest thing on the surface and it has been wrong more times than
anything else. That is why it is worth a document.

---

## I · WHAT IT IS, AND WHAT IT REFUSES TO BE

**It is a clock laid on the ground.** The line is real geography. The arrivals
are real years, 830 of them, computed at Giza and held in `SKY.csv`.

**The sign's longitude means nothing.** Jupiter's sub-planetary point sweeps
the entire globe every day. At a register whose resolution is the YEAR there is
no honest longitude to draw, and computing one from orbital elements would put
a second, worse sky beside the DE422 one already aboard. So the travelling
sign is a **progress bar between two dated arrivals** and not a position, and
the label says so in those words:

> **A COUNT, NOT A POSITION.**

**And Giza is the OBSERVER, not the event.** This is the same distinction that
keeps Halley in the sky band rather than at a coordinate. A conjunction happens
in the sky and belongs nowhere on the earth; what belongs at Giza is the place
it was computed from. The one honest coordinate for a sky event is where
somebody stood to see it.

---

## II · THREE FAILURES IN ONE DAY, AND NOT ONE OF THEM A BUG

### drawn at a quarter opacity

`stroke-width: .3`, `opacity: .28`, dashes of one pixel in four. An amber
hairline on a dark map, below the threshold of visible on most displays. It
rendered exactly as written and **was reported as missing from the
application** — while its own label sat legible above it, which made the
invisible line read as a fault rather than a faintness.

> **A LINE THAT CARRIES A CLAIM MUST BE VISIBLE ENOUGH TO BE DOUBTED.**

### absent past the end of the register

The register's last Jupiter rising is **AD 2022**. The map opens at **2026**.
The drawing needed a rising before AND after the current year, so at the
default view there was no *next*, and nothing was drawn.

The refusal was correct — extrapolating a rising the register does not hold
would be inventing sky. **But it refused in silence**, and a reader landing on
the default view saw nothing and concluded the feature was gone. A correct
refusal that looks identical to a broken feature is a design fault, not a
virtue.

### and then the fix that was still wrong

The first repair added a note explaining the absence: *"♃ last rose due east
over giza in AD 2022 · the register ends there."* Honest, and still wrong,
because the captain said the obvious thing:

> *"the Jupiter line is the default view"*

**THE LINE IS GIZA'S LATITUDE.** That is geography. It is true in 2026 and in
3000 BC and in every year the map can show. Only the TRAVELLING SIGN is a
count, and only the sign needs a next arrival to travel toward. The whole mark
had been made conditional on the one part of it that is contingent.

> **DO NOT MAKE A PERMANENT FACT CONDITIONAL ON A PASSING ONE.**
> The line always. The sign when there is something to count. The note when
> there is not.

---

## III · WHAT THE THREE HAVE IN COMMON

None was wrong data. None was broken code. Every one was **a correct thing that
a reader could not reach** — too faint to see, or refused without saying so, or
explained instead of shown.

That is a class of fault no file probe can catch, and it is why
`probes/hall-probe.js` exists: it opens the page, counts what actually
rendered, and flags anything drawn below 0.2 opacity as *drawn, and arguably
not there*. It found the third failure itself, in one line:

```
X  nothing drawn for: Jupiter line  (.mp-return)
```

The general form, which GLOSSARY now records as the third of the water
between's four shores:

> **A FEATURE THAT EXISTS, IS WIRED, AND CANNOT BE REACHED READS TO A VISITOR
> AS ABSENT — AND THAT IS WORSE THAN ABSENT, BECAUSE NOBODY LOOKS FOR IT
> TWICE.**

---

## IV · WHY THE LINE IS WORTH THE TROUBLE

It is the only mark on the map that is **neither a soul, an event, nor a
place**. It is a period — a thing that recurs — and it is the one instrument
that makes the register's own clock visible on the ground.

It also anchors the ladder everything else is measured against. The apertures
are not 10, 50, 100, 200 but **6, 20, 42, 76**: one Jupiter, one great
conjunction, one Uranus, one Halley — periods measured out of `SKY.csv` rather
than out of the decimal habit. The smoulder of an event is counted in comet
passes for the same reason. Jupiter's line is where that clock is legible
rather than merely used.

**And it ends.** At AD 2022 the register stops and the sign stops with it. The
map does not compute the next rising, though it easily could. What it does
instead is say where the record runs out — which is the whole argument of this
ship, drawn as one dashed line across the top of Africa.

---

*Related: `probes/hall-probe.js` · GLOSSARY, `the water between` and its four
shores · SLIP #64 (the map surface), #71 (the smoulder). The apertures and the
comet passes both descend from the same register, `SKY.csv`, 1,604 events
computed at Giza.*
