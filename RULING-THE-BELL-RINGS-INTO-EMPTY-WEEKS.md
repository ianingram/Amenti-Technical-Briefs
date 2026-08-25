# AMENTI — THE BELL RINGS INTO EMPTY WEEKS
**Ingram Manor LLC · 25 August 2026 · a reading, correcting a lost memory**

## WHY THIS EXISTS

For weeks the fleet status showed THE WEEK as the one red card — "0 fired,"
"never delivered," the tube that would not fire. Two sessions diagnosed it as a
missing or commented-out cron. **That diagnosis was wrong.** This brief records
what the `amenti-mint` Worker source actually says, so the error is never
repeated: the knowledge had become a memory, and the memory was mistaken. Read
from the deployed mint source, 25 Aug.

---

## THE ONE-LINE TRUTH

> **The cron is armed and ringing. It rings weekly, Monday 00:00 UTC, on
> amenti-mint. It shows 0 fired because it has been ringing into EMPTY WEEKS —
> no votes in the pool to settle. The fix is votes, not a cron edit.**

---

## WHAT THE MINT SOURCE SAYS

- **The schedule is `0 0 * * mon` (Monday 00:00 UTC), DEPLOYED and ARMED** on the
  `amenti-mint` Worker. `WORKERS.json` confirms it is the only live cron in the
  fleet. It is not missing and not commented out. (The earlier reading of
  "`0 12 * * 0`, Sunday noon, commented out" was incorrect — that schedule is
  not deployed anywhere.)

- **Firing is a SETTLEMENT, not a plain publish.** Each Monday the bell rings and
  `settlePool()` settles that week's votes/arguments into verdicts, distributing
  the fixed pool (POOL_SIZE = 500 ET). A "firing" is a settled week.

- **An empty week rings but delivers nothing — by design.** The mint's own
  comment, verbatim in spirit:
  > *A cron that fired with zero votes and a cron that was never registered look
  > identical from outside — both leave no verdicts, quiet:true, and a settlesAt
  > that rolls forward on its own. A row with ok=true and votes_found=0 means it
  > rang into an empty week — a fact, not a fault.*

  This is the whole explanation for "0 fired." The bell has been ringing on time,
  into weeks with no votes. Not broken — starved.

- **The bell_log is the row that tells the two apart.** `bellWake()` writes a row
  BEFORE the settlement (ok:false), `bellDone()` updates it after (ok:true +
  votes_found). An ABSENT row = the bell never rang. A row with ok=true,
  votes_found=0 = it rang into an empty week. A row with ok=false + error = it
  rang and failed. To know which, read `bell_log`, not the verdict count.

---

## THE DRY-FIRE THE CAPTAIN REMEMBERED

The captain recalled that THE WEEK "cannot fire if a quiz is not taken and a
ruling is not made — it would be a true dry fire; cron counts down, no quiz no
ruling, reset." **That memory was correct.** It is exactly the empty-week ring:
the cron fires, finds zero votes, settles nothing, and `nextSettlementISO()`
rolls the promise forward to the following Monday. The confusion was only about
the cron being "off" — it is not; it is on and ringing empty.

---

## HOW TO MAKE THE NEXT BELL FIRE REAL

1. **Put votes in the pool before Monday 00:00 UTC** — quizzes taken, arguments
   cast this cycle. This is the entire fix. No Worker edit.
2. **Test without waiting for Monday:** `POST /pool/settle` on the mint
   (admin-secret-guarded) rings the bell by hand — logged as `trigger='manual'`
   so a hand-pull is never mistaken for the automatic bell. Use it to confirm
   votes are landing and the settlement produces verdicts.
3. **Verify by reading `bell_log` and the verdicts**, not by assuming — after a
   real settlement, `fleet-status.html` / the ordnance reading should show
   votes_found > 0 and delivered verdicts.

---

## WHAT THIS CORRECTS

- `fleet.json` THE WEEK entry: cron corrected to `0 0 * * mon`, state_reason
  corrected to "armed and ringing weekly; 0 delivered because the pool is empty,
  not because the schedule is broken."
- Any prior brief or handoff saying THE WEEK needs its cron wired/armed is
  **superseded by this.** The cron is fine. Feed the pool.

---

## THE LESSON

This is the fleet's own law turned on itself: *a schedule that nobody checks is
a promise nobody keeps* — but also, **a schedule that IS checked can still be
misread if the reader forgets what firing means.** THE WEEK's "firing" is a
settlement of votes, and a settlement of nothing is a lawful quiet, not a fault.
The instrument (the red card) was right that nothing was delivered; the humans
reading it invented a broken cron to explain a fact that had a simpler cause —
an empty pool. The mint said so all along, in a comment written before the work.

> The bell was never silent. It rang every Monday, into a room with no votes to
> count. Fill the room.
