# BRIEF — THE LIBRARY HAS NO INSTRUMENT
### A living library, growing, and no probe reads it
**Ingram Manor LLC · Amenti Fleet · 25 August 2026 · status: PROPOSED**

---

## THE FINDING

The `library/` folder in `Amenti.live` holds the reading rooms — one folder per
figure, each containing that figure's primary-source works. It is a **living
subsystem**: it grows as rooms are added, and rooms fill as works are added to
them. It is arguably the heart of "a library of the dead."

**And no instrument watches it.** Every other core subsystem on the ship has a
probe or register reading its true state:

- the fleet → `fleet.json` (intent) + `probe-ordnance.mjs` → `fleet-dispatch.json` (reading)
- the plates → `PLATES.json` + the PLATE DECK pane
- the workers → `WORKERS.json` + the WORKERS pane

The library has **none**. No probe walks it. No register holds its state. No pane
shows it. It is the one core subsystem that is completely uninstrumented.

This is a **Silent Signature at the scale of a whole subsystem**: the library is
alive and no instrument can see it.

---

## THE SYMPTOM THAT REVEALED IT

The Codex header reads **"9 ENTRIES UNLOCKED."** That number is hardcoded text in
`Page1.html`, typed once and never updated. Meanwhile:

- the hardcoded key list `AMENTI_LIBRARY_KEYS` in Page1 holds **21** figures,
- and the actual `library/` folder holds **more than 21** rooms (confirmed —
  folders like apollo, augustus-caesar, brutus, christopher-columbus, cleopatra,
  dante-alighieri appear in `library/` but are absent from the 21-key list).

So there are **three layers of drift**, each behind the last:

| layer | says | reality |
|---|---|---|
| the label | 9 | wrong |
| the hardcoded key list | 21 | stale |
| the `library/` folders | 21+ (true, growing) | the source of truth |

The label is not the bug. The label is a *symptom* of the bug: **there is no
register that reads the library, so a hand-typed number was the only option, and
a hand-typed number always drifts.** This is the third time this session a
hardcoded count has been found stale (the entries label, the firing-log
schedule, now the library). The lesson is the same each time: *count the real
thing; do not store the number.*

---

## PLACEHOLDERS — THE EMPTY-GLASS ANGLE

Not every room is full. The commit log shows
`Delete library/dante-alighieri/placeholder.md` — evidence that some rooms are
**stubs** (a folder exists, but holds a placeholder, not real works). So a naive
folder-count would over-report: it would count empty rooms as unlocked entries.

A real reading must distinguish, the ship's "empty glass" way:

- a room with real works = a true reading room
- a room with only a placeholder = an empty room wearing a folder

A room that exists but holds nothing is exactly the bell ringing into an empty
week — a fact the instrument must report honestly, not paper over.

---

## THE PROPOSAL — THE LIBRARIAN

Give the library the same treatment the fleet got when it was "made legible":
a probe that reads it, and a register that holds the reading.

**1. The probe — `probe-library.mjs` (the librarian).**
Runs in GitHub Actions (the only runtime; the captain's Mac has no tooling).
Walks `library/`, and for each room folder reads:
- the figure key (folder name)
- how many works it holds
- whether those works are real or placeholder/stub
- (optional) titles / file list per room

Modelled on `probe-ordnance.mjs`, which walks the tubes and writes the firing
log. The tube is the instrument; the reading is the register. Same doctrine.

**2. The register — `LIBRARY.json`.**
What the librarian writes. The reading of the library's true state:
- total rooms
- rooms that are real vs. placeholder
- the list of unlocked figures (real rooms only)
- per-room work counts

Modelled on `PLATES.json`. A register is a reading, regenerated — never
hand-edited.

**3. The wiring.**
- The Codex label reads `LIBRARY.json` → shows the TRUE unlocked count, always
  current, never drifts.
- `AMENTI_LIBRARY_KEYS` is sourced from `LIBRARY.json` (real rooms only) instead
  of being a hand-kept list of 21 — so the "OPEN THE FULL FILE" button appears
  for exactly the figures who actually have a room.

**4. (Optional, later) a LIBRARY pane.**
Like PLATE DECK shows the plates, a LIBRARY pane would show the library's state
at a glance — rooms, fill, placeholders, growth. Closes the instrument blind
spot visibly. Not required for the fix; a natural follow-on.

---

## WHY THIS IS THE RIGHT FIX, NOT A STOPGAP

The tempting quick fix — count the folders by hand, change "9" to the real
number — is a **fresh lie**. It is correct for exactly as long as it takes to add
the next room, then drifts again. That is the same trap that produced "9" in the
first place, reset.

The library is a *living* thing. A living thing must be *read*, not *remembered*.
Wiring the label and the key list to a register that reads `library/` kills this
entire class of bug for the codex — the count is correct now and stays correct as
the captain adds rooms, with no further human bookkeeping.

This is precisely the "make the fleet legible" work — one of the best things the
ship has — applied to the one subsystem that never got it.

---

## BUILD ORDER

1. **Write `probe-library.mjs`** — walk `library/`, classify rooms (real vs.
   placeholder), emit `LIBRARY.json`. Decide the placeholder test (e.g. a room is
   "real" if it contains ≥1 non-placeholder `.md`).
2. **Add the Action** that runs it (on push to `library/**`, and on a schedule)
   and commits `LIBRARY.json`.
3. **Wire the Codex label** to read `LIBRARY.json`'s real-room count.
4. **Wire `AMENTI_LIBRARY_KEYS`** from `LIBRARY.json` (real rooms only).
5. **(Later) build the LIBRARY pane.**

Each step is verifiable against the real folders. Verify by CONTENT (the count
matches the folders), not by existence.

---

## OPEN QUESTIONS FOR THE CAPTAIN

- **What is the placeholder test?** How does the librarian tell a real room from a
  stub — filename convention (`placeholder.md`), a front-matter flag, a minimum
  work count? The captain knows the convention.
- **What counts as "unlocked"?** Confirm it means "has a real reading room"
  (recommended), as opposed to the whole roster (1016) or the plates (51).
- **Should empty/placeholder rooms show the "OPEN THE FULL FILE" button at all?**
  Recommendation: no — a button that opens an empty room is a broken promise.

---

## THE PRINCIPLE

> The fleet was made legible by giving it a register that reads it. The library is
> the older, quieter subsystem that never got the same courtesy — a living thing
> no instrument watches. A hand-typed count is a memory, and memories of living
> things go stale the moment the thing grows. Give the library its librarian: a
> probe that walks the rooms and reports what is really there — full rooms, empty
> rooms, and all — so the number on the page is a reading, not a wish.
