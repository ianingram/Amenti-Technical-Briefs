# AMENTI — BRIEF: THE FLEET, MADE LEGIBLE
**Ingram Manor LLC · 24 August 2026 · a shop-floor account**

## HOW TO USE THIS

An account of one evening's work: turning the publishing fleet from something
only the captain could describe into something the ship can read. It is correct
about the night it describes and makes no claim about later. Its counts are of
its own night; the registers named in it are the source thereafter.

The evening began as a conversation about the site's chronology — what publishes,
when — and became something more useful: the discovery that the chronology could
not be *mapped* because its foundation had never been *written down*. The map
existed only in the captain's head. This is the account of moving it out.

> **STAGE 2 TAUGHT THE SHIP TO BE READ.
> THIS TAUGHT THE FLEET TO BE READ.**

---

## I · THE THREE LAYERS, AND WHICH ONE WAS MISSING

The publishing system was never one thing. It is three, and only two were
legible:

- **The mechanical layer — readable.** What the code stores and the probes see:
  KV prefixes (`atlantica:`, `week:`, `dailyplanet:`), the firing log
  (`fleet-dispatch.json`), the cadences hardcoded inside `probe-ordnance`.
- **The surface layer — partly readable.** What a reader meets: Atlantica, THE
  WEEK, the Amenti Dispatch. Some of this lived only on the pages.
- **The intent layer — NOT readable.** What the captain *decided*: which tubes
  are live, which are paused, which retired, what cadence each should hold,
  which surface name maps to which mechanism. This lived nowhere. It lived in
  the captain's memory and in conversation.

The whole month's work had been about legibility — the source index, the
glossary, the registers, the hall — so that a fresh session reads the ship
instead of interviewing the captain. And yet, asked "what tubes are meant to
fire," the honest answer was: *nobody can read that; you have to ask Ian.* That
was the gap. Not a failure of the machinery — a decision that had never reached
a register.

---

## II · WHAT THE FIRING LOG SAID, AND WHY IT MISLED

`fleet-dispatch.json`, re-read this evening, reported:

- **ATLANTICA** — fired 64×, last 18 days ago — WARN
- **THE WEEK** — fired 0 — FAIL
- **THE DAILY PLANET** — fired 20×, last date 76 days in the FUTURE — OK
- **THE PODCAST** — fired 0 — FAIL
- **THE DOCKET** — unknown — WARN

Read cold, this looks like a fleet in collapse: two never fired, one dark, one
reporting an impossible date. It is not. **The log can only see whether a tube
fired — it cannot see whether the captain meant it to.** ATLANTICA did not fail;
it was *stood down deliberately* while the ship's foundation was rebuilt. THE
PODCAST was never built. The presses were paused with intent, and a probe that
reports mechanical fact without intent reads a deliberate pause as a failure.

The correction the captain supplied, and the reframe that followed: **the
surfaces are built and most have fired; they were paused, not broken; going
forward is RESUMPTION, not construction.** But that correction, too, lived only
in conversation — which is exactly the disease, not the cure.

---

## III · TWO RULINGS THE EVENING SURFACED

Before anything could be mapped, two decisions had to be written down, because
both were load-bearing and both lived only in memory.

**The Dispatch, and the two names** (its own brief,
`RULING-THE-DISPATCH-TWO-NAMES.md`). The Daily Planet was renamed to the Amenti
Dispatch *at the surface only* — for legal reasons (trademark exposure on the
public name) — while the `dailyplanet:` mechanism was kept untouched, because it
is wired into the docket, the court-reporter slots, the feed index and the
weekly manifest. The mismatch between code-name and reader-name is deliberate
and defended: renaming the code would break surfaces AND reopen the exposure the
surface rename closed. A future session meeting `dailyplanet:` in the code and
"Amenti Dispatch" on the page must read it as this ruling working, not a bug to
tidy.

**The fleet is weekly.** The Daily Planet's daily cadence is retired; the fleet
rotates weekly now. Stated in conversation weeks ago; written into a register
for the first time this evening.

---

## IV · THE INSTRUMENT ALREADY HALF-EXISTED

The key finding, and the reason almost no new machinery was built:
`probe-ordnance.mjs` **already** checked intent against reality. It declared each
tube's cadence, computed `lastAgeDays`, raised WARN/FAIL on staleness, and even
inspected whether the cron was *armed* or still commented out — the exact THE
WEEK diagnosis, automated. It carried the law: *a schedule that nobody checks is
a promise nobody keeps.*

What it lacked was not capability but a *readable declaration*. The cadences
were **hardcoded inside the probe's own body.** To change the fleet, one edited
the checker. And the probe knew nothing of surface names, of retired-vs-paused,
of the Dispatch ruling — because those had never been written anywhere it could
read.

So the work was not to build a checker. It was to **lift the declaration out of
the checker and into a register**, and add the three things the probe could not
know.

---

## V · WHAT WAS BUILT

**`fleet.json` — the fleet declared.** A hand-authored register naming each
tube: `mechanism` (permanent internal name), `surface` (public name),
`state` (live / paused / planned / retired), `cadence`, the `cron` it should
carry, the KV `prefixes` its output lands under, and `logId` — the explicit key
linking it to the firing log, so no reader has to guess that "THE DAILY PLANET"
in the log is the Amenti Dispatch. It holds **no numbers** — only intent. The
firing log holds what fired; this holds what *should*.

**`fleet-status.html` — the captain's window.** A self-contained page that reads
`fleet.json` and `fleet-dispatch.json` live and lays intent beside reality, one
card per tube. It is **state-aware**, which is the whole point: a paused tube
reading quiet shows calm; a *live* tube that has never fired shows red. The
difference between a dashboard that cries wolf on five tubes and one that points
at the single thing wrong.

On the night it was built, that single red card was **THE WEEK** — declared
live, never fired, its content loaded in the hold, its cron almost certainly
never registered. Everything else read true: Atlantica calm (paused by intent),
the Podcast calm (planned), the Dispatch amber (the future-date sensor bug), the
Docket noted as live-but-unwalked.

---

## VI · A BUG THE TEST CAUGHT

The status page was tested against the live registers before it shipped, with
the model of matching each declared tube to its firing-log entry. The first
matcher guessed the mapping from surface and mechanism names — and the **Amenti
Dispatch matched nothing**, because the log calls it `THE DAILY PLANET`. A live
tube that had fired 20 times would have shown as *never fired, fault* — the
naming trap from the Dispatch ruling, biting the very page built to clarify it.

The fix was to stop guessing: `fleet.json` now carries an explicit `logId` per
tube, stating its own link to the log. **The declaration names its own
correspondence rather than leaving a reader to infer it** — the same principle
as everything else here. Intent, written down, not derived.

---

## VII · WHAT THIS IS, TOWARD AUTONOMY

Autonomy here does not mean the presses run themselves. Most of Amenti's content
is authored — chapters, plates, dispatches — and *should not* run without a
hand. Autonomy means something narrower and more honest:

> **The ship knows what it is meant to do, checks whether it did, and can show
> the gap — without the captain being the register.**

THE WEEK failed silently for six weeks because nothing watched the gap between
*declared* and *fired*. The fault was not the missing cron; it was that no
instrument was positioned to notice the cron was missing. `fleet.json` gives the
instrument something to check against; `fleet-status.html` gives the captain
something to read. The loop is not yet closed — `probe-ordnance` still reads its
own hardcoded cadences, not `fleet.json` — but the register it must read now
exists.

---

## VIII · OPEN, RECORDED, NOT CHASED

1. **Wire `probe-ordnance` to read `fleet.json`.** The keystone move: the probe
   should read the declaration, not carry its own copy. Then changing the fleet
   is editing one register, and both the checker and the window follow. Until
   then, the two agree only because one was copied from the other, and they can
   drift.
2. **THE WEEK's cron** — the one red card. Content loaded; the trigger in
   `Amenti-Workers` was almost certainly never registered. Wiring it is the
   first act of resumption.
3. **The Dispatch date sensor** — reads a future last-fired date, passes a
   `< threshold` test, shows green. A sensor bug, to be fixed without touching
   the `dailyplanet:` mechanism name.
4. **The Podcast keystone** — verify whether Amenti Studios' Phase One
   (`/speak` content-addressed R2 caching) ever shipped, before treating the
   tube as buildable.
5. **The Docket** — `probe-ordnance` does not walk the mint tube. A silent court
   is currently seen only when a human reads a date. Teach an instrument to
   watch it.
6. **Fold the window into ORDNANCE BAY** — the Fleet-Documents pane
   (`ordnance.html`) is the natural home for this display, but reading
   `fleet.json` from there is a cross-repo fetch (the pane in Fleet-Documents,
   the register in Amenti.live) — the water-between shape, to be ruled on
   deliberately, not wired quietly.

---

## IX · THE LESSON

The evening looked like a detour. It began aimed at a map and spent its hours
writing rulings and a register instead. But the map could not have been drawn:
its foundation — the fleet's intent — had never been committed to anything a
session could read. Drawing it from memory would have produced a map that
re-resurrected the Daily Planet, mis-read the `dailyplanet:` keys, and perhaps
"fixed" the name straight into a lawsuit.

> The sidetrack was the track. A chronology cannot be mapped until the fleet's
> intent is legible — and tonight it became legible for the first time.

The registers were built so the ship could be read. The fleet declaration is
the ship's schedule, made readable the same way — so the next session, and the
next captain, reads what is meant to fire instead of asking.

*A schedule that nobody checks is a promise nobody keeps. Now the promise is
written down, and something can check it.*
