# AMENTI — RULING: THE DISPATCH, AND THE TWO NAMES
**Ingram Manor LLC · 24 August 2026 · a standing ruling, not an account**

## THE ONE-LINE RULING

> **The machinery is named `dailyplanet:`. The publication is named the Amenti
> Dispatch. Do not reconcile them. The mismatch is deliberate and defended.**

The code keeps the old name. The reader sees the new one. Anyone who "fixes"
the discrepancy by renaming the code breaks working surfaces AND reopens a
legal exposure. This document exists so that never happens.

---

## THE TWO LAYERS

| | Name | Where it lives | May it change? |
|---|---|---|---|
| **Mechanism** | `dailyplanet:` | KV key prefix, `generateDailyPlanetPiece`, the firing-log tube, the weekly manifest, the docket/court-reporter slots, the feed index | **No.** Load-bearing. |
| **Surface** | **Amenti Dispatch** | What a reader sees on the page | Already changed. This is the public name. |

Both are correct at once. `dailyplanet:anubis:<week>` and
`dailyplanet:thoth:<week>` are the Dispatch's front page and register, stored
under the mechanism name and published under the surface name. The `dailyplanet:`
KV entries are **not residue and not a retired tube** — they are the live
storage of the Amenti Dispatch.

**Read things by their layer.** Surface names (Dispatch, Atlantica) for what
readers meet; mechanism names (`dailyplanet:`, `atlantica:`, `week:`) for what
the registers store. A reading that conflates them will mistake a live tube for
a dead one — this has already happened once, on 24 Aug, which is why this is
written down.

---

## WHY THE CODE WAS NOT TOUCHED

Two reasons, and the second is the one that must survive.

**Structural.** `dailyplanet:` is wired into several surfaces at once — the
docket, the court-reporter slots (Anubis's summons, Thoth's register, the
confession), the feed index, the weekly manifest. Renaming the mechanism means
surgery across all of them, each edit a chance to break a working system for a
cosmetic gain. Minimum blast radius says: do not.

**Legal — the governing reason.** "The Daily Planet" is a well-known fictional
newspaper under existing trademark. A public-facing publication under that name
is an exposure. The exposure exists **only at the surface** — in what is
published and seen — not in an internal KV key nobody reads. So the fix lives
**only at the surface**: the reader sees "Amenti Dispatch," the exposure is
gone, and the working machinery underneath is never disturbed.

> The legal problem exists only at the surface, so the fix lives only at the
> surface. The code does not care what it is called; the exposure is in what is
> published.

**Therefore: renaming the code would break surfaces AND reopen the exposure the
surface rename exists to close.** It is the worst of both — structural risk and
legal risk, for no gain. The mismatch is not debt. It is the shape of a correct
decision.

---

## FOR ANY SESSION THAT MEETS THE MISMATCH

- Seeing `dailyplanet:` in the code and "Amenti Dispatch" on the page is **not
  a bug.** It is this ruling, working.
- Do not "tidy" the KV prefix, the function names, or the tube name.
- If the firing log or a probe reports the tube as `dailyplanet:` / THE DAILY
  PLANET, read that as the mechanism name for the Dispatch. It is live, on the
  weekly rotation.
- The one genuine open defect near this tube is unrelated to the name: the
  date sensor reads a last-fired date in the future (age negative), which passes
  a `< threshold` test and shows green. That is a sensor bug, not a naming
  matter, and fixing it must not touch the `dailyplanet:` name.

---

## WHERE THIS SHOULD ALSO BE RECORDED

A ruling in a brief is read by a person. The registers are read by machines and
by fresh sessions, and they currently say nothing about this. To close the gap
fully, a one-line note belongs in the mechanism's own registers:

- **`SOURCES.semantics.json`** — where `fleet-dispatch.json` is described, note
  that the `dailyplanet:` tube publishes as the Amenti Dispatch.
- **`fleet-dispatch.json`'s own header** (via `probe-ordnance`) — a `surface`
  field beside the tube, so the log itself names both layers and no reader has
  to hold the mapping in their head.

Until then, this brief is the only place the mapping is written, and a brief
that a probe cannot read is a memory with a longer shelf life — better than
none, not yet a reading.

*The code keeps the old name for safety. The reader sees the new one for
safety. Both safeties are real, and they point in opposite directions — which
is why the mismatch must stay.*
