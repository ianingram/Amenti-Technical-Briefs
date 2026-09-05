# FINDING — THE SQUARING OF THE LAKES

### Ingram Manor LLC · 4 September 2026 · one appearance, three causes, and only one of them a fault

The inland water on the map looked wrong. Lakes and seas rendered as angular
polygons — the Black Sea a dozen straight edges, Crimea a triangle. The question
asked was whether these were artefacts or whether they might be real: **the
squaring of the lakes, possibly attributable to human activity.**

Measured, the appearance had **three unrelated causes**. Two were mechanical and
one was the world. Nothing about them is visible without measuring, and the
instinct that some of it was real turned out to be correct.

---

## 1 · THE BLACK SEA IS COARSE BECAUSE THE SOURCE IS COARSE

Counted, inside a box around the Black Sea:

```
WORLD.json  (Natural Earth 1:110m)      59 vertices     of 5,123 worldwide
COAST.json  (Natural Earth 1:50m)      197 vertices     of 13,220 worldwide
                                       3.3x finer
```

`world.mjs` **never ran a simplification pass.** It decodes the topojson arcs,
projects them, and drops rings whose bounding box is negligible. The angularity
arrived generalised, at 1:110 million, before the file was ever fetched.

This matters because the obvious suspect was the wrong one. It would have been
easy to blame the simplifier — it was in the code, it had a tolerance, and it
was demonstrably guilty of something else. **Attribute, never infer** is the
Probe Corps' second rule, and it is second because the plausible cause and the
actual cause are so often different objects.

**Fixed** by `COAST.json`, drawn over the coarse fill rather than replacing it:
the fill still carries the land and the relief clip, and only the edge improves.

---

## 2 · DOUGLAS-PEUCKER WAS GUILTY OF SOMETHING ELSE, TWICE

### A RING BREAKS IT SILENTLY, AND ALL 412 LAKES VANISHED

Douglas-Peucker measures each point's distance from the line joining the two
ends. **On a closed ring the two ends are the same point.** The baseline has
zero length, every perpendicular distance computes as zero, nothing exceeds the
tolerance, and the entire shape collapses to two points — then fails a
`length < 4` test and is dropped.

`LAKES.json` came out **0 KB, 0 rings**, from a source file holding 412 lakes.
It threw no error. The rivers, being open lines, had passed through the same
function without complaint an hour earlier.

**Fixed** by splitting each ring at the vertex farthest from its start and
simplifying the two open halves.

### AND THE TOLERANCE WAS TOO LOOSE TO SEE

At 0.12° the rivers survived and were quietly ruined:

```
Thames      5 vertices
Tiber       absent entirely
Nile        28 vertices · median spacing 73 km
```

It rendered acceptably at world scale, which is exactly why it shipped. The zoom
built the same evening is what it could not survive. Rebuilt at 0.03°: 181 KB,
Thames 10, Tiber restored.

**A third fault followed from the second.** A measurement of "how many seats sit
on a major river" returned 4% within 10 km — implausible, and false. It was
measuring distance to the nearest river VERTEX, and with vertices 73 km apart a
city standing on the bank can be 36 km from one. Point-to-segment is the measure;
point-to-vertex is a different question nobody asked.

---

## 3 · AND SOME OF THE SQUARING IS REAL

The lakes register distinguishes three classes, and the first pass treated them
as one:

```
320   Lake
 40   Alkaline Lake        Great Salt Lake · Issyk-Kul · Turkana
 52   Reservoir            MADE BY PEOPLE
```

Lake Mead was impounded in **1935**. Rybinsk was flooded in **1941**, Bratsk in
**1967**, Kainji in **1968**. Their outlines are angular *because a dam drowns a
valley and takes its shape.* **The squaring is the record, not an artefact** —
which is precisely why they must not be mistaken for natural water.

### THE ANACHRONISM THIS EXPOSED

Fifty-six rings of twentieth-century engineering were about to be drawn across a
map that scrubs to 4000 BC — visible under the Bronze Age, with nothing to say
they had not been there.

**Fixed:** a made lake appears only once the window reaches the year it was
built, and is drawn outlined rather than filled. Where the impoundment year is
unknown the register says 1900 — modern, and honest about being no finer than a
century. Same rule that keeps a soul out of a century nobody recorded.

```
window edge   made lakes drawn
   AD 1000      0 of 56
   AD 1945     40
   AD 1970     54
   AD 2026     56
```

---

## 4 · WHAT THIS SETTLED ABOUT AQUIFERS

Groundwater was considered in the same session and **refused**, for a stronger
version of the same reason.

Relief barely moves in six thousand years. Coastlines move a little —
Thermopylae's pass is now inland, Ephesus is six kilometres from the sea.
**A water table moves in decades.** The Nubian Sandstone has been drawn down
enormously since 1960; the Aral has largely dried since the same decade.

An aquifer map is a modern subsurface survey. Drawn across this span it would
be authoritative-looking and wrong, and a reader would have no way to tell.
The refusal is recorded in `REGIONS.json`'s own law, beside the deserts that
were accepted instead — **a desert's extent is stable across this map's span in
a way a water table is not.**

---

## THE FINDING

**An anomaly is not one thing.** A single appearance — squared water — carried a
source-scale artefact, two bugs in one algorithm applied to geometry it does not
handle, an invalid measurement built on top of one of them, and a real feature of
the world. Four different answers wearing one face.

The general shape, and the reason this is written down: **the plausible cause was
present, was guilty of something, and was not guilty of this.** Blaming the
simplifier for the Black Sea would have produced a fix that changed nothing,
verified against an appearance rather than a count, and left the ring collapse
and the reservoirs undiscovered.

Count first. The appearance is not the evidence.

---

*Registers changed by this finding: `COAST.json` (new), `LAKES.json` (new, with
`k` and `built`), `REGIONS.json` (new), `RIVERS.json` (rebuilt at 0.03°).
Aquifers refused, with the reason recorded in the file rather than in a
conversation.*
