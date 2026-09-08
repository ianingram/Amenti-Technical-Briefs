# BRIEF · A PROXY BECOMES A FOUNDATION
## modern infrastructure standing in for ancient routes, and why it was refused

*7 September 2026. Companion to slip #77. Written because the idea was good,
the refusal was close, and the reasoning will be needed again.*

---

## THE PROPOSAL

Use today's major roads as a first approximation of the ancient network. They
are mapped everywhere, free, precise, and easy to obtain. Terrain constrains
routes, so a modern line should be near an ancient one. Street-by-street
accuracy can be built off it later.

**Every part of that is true except the last clause, and the last clause is the
whole problem.**

---

## WHAT THE EVIDENCE SAYS ABOUT THE ALTERNATIVE

There is no easy honest source, which is the condition under which a proxy is
most tempting. Measured in the Pleiades GIS package:

```
    3,293  places typed road · via · canal · bridge · pass · station
      296  of them carry any geometry at all
        2  of those fall inside a hundred miles of the Acropolis
```

`ATTICA.csv` holds nineteen road-ish entries and almost all are bridges and
passes. **The Barrington Atlas drew the roads; the digital gazetteer recorded
them as PLACES WITH A REPRESENTATIVE POINT.** A road's representative point is
meaningless — it is the middle of a line nobody stored.

So the choice really was between a proxy and nothing.

---

## WHY THE PROXY FAILS ON ITS OWN TERMS

**TERRAIN CONSTRAINS ROUTES IN THE PASSES AND NOWHERE ELSE.** At Eleutherai
there is one way over Kithairon and it has not moved. Thermopylae, the Isthmus,
the Cilician Gates — the same. That is real, and it is why the intuition feels
strong.

Across the Boeotian plain the ground permits any line at all. What decides a
modern road there is modern economics: which ports matter now, which cities
matter now, where a border was drawn in 1832, where a rail line went in 1900 and
a motorway followed in 1970. **The Athens–Thessaloniki motorway serves a country
that did not exist.**

> **A CONSTRAINT THAT HOLDS AT THERMOPYLAE AND FAILS ACROSS BOEOTIA IS NOT A
> METHOD. It is a coincidence with good publicity.**

And the failure is worst exactly where the register is thinnest. In the passes,
where the proxy would be right, the register already has the pass — `NARROWS.csv`
holds it and named it. In open country, where the register has nothing, the
proxy is at its least reliable. **It is accurate where it is redundant and
invents where it is needed.**

---

## AND THE REAL FAULT IS INHERITANCE

This is the part that makes it a doctrine and not a preference.

> **A PROXY LAID DOWN AS A FOUNDATION IS BUILT ON, AND WHAT IS BUILT ON IT
> CANNOT REMEMBER THAT IT WAS A PROXY.**

The sequence is not hypothetical, it is what always happens:

1. The modern network goes in, honestly labelled, as scaffolding.
2. A road is authored against it — *the Sacred Way ran roughly here, beside the
   modern road*.
3. A site is placed relative to that road.
4. Someone corrects the road. They are correcting the position of a modern
   motorway, and they do not know it.
5. The label falls off. It survives in a file header for one session and in
   nobody's head after that.

The register ends up asserting a road network derived from the E75 with no way
left to tell — and every correction after step 3 makes the entanglement worse
rather than better, because each one adds work that would have to be undone.

**The scaffolding cannot be removed once anything leans on it.**

---

## THE SHIP HAS ALREADY MET THIS IN A SMALLER FORM

`ATTICA.csv` dates the Acharnian Gate to **AD 2000–2099**.

That is not an error. Pleiades is recording where a *modern excavation*
identified the gate, and dating that identification to the modern period, which
is correct and careful. It becomes false the moment it is read as the date of a
gate — and it would be, by any surface that filtered places by year without
asking what the year meant.

Same shape, one register lower: **a modern fact standing in for an ancient one,
honest at the source and false downstream.**

The lesson generalises past roads. Any modern layer — land cover, coastline,
settlement, place-name — is a proxy the moment it is used to say something about
antiquity, and the danger is proportional to how useful it is.

---

## WHAT TO DO INSTEAD

**FIRST, LOOK FOR THE REAL SOURCE.** `itiner-e` appears in the Pleiades
linestrings and is digitising Roman roads as actual routes rather than as
points. If it is openly licensed and covers Greece, the problem is solved
properly and none of this matters.

**FAILING THAT, AUTHOR THE FEW.** Attica's roads are not many and are well
attested:

```
    the Sacred Way              Athens to Eleusis, and the procession walked it
    the Panathenaic Way         the Dipylon Gate to the Acropolis
    the road over Pentelikon    Athens to Marathon — the road of the run back
    the road to Sounion         down the east coast to the cape
    the Diolkos                 across the Isthmus, ALREADY IN THE REGISTER
```

Ten or twelve entries, each with a source, is a better register than a thousand
lines nobody can vouch for. **The register's value has never been its size.**

---

## THE STANDING RULE

> **A MODERN LAYER MAY BE SHOWN BESIDE THE REGISTER, LABELLED AS TODAY'S, AND
> MAY NEVER BE SHOWN AS THE REGISTER. WHERE A PROXY IS THE ONLY THING
> AVAILABLE, IT IS DRAWN AS A PROXY OR IT IS NOT DRAWN.**

Shown beside, it is useful and honest: a reader comparing today's motorway to an
authored ancient road learns something real about how terrain works and how much
it does not. Shown as the register, it is a claim nobody made.

**Acceptance test:** no coordinate in any register can be traced to a modern
road, and a reader can tell at a glance which lines are attested and which are
today's.

---

*Slip #77. The measurement is from the Pleiades GIS package as of 7 September
2026; if a later release ships road geometry, this brief is superseded and the
harvest should take it.*
