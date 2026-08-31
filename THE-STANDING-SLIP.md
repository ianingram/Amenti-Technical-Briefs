# THE STANDING SLIP
**The yard's open work · Ingram Manor LLC · opened 24 August 2026**

Every other slipway plans one build. This one holds the work that is not yet a
build — the loose items, the recorded-not-chased, the things a session
discovers and the next session must not rediscover by accident. It is a slipway,
so it obeys the slipway's law:

> **A MOVE IS NOT DONE WHEN THE FILE IS UPLOADED. IT IS DONE WHEN ITS
> ACCEPTANCE TEST PASSES.**

This is the durable home for open items. When an item grows large enough to need
its own phases, it graduates to its own slipway and leaves here. Until then it
lives here, stated as a move — what it is, what it unblocks, and how you will
know it is done. **The chat is not enough; this file is the memory the chat
cannot keep.**

Kept by hand. Reviewed at the top of a session, not the bottom.

**THE NUMBERS ARE NAMES, NOT RANKS.** They are referenced from the handoff and
from other briefs, so they do not move once given. The order lives in THE
CRITICAL PATH below, and a move added late can outrank one added early.

**AND MOVES LIVE OUTSIDE THIS FILE.** Three addenda hold work that has never
been folded in — `slip/SLIP-ADDENDUM-THE-DAILY-ROTATION.md` (three moves),
`slip/SLIP-ADDENDUM-THE-SECOND-VOICE.md` (two), and
`slip/SLIP-ADDENDUM-THE-EDITIONS.md`. Until they are read and folded in or
cited here as moves, this file is not the whole of the yard's open work and
should not be trusted as if it were.

---

## THE HONEST CONSTRAINT

The same one every slipway names: the captain deploys, uploads, runs SQL, sets
secrets, and verifies by opening. The assistant reads, reasons, and writes files
but cannot reach, push, or see the result. So every move below ends in a check
**the captain can perform by opening something** — not a claim the assistant
can make alone.

---

## THE STANDING WORK — stated as moves

Ordered by how much it hurts to leave undone.

### 1 · Wire `probe-ordnance` to read `fleet.json`
**The keystone of the autonomy step.** The probe still carries its tube cadences
hardcoded in its own body; `fleet.json` now holds the same declaration as a
register. Until the probe reads the register, the two agree only because one was
copied from the other, and they will drift.
- **Unblocks:** changing the fleet becomes editing one declaration; the checker
  and the window both follow. The ship keeps its own schedule honest.
- **Acceptance test:** edit a cadence or state in `fleet.json` alone, run the
  probe, and see the probe's output change to match — with no edit to the probe.

### 2 · Wire THE WEEK's cron
The one red card on the fleet status. Content is loaded in the hold (6 issues);
the tube has fired zero times, almost certainly because the `[triggers]` cron
block was never registered in the Worker's `wrangler.toml`. Diagnosed 13 July,
again 24 Aug.
- **Unblocks:** the weekly issue actually publishes; the first act of resumption.
- **Acceptance test:** dry-run once by hand, confirm the ledger, then arm the
  cron; the following Sunday, `fleet-status.html` shows THE WEEK green.

### 3 · Fix the Amenti Dispatch date sensor
It reports a last-fired date in the future (negative age), which passes a
`< threshold` test and shows green — a broken sensor behind a green lamp. Must be
fixed **without touching the `dailyplanet:` mechanism name** (see
RULING-THE-DISPATCH-TWO-NAMES).
- **Unblocks:** the Dispatch's status can be trusted.
- **Acceptance test:** the probe reports a real, non-negative age for the
  Dispatch, and `fleet-status.html` shows it accordingly.

### 4 · CLOSED BY SUPERSESSION, 31 Aug — and a new number replaces it
The move asked for a 123-entry `SOURCES.semantics.json` describing `fleet.json`
and `fleet-status.html`, with `unindexed: 0`. Read against the register on
31 Aug: **both fleet files are described** — `fleet-declared` and `fleet-status`
carry real glosses — and the index holds **191 entries, not 123.** The upload
landed and then grew. That half is done.

But `unindexed` is **21, not 0**, and it is a different 21: briefs in
`Amenti-Technical-Briefs`, among them `BRIEF-THE-DIRECT-PUSH-QUESTION.md` — the
brief for move #10, sitting outside the index. One path is unreachable, a 404 on
`Amenti.live/main/book/00-the-beach.md`.
- **Unblocks:** nothing further; the drift it named is a different drift now.
- **Acceptance test:** none. This move is closed. The remaining work is #22.

### 5 · BLOCKED, NOT SCHEDULED — the hall's brief-quoting
The move proposed spending ~2,000 chars on a passage (`MAX_BRIEFS` 0 → 1,
`BRIEF_SLICE` → ~2000). **Measured on 31 Aug by `probe-hall-wall`, running the
hall's own functions: there is no budget to spend.** The prompt stands at
**24,208 against a wall of 20,000** with `MAX_BRIEFS` at 0 — over by 4,208
before a single passage is fetched.

It also named the wrong pressure. The slices were what crowded the wall on
24 Aug. What crowds it now is the catalogue growing underneath it, 106 documents
to 190, because the hall declares every document on every question.
- **Unblocks:** nothing, until #12 is fixed. Quoting is not a feature to
  schedule; it is the first thing that becomes affordable again afterwards.
- **Acceptance test:** deferred to #12 and #13. When the prompt fits with room
  to spare, arm one short slice and confirm the proxy does not 413.

### 6 · Teach an instrument to walk the Docket
`probe-ordnance` does not walk the mint tube. The first case-set closed 13 July
with zero arguments submitted — learned because a human read a date, not because
anything watched. A silent court should be seen by an instrument.
- **Unblocks:** the Docket's silence becomes a reading, not a surprise.
- **Acceptance test:** the probe (or a sibling) reports the Docket's real state
  from the mint, and `fleet-status.html` shows it instead of "not walked yet."

### 7 · Verify Amenti Studios Phase One
The podcast tube is marked `planned`. Studios (source material, not spec) says
the keystone — `/speak` content-addressed R2 caching — was "buildable, status
unconfirmed." Confirm whether it ever shipped before treating the tube as live.
- **Unblocks:** the podcast tube's true state is known, not assumed.
- **Acceptance test:** a read of the Worker confirms whether `/speak` persists
  to R2; `fleet.json`'s podcast state is updated to match reality.

### 8 · The deck-card crops
Several cards on the arena deck read too tight — Bram Stoker, Helen Keller,
Seneca named so far. The crop rule (`object-fit:cover; object-position:50% 20%`)
suits most cards; a few need per-card overrides or `contain`. The captain will
**walk the deck and bring the list** rather than change the global rule.
- **Unblocks:** the deck reads right without disturbing the 48 cards that are fine.
- **Acceptance test:** the named cards show their subject fully; the rest are
  unchanged.

### 9 · The churn signal (idea, not yet a build)
`SOURCES.semantics.json` has been edited often lately. Raw edit-counts are
vanity — git already has them. The *useful* form is a finding: a small probe
reads git's own history and flags files churning unusually for their kind, the
way the drift report flags unindexed files. **Recorded as an idea; not worth
building over higher-value work.** Promote to its own slipway if it earns it.
- **Unblocks:** nothing yet — held in reserve.
- **Acceptance test:** n/a until adopted.

---

### 10 · Decide the direct-push workflow (PROPOSED — see its own brief)
The download-edit-upload loop is a tax on every session, and hand-editing is off
the table. A full proposal exists: `BRIEF-THE-DIRECT-PUSH-QUESTION.md` — the
assistant commits to the repo directly via a fine-grained GitHub token, with
safety rails (branch-not-main, diff-then-approve, revert, start-small). NOT
adopted. The captain flagged the real risk: a faster workflow carries faster
mistakes, and the manual slowness has been an unplanned checkpoint the whole
history of the project. Rejected along the way: breaking up Page1 (the monolith
is a VIRTUE in an already-fragmented system — do not fragment the one coherent
artifact). Move: read the brief, decide adopt-or-keep-manual, and if adopt, pick
the rail and the Phase-1 file. The manual road stays open until then.

### 11 · Close the card-originals exposure (DECISION PENDING — the last known hole)
The deck cards and terminal plates on the site (`img/{key}-card.jpg`,
`-terminal.jpg`, `-thumb.jpg`) are baked DISPLAY versions. The ORIGINALS —
full-res source images before cropping — live ONLY on the captain's hard drive.
One copy, one disk, nothing watching it. A true single-point-of-failure, and the
last known hole after the library was closed.

WHAT WE KNOW (read 25 Aug):
- `img/MANIFEST.json` records each image's provenance — `source` (original
  filename, e.g. `openart-sample_…jpg`), `crop` (e.g. "trimmed 16px to 0.571"),
  `prompt_file`, `seed`, `note`. So the RECIPE is known and in the repo.
- But the original FILES are referenced by name only — they are NOT in any repo.
- The crop is lossy: display versions cannot rebuild the originals.

OPTIONS (weighed, not chosen):
- A · private `Amenti-Originals` repo — rides the ARK (add it to the Ark's repo
  list → daily verified off-provider backup automatically); instrumentable later.
  RECOMMENDED fit for this ship. Caveat: full-res images can make a repo heavy.
- B · R2 — cheaper for large binaries, but not versioned and needs its own upload
  path.
- C · external/cloud drive — simple, but uninstrumented (Silent Signature: nothing
  would know or verify it happened).

STANDING RULES: do NOT put originals in the PUBLIC `img/` (masters ≠ display, and
they'd bloat the site). Do NOT delete from the hard drive — add copies, never move.
If a repo is chosen, the ARK's repo list must be extended to include it (it bundles
six today).

Captain not ready to decide (25 Aug) — correctly deferred; moving irreplaceable
source files deserves fresh eyes, not the end of a long session. Move: pick the
home (A/B/C), get the originals off the single drive, confirm the Ark covers it,
then (later) instrument it against the MANIFEST so you can SEE which originals are
safely stored.

---

## ADDED 31 AUGUST 2026 — the hall, the corps, and what the last session left

Eight findings from the 29–30 Aug session reached a log and a handoff and never
reached this file. That is the fault this slip exists to prevent, and it is
recorded here rather than quietly corrected. A ninth — the decision to make Ask
Amenti *one box containing several* — was made in an earlier session and exists
nowhere at all; it survived only because the captain remembered it and said so.

### 12 · THE HALL'S ENGINE IS OVER THE WALL — Ask Amenti does not answer
**Live, and the only fault here that a visitor could hit.** The engine
(`amenti-hall.js`) assembles a system prompt of **24,208 characters against the
proxy's `SYSTEM_CHARS` of 20,000.** The Worker refuses it with
`system_too_long` — a 413 with a named reason in the body. It does not truncate.
So this is not a degraded hall giving worse answers; it is a silent one.

Measured 31 Aug by `probes/probe-hall-wall.mjs`, which lifts and runs the hall's
own `catalogueText` and `buildSystem` rather than a copy of them:

```
HALL.md          5,751
the counts         599
the catalogue   16,160    190 entries, 85.1 chars each
the rest         1,698    preamble and the nine rules
SYSTEM PROMPT   24,208    wall 20,000 — over by 4,208
```

The hall as a *place* is fine — the page loads, the image shows, the box takes
typing. Only the answering fails.

- **The stopgap:** the gloss trim at `amenti-hall.js` line 115 is 90 chars.
  At 40 the prompt fits with ~2,000 to spare. **It buys about three weeks** at
  the observed growth of ~14 documents a week, and costs gloss quality. It is
  triage, not a fix, and it should not be mistaken for one.
- **Unblocks:** Ask Amenti answers at all. #5 becomes affordable again.
- **Acceptance test:** open the hall, ask a question, get an answer — and
  `node probes/probe-hall-wall.mjs` exits 0.
- **Do not raise the wall to fix this.** The Worker's own policy is *if a
  surface 413s here, CHUNK THE SURFACE*, written after a real overrun. Raising
  it is a decision for #13, taken deliberately, not a patch taken tonight.

### 13 · DECIDE WHAT REPLACES DECLARE-EVERYTHING (DECISION PENDING)
**The structural version of #12, and the one that matters.** The hall sends the
whole catalogue on every question by design, because a retrieval pass can miss
and never say it missed. That principle is right and this move does not argue
with it. But it costs one line per document, forever, and the corpus grows.

The captain's decision, recorded: **Ask Amenti becomes one box containing
several** — a single surface that answers about the architecture, about history,
and about a person, so a visitor need not already know which chat surface
answers which kind of question. Mostly inward-facing, because the primary-source
library is the point. The works are called and cited; next they must be
searched and worked with.

**Declaring everything cannot survive that. Not tightly — at all:**

```
the architecture     190 documents
the library          550 works
the roster         1,011 souls
                   ─────
                   1,751 entries

at today's gloss   148,835 chars    7.4x the whole wall
at a hard trim      87,550          4.4x
at bare ids          36,771         1.8x the wall, 3.1x the space actually free
```

Every description deleted still overruns three times. There is no trim that
reaches it.

**Retrieval is not tight — it is roomy.** Forty results at full 85-char gloss
cost 3,400 chars and leave ~8,552 of the wall for meaning and passages.

Three things that shape the decision:
- **The routing is already built.** `AmentiHall.find()` searches `SOURCES.json`
  and `ROSTER-INDEX.json` with **no model call and no cost.** It ships today and
  nothing uses it for this. Read it before building anything (`SERVES`).
- **The honesty property must be built in from the first line.** The objection
  to retrieval is *silent* missing, not retrieval. A pass that states its own
  coverage — searched 1,751, read 12, and here is what it did not open — keeps
  the ethic. Added later, it will not be added.
- **The fixed cost is the wrong content for most questions.** `HALL.md` is 5,751
  chars, 29% of the wall, and it is the ship's meaning. Exactly right for *ask
  the architecture*; largely wasted on *what did Caesar write*. A box with lanes
  should choose **what meaning to carry**, not only what to retrieve.

- **Unblocks:** Ask Amenti can grow past ~250 entries at all; the library
  becomes searchable rather than only cited.
- **Acceptance test:** none yet — this is a decision, not a build. It graduates
  to its own slipway once the road is chosen. The move is: choose between
  retrieval-with-declared-coverage, purpose-built short glosses, cutting the
  fixed 40%, and a deliberate wall change — and write the choice down.
- **A NAMING CAUTION.** `modes` is taken: the terminal's five ways a figure
  speaks, with a control on the page and `setMode` behind it. `throttle` is
  taken: `amenti-throttle.js`, retired, guarded by probe17. `registers` is
  taken. Whatever the lane-selector is called, it needs a free word.

### 14 · Put `probe-hall-wall` on a rung
`probes/probe-hall-wall.mjs` landed on `main` 31 Aug and **nothing invokes it.**
A probe that has never run is a prayer. `patrol.yml` fires only
`probe-watches` and `probe-ordnance`, so the rung is whatever workflow fires
`probe-hall` — which has never been identified.
- **Unblocks:** the wall is watched instead of discovered; #12 cannot recur
  silently.
- **Acceptance test:** the workflow runs, and a deliberate overrun fails the
  build with the probe's FAIL in the log.
- **Order matters:** the walk, then `probe-hall`, then `probe-hall-wall`. See
  #15 — that ordering closes a second fault as a side effect.

### 15 · `probe-hall` has no freshness check on what it reads
It takes `documents_indexed` straight from `srcs.counts.reachable`, so its
counts are only as fresh as the walk that ran before it. On 30 Aug it ran at
18:44 against a register the walk did not update until 01:08, and the hall is
now permitted to state **187 documents while the register holds 190.**

Its own header says *a count that is silently stale is the fault this place was
built to refuse* — but the guard it implements only nulls a register it cannot
**read**. A register that reads fine and is six hours behind passes straight
through.
- **Unblocks:** the hall states no number that is quietly out of date.
- **Acceptance test:** `HALL-STATE.json` carries the `generated` stamp of the
  `SOURCES.json` it read, and the probe says so when they diverge.

### 16 · The Probe Corps roster is six weeks stale, and `probe3` carries a false green
`Amenti_Probe_Corps.html` is Rev B, 19 July. It says *when you ask "where are the
probes?", the answer is here*, and for roughly sixteen of them it is not —
`probe-hall`, `probe-citations`, `probe-engine`, `probe-gate`, `probe-library`,
`probe-serves`, `probe-surfaces`, `probe-voice`, `probe-works`, `probe-post`,
`probe-production`, `probe-spells`, `probe21`, `probe-page1`, `probe-roster`,
`probe-panes` are all absent, and `probe-hall-wall` is new.

**Worse, the doctrine and the register disagree about `probe3`.** The roster
calls it THE PHANTOM, guarding script injection. `SOURCES.json` says it is Page1
integrity and that it **carries a false green** — a section reading one file into
two variables and asserting they are equal, an assertion that cannot fail. The
register wins. So a probe that cannot fail is patrolling, and the doctrine points
at a different probe entirely.
- **Unblocks:** the corps' own doctrine stops being a source of false comfort.
- **Acceptance test:** the roster lists every probe in `SOURCES.json`, `probe3`
  is described as the register describes it, and its false-green section either
  asserts something that can fail or is removed and its absence recorded.

### 17 · Caesar may be speaking in the wrong voice
The terminal displays **GAIUS JULIUS CAESAR**; `names.csv` holds **Julius
Caesar**; the voice resolver keys on that exact lowercased string. This is
Lincoln's fault on a different figure, and it is live. Not settleable from the
registers — neither Page1 nor Page2 contains the lookup; it is inside
`amenti-core.bundle.js`.
- **Unblocks:** a figure speaks in the voice he was cast in.
- **Acceptance test:** press CALL on Caesar; the console does **not** say
  `NO GENDER RESOLVED`.

### 18 · The nine rooms that name a translator and stop short of an edition
The citation work is **done** — 550 works, 495 cited, EMPTY zero, 42 of 52 rooms
clean, and `citations.yml` fails the build on an empty source. What remains is
nine rooms naming a translator without an edition. **Not urgent and nothing is
wrong.** Written up in full, with the method and the acceptance test, in
`Amenti.live/main/slip/SLIP-ADDENDUM-THE-EDITIONS.md`.
- **Acceptance test:** read the addendum; do not plan this from memory.

### 19 · The three instruments that never run
`probe-post.mjs`, `probe-serves.mjs`, `probe-works.mjs` sit in `probes/` and
nothing invokes them. Being loaded is not being used. **`probe-serves` first** —
it is the guard against building the same thing twice, and should fire whenever
`SERVES.semantics.json` changes. Two things were built twice in one session
because nothing did.
- **Acceptance test:** each appears in a workflow, and a deliberate fault in the
  register it guards fails a build.

### 20 · Delete `WORKS.semantics.json` if it landed
It duplicates `LIBRARY.json`, which holds 550 properly cited works. Built before
looking. Remove its entry from `SOURCES.semantics.json` too.
- **Acceptance test:** the file is absent and the index does not name it.

### 21 · Four small ones from the 29–30 Aug log
Recorded so they are not rediscovered by accident. None is large.
- **`quiz-close` is declared twice** in the CSS; the later, stale copy is the one
  that runs. Ten minutes.
- **`amenti-visits.js` is never mounted** on Page1 — one counted surface of five.
- **`acceptsSystemTail` is unset.** A 33% saving, measured, unclaimed.
- **The source index does not walk root `.js`,** so the whole engine —
  `amenti-hall.js` included — is invisible to `SOURCES.json`.
- **Acceptance test:** each has its own and each is one line; take them when a
  session is already in that file, not as a campaign.

### 22 · Twenty-one briefs are unindexed
Inherited from the closed #4. The walk reaches 191 paths and 21 are in no
semantics entry, nearly all briefs in `Amenti-Technical-Briefs` — including
`BRIEF-THE-DIRECT-PUSH-QUESTION.md`, the brief for move #10. A brief the index
cannot see is a brief the hall cannot cite.
- **Unblocks:** the drift report reads clean; #10's own brief becomes findable.
- **Acceptance test:** the source index run reports `unindexed: 0`.

---

## THE CRITICAL PATH — what gates what

Reordered 31 Aug. A live fault on a visitor-facing surface outranks the fleet
work, and the fleet work is unchanged beneath it.

| # | Move | Unblocks |
|---|---|---|
| 1 | Make Ask Amenti answer at all (#12) | the surface stops being silent |
| 2 | Decide what replaces declare-everything (#13) | the box can grow past ~250 entries |
| 3 | Put `probe-hall-wall` on a rung (#14) | the wall is watched, not rediscovered |
| 4 | Wire `probe-ordnance` to `fleet.json` (#1) | the autonomy loop closes |
| 5 | Wire THE WEEK's cron (#2) | resumption begins; a press fires |
| 6 | Fix the Dispatch sensor (#3) | the fleet status can be trusted |
| 7 | Walk the Docket + Studios (#6, #7) | the last two tubes become readings |

**#12 and #13 are one problem at two timescales.** #12 is triage that buys about
three weeks; #13 is the road. Doing #12 alone and calling it closed is the
failure this entry exists to prevent — the reason it stands above #13 is only
that a silent surface should not wait on a design decision.

Items 8, 9, 15–22 are independent — do them when they surface, not in sequence.

---

## DECISIONS THE ASSISTANT SHOULD NOT MAKE ALONE

- **Arming THE WEEK's cron** — it touches the Worker that handles publishing.
  Dry-run, confirm, then the captain arms it.
- **Any change to the `dailyplanet:` mechanism** — the name is legally and
  structurally load-bearing. Surface-only, always.
- **Which deck cards are wrong** — the captain walks the deck; the eye is the
  instrument here.
- **Where the card originals live / moving the source files** — irreplaceable
  art, real storage decision (repo vs R2 vs drive), possibly a new repo + the
  Ark's repo list. The captain decides the home; don't move files without it.
- **What replaces declare-everything in the hall (#13)** — it decides the shape
  of the surface the captain has twice called the important one, it touches the
  Worker's `SYSTEM_CHARS` policy, and it trades a principle (nothing can be
  missed silently) for a budget. The assistant measures, lays out the roads, and
  writes the choice down. **The captain picks the road.**
- **Adopting direct push / creating a write-token** — it changes how the whole
  ship is built and can reach the live flagship in one motion. The captain
  decides if and when, and it stages in (see the brief). Never push to `main` on
  `Page1.html` unattended.

---

*Updated 31 Aug 2026: moves 12-22 added, #4 closed by supersession, #5 blocked,
the critical path reordered. Eight of those moves had been sitting in a log and a
handoff since 30 Aug without reaching this file, and one design decision existed
only in the captain's memory. If a session surfaces a move and it does not land
here, the session did not happen.*

*Opened 24 Aug 2026, seeded from the fleet-legible session and its briefs. Add
a move when a session surfaces one; close it when its test passes; graduate it
to its own slipway when it grows phases. Read this at the top of a session — it
is the yard's memory between the tides.*
