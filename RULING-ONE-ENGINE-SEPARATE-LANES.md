# AMENTI — RULING: ONE ENGINE, SEPARATE LANES, SEPARATE BUDGETS
**Ingram Manor LLC · 24 August 2026 · ruled, not built**

## WHAT THIS IS

The captain's ruling on the proxy, made at the close of the Stage 2 session,
recorded so the session that builds it begins with everything instead of
nothing. **No code exists yet.** This is the decision and its lineage. The
build session writes the brief — proposed title: **THE TWO THROTTLES** — and
that brief supersedes this note.

---

## THE RULING

> **ONE ENGINE. SEPARATE LANES. SEPARATE BUDGETS.**

There is one engine: `amenti-proxy` — one Worker, one key, one gate. That does
not change. What changes is that the gate learns to tell its doors apart.

- Every surface declares its **lane** — the flagship's terminal and counsel on
  one, the hall on another, any future advertising embed on a third.
- Each lane has its **own budget and its own limits** — per-IP rate, per-hour
  ceiling, daily spend cap.
- A lane that exhausts its budget **fails to a sentence**, not a broken box —
  the hall already renders a 429 as *the hall must catch its breath*.
- A lane can be throttled or **shut off in one line** without any other lane
  feeling it. A flood through the ad door must never starve Caesar's terminal.

**Engines are for capability. Lanes are for blast radius.**

## WHY NOT A SECOND ENGINE

A second engine is another Worker, another key, another gate to harden,
another thing the mirror must hold and the probes must watch — and it doubles
the security work that is the whole point. Every duplicated path in this
system has cost a night; a duplicated engine is the most expensive kind. The
lanes give everything a second engine would — isolation, a kill switch for the
marketing surface — with one wallet to guard and one gate to fortify.

## WHY NOW

The hall (`hall.html`, shipped this night) is being considered for
**advertising surfaces on third-party sites**. The proxy currently answers
anyone who can load a page, with no origin check, no rate limit, no spend
ceiling — an open door with the wallet behind it. Fine at the ship's own
traffic; an invitation at ad traffic. **The lanes are the precondition for any
embed. No ad runs before the gate can say no.**

## THE LINEAGE — THE NAME WAS THE DIAGNOSIS, AGAIN

This is not an imported web-security pattern. It is the ship's own throttle,
applied to the intake:

- **July:** the voice engine flooded — the HTTP 524 was not a timeout but a
  flood, and `amenti-throttle.js` cut the metering, the measures, the rests.
  *An engine does not run on a tank of fuel dumped into the cylinder at once.*
  That architecture lives on, byte for byte, inside `amenti-voice.js` — the
  Elder Boatswain.
- **13 July:** a session decided "throttle" was a misnomer and wrote *not a
  throttle and never was* into the semantics. The captain caught it. **The
  name was the diagnosis.**
- **24 August:** the ads question raised a flood at the other end of the pipe
  — a flood of questions instead of a flood of speech — and the captain
  recognised the word before finding the section. The voice throttle meters
  what the ship says; the proxy lanes meter what the crowd asks. **One
  engine, a throttle at each end.**

The recognition itself is the finding: the solution pre-existed the problem
because it was solved, named, and written down — and the index made the
writing reachable. The architecture expressed itself in thought before code,
because it was expressed in writing after the last code.

## FOR THE BUILD SESSION

1. Read the Worker as it is. **This note contains no reading of
   `amenti-proxy`'s code — nothing here about its current shape is verified.**
2. Lanes: a `surface` field or per-lane routes on the same Worker — the build
   session rules on the mechanism after reading.
3. Origin allow-list, per-IP limit, per-lane hourly and daily ceilings; every
   refusal a sentence.
4. The hall's Worker-side **question log tube** belongs in the same session —
   deferred from Stage 2 because the browser may not write.
5. A **search-only embed variant** of the hall (ask path disabled, "enter the
   hall to ask" linking home) costs nothing per impression and may be the
   stronger ad shape — the ad invites; the site answers. Ruling open.
6. `probe-gate` or a sibling learns to knock on each lane and read its limits
   back — **a limit nobody has tested is a prayer.**

*The hall is a doorway; the gate decides who may keep asking.*
