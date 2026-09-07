# FINDING · THE NARROWNESS WAS MADE OF SEA
**7 September 2026 · Thermopylae, measured against the modern ground**

---

## THE SHORT VERSION

Thermopylae is a pass because the mountain comes down to the water. The
mountain is still there. **The water is not.**

Measured on the Copernicus 30 m surface model: from the coordinate the register
holds, the ground climbs 950 metres in a kilometre and a half to the south, and
runs **flat for six kilometres to the north before it reaches the sea.**

In 480 BC that six kilometres was the Malian Gulf. The Spercheios has been
filling it for two and a half thousand years.

---

## THE TRANSECT

North–south through 38.796N 22.536E, one reading every 500 m:

```
    38.856N      0.0 m      sea
    38.836N      0.3 m
    38.816N      1.9 m
    38.806N      4.6 m      flat coastal plain
    38.796N     17.4 m      \u2190 the coordinate the register holds
    38.791N    162.0 m
    38.786N    328.4 m
    38.781N    551.0 m
    38.776N    976.2 m      Kallidromo
```

**Seventeen metres to nine hundred and seventy-six in a kilometre and a half.**
The cliff is unambiguous and it is exactly where a defensive line would stand.
That half of the geography is intact.

---

## AND THE MEASUREMENT DISAGREES WITH THE PASS

`harvest-narrows-terrain.py` walks outward in 36 directions until the ground
rises 150 m above the floor or falls into the sea, and takes the smallest
opposite-pair sum:

```
    Thermopylae     crossing 3,784 m  on the 040\u00b0 axis
```

Against a strip that the transect implies is a few hundred metres wide.

**Both numbers are correct.** They are measuring different centuries. The
mountain blocks to the south at about a kilometre. Nothing blocks to the north
until the modern shoreline, six kilometres out.

> **THE PASS IS IN THE TERRAIN. THE NARROWNESS IS NOT, BECAUSE THE NARROWNESS
> WAS MADE OF SEA.**

---

## WHY THIS IS THE FINDING AND NOT A FAULT

The register's `why` sentence already said the coast had silted several
kilometres. That was a remembered fact carried in prose. **The DEM turned it
into a number**, and did it without being asked — the harvest was built to check
whether coordinates were right, and what it produced instead was a measurement
of how much the ground has changed underneath a correct one.

It is also the clearest case yet of the rule the map keeps everywhere else:

> **THE TERRAIN IS THE BASELINE BECAUSE IT IS COMPLETE AND FREE, NOT BECAUSE IT
> IS CONTEMPORARY WITH ANYTHING IN THE REGISTER.**

Modern elevation is exact. The modern *shoreline* is a modern claim, and on a
map that scrubs to 4000 BC it is the single most misleading thing on the
surface — because it looks as reliable as the mountains beside it and is not.

---

## WHAT IT IMPLIES ELSEWHERE

Thermopylae is not special; it is legible. The same displacement is under other
entries and mostly unmeasured:

- **Piraeus, Eleusis and Marathon** are all silted harbours. The Attica render
  shows their modern shorelines at 30 m and cannot show their ancient ones.
- **Ephesus** is now five kilometres inland.
- **Every delta on the map** has grown seaward since the register's earliest
  windows \u2014 the Nile, the Po, the Rhône, the Danube.
- And the reverse exists too: **the Fens and the Pontine Marshes were drained**,
  so ground that was impassable now reads as farmland. `NARROWS.csv` already
  carries a `drained` year for exactly this reason.

**A COASTLINE IS THE FASTEST-MOVING THING THE MAP DRAWS AS THOUGH IT WERE
FIXED.** Rivers wander, forests regrow, lakes are impounded — all of those the
register handles or refuses. The shore is drawn once, from one century, at every
year.

---

## WHAT WOULD ANSWER IT, AND WHAT WOULD NOT

**Would not:** finer elevation. The problem is not resolution. A 1 m survey of
the modern Malian Gulf tells you nothing about where the water was.

**Would:** a palaeoshoreline register — an authored coastline per era for the
handful of places where the difference decides something. Small, editorial, and
the same shape as `NARROWS.csv`: perhaps twenty coasts, each with a date and a
source, drawn only in the windows they belong to.

**Or, cheapest and honest today:** say so. A note on any narrow whose shoreline
has moved, and the shelf visible under the water in `GROUND.jpg` so a reader can
see the flat ground that used to be seabed.

---

*Found while measuring `NARROWS.csv` against Copernicus GLO-30 on 7 September.
Companion to slip #74. The harvest that produced it is
`tools/harvest-narrows-terrain.py`; the numbers are in `NARROWS-terrain.csv`.*
