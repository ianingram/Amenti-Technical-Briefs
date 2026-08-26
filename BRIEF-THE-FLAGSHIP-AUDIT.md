# BRIEF — THE FLAGSHIP AUDIT
**Ingram Manor LLC · read of `Page1.html` · 25 August 2026**

A mechanical read of the flagship, taken because the ship instruments its
library, its panes, its fleet and its ark — and does not instrument the one
artifact all of them exist to serve.

**What was read:** `Page1.html` (519,093 chars · 8,510 lines · 28 inline script
blocks · 24 external scripts · 26 inline style blocks · 156 `id` attributes).
Read by machine, not by eye. Every finding below cites a line.

This brief obeys the slipway's law: every item ends in a check the captain can
perform by opening something.

---

## WHAT IS ALREADY RIGHT — stated first, so it is not disturbed

The monolith is not the mess its size implies.

- **The Flight Recorder** (line 4) is inline, first in `<head>`, sub-kilobyte,
  no network. Two independent methods for main-thread blocking, and it already
  learned that a hidden tab looks like a frozen one and corrected for it. This
  is real instrument-building.
- **The diagnostic is opt-in** — 47 KB that loads only on `?diagnose=1` (8,045).
  Someone already found that cost and moved it off every visit.
- **`amenti-tabs.css` is preloaded, not blocking** (845), with a `<noscript>`
  fallback. Deliberate.
- **18 of 28 inline blocks are IIFE-scoped.** Someone was thinking about it.
- **The empty glass is honoured in the tail script** (8,489) — a failed
  `LIBRARY.json` fetch leaves the fallback showing rather than blanking.
- **21 of 24 external scripts are `defer`.** Order was deliberately removed as a
  dependency — the comment at 5,614 says so explicitly.

**The monolith is a virtue and stays a monolith.** Nothing below asks to split
it. (See STANDING SLIP #10, already settled.)

---

## RED — silent, live now, user-visible

### R1 · The Codex key-list race
**Two writers, one global, no ordering guarantee.**

- Line 5,613 (inline, parse-time): `window.AMENTI_LIBRARY_KEYS = window.AMENTI_LIBRARY_KEYS || [9 hardcoded keys]`
- Line 8,489 (tail, after `fetch`): `window.AMENTI_LIBRARY_KEYS = d.unlockedKeys` — **52 keys, unconditional, async**
- Line 5,695–5,697: the Codex builds its OPEN buttons from
  `(window.AMENTI_LIBRARY_KEYS||[]).indexOf(c.key)`

The fallback is correctly guarded with `||`. The repair is not. The tail sets
the true list and then calls the refresh — but behind a guard:

```js
if(window.AmentiCodexRefresh) try{ window.AmentiCodexRefresh(); }catch(e){}
```

If the fetch resolves **before** `AmentiCodexRefresh` is defined (warm cache,
slow deferred script — an ordinary Tuesday), the guard is false, nothing
refreshes, and nothing is recorded. The `codex-count` label reads **52** while
the roster offers **9** OPEN buttons.

That is the empty glass inverted: not a missing reading, but a stale one
rendered as current, with a green lamp over it. Worse than the hardcoded 9 it
replaced, because the hardcoded 9 was at least consistent with itself.

- **Fix:** make the reading a promise, not a race. Publish
  `window.AMENTI_LIBRARY = fetch(...)` from the head and have the Codex `await`
  it at render time — or, minimally, have the tail set a pending flag the
  builder checks when it defines `AmentiCodexRefresh`. Either way the guard must
  never be able to fail *silently*.
- **Acceptance test:** load Page1 with the network throttled to Slow 3G, then
  again from a warm cache. In both, the eyebrow count and the number of OPEN
  buttons agree. Then load with `LIBRARY.json` blocked in devtools: both read 9.

### R2 · Duplicate `id="quiz-close"` — a dead button
Two elements (5,114 and 5,147), two bindings (5,131 and 5,159). Both
`getElementById` calls resolve the **first** button. The second modal's ✕ is
inert, and the second binding silently re-wires the first.

- **Fix:** unique ids, or bind by class within the modal's own scope.
- **Acceptance test:** open the second quiz surface and click ✕. It closes.

### R3 · Duplicate `dispatch-card` / `dispatch-feed` / `dispatch-court`
Static markup at 2,910/2,913; an injected copy written by `innerHTML` at
3,470–3,472. Three consumers — 3,090, 3,505, 3,509 — all `getElementById`, all
resolve whichever is first in the DOM.

If the injection replaces its container this is harmless. If both are ever in
the document at once, one dispatch card is wired and the other is decoration,
and which one you get depends on render order.

- **Fix:** decide which is canonical and delete the other; if the injected one
  is canonical, scope its lookups to the injected container.
- **Acceptance test:** in devtools console,
  `document.querySelectorAll('#dispatch-card').length` returns `1` on every tab
  of the page, before and after the dispatch renders.

---

## AMBER — drift surfaces

### A1 · The cache-bust rule is stated and not kept
STANDING RULE: *"bump `?v=` on css/js in Page1; verify by CONTENT not 200."*

Of the local assets referenced, **two carry a version**: `amenti-tabs.css?v=7`
and `amenti-diagnose.js?v=21`. The other 24 external scripts,
`amenti-responsive.css`, and `img/grades.css` carry none.

A rule that is written down and obeyed 2 times in 26 is not a rule; it is a
description of two files. Every unversioned deploy is a coin-flip on whether a
returning reader gets the new code — and it will *usually* work, which is what
makes it expensive.

- **Fix:** one build-stamp token, applied to every local `src`/`href` by the
  same hand that deploys.
- **Acceptance test:** after a deploy, a hard-refresh and a normal refresh serve
  byte-identical JS. Verified by content hash, not by 200.

### A2 · Two counts of one thing, from two sources
- `codex-count` (4,239) — written from `LIBRARY.json` → **52**
- `cdx-count` (4,248, rewritten at 5,643) — written from `AMENTI_CHARS` → `n / n`

Same page, same concept, two registers. They will disagree the moment the
library and the roster diverge, and neither is wrong from where it stands.

Also frozen in the markup: `LAST SYNC 04:22 UTC` and `FILE: AMENTI/COD/v0.4.9`
(4,243). Both are already on the handoff's hardcoded-count list; naming their
lines here so the audit does not have to be repeated.

### A3 · Supabase is unpinned and unverified
Line 8,010: `cdn.jsdelivr.net/npm/@supabase/supabase-js@2` — a floating major
tag, no `integrity`, no `crossorigin`. A minor release changes auth behaviour
overnight with no commit in any repo; a bad day at the CDN gets full DOM access
including the session.

- **Fix:** pin the exact version, add an SRI hash. Better: vendor it and let the
  Ark hold it.
- **Acceptance test:** the `<script>` tag names a full semver and an
  `integrity=` hash, and the page still authenticates.

### A4 · Ten inline blocks in shared global scope (~68 KB)
Lines 4, 5,613, 6,746, 6,798, 7,134, 7,252, 7,837, 8,408, 8,436, 8,449, 8,489.
In an 8,510-line file, a redeclared `var d` is silent and the symptom appears
somewhere else entirely.

- **Fix:** wrap them as the other 18 already are. Mechanical, low-risk,
  one block at a time.
- **Acceptance test:** `document.querySelectorAll('script:not([src])')` count
  unchanged; the page behaves identically; the audit probe (below) reports
  `globalScopeBlocks: 0`.

### A5 · Three render-blocking scripts mid-body
`amenti-core.bundle.js` (893), `amenti_audio_pipeline.js` (7,265),
`amenti_voice_glow.js` (7,309). The other 21 are `defer`. Worth confirming the
three are deliberate — the Flight Recorder can already tell you what they cost.

### A6 · Two fetches without a `.catch`
Line 3,322 (library catalog) and 7,984 (`/article/generate`). Both `throw` on
`!r.ok` into nothing. Fourteen fetches, seventeen catches — these are the two
gaps.

---

## THE STRUCTURAL FINDING — and the move that follows

The Flight Recorder measures **performance** and reports to **a human who
typed `?diagnose=1`**. It does not persist, does not produce a register, and no
pane reads it. It also does not watch for **errors** — there is no
`unhandledrejection` handler anywhere in 519 KB, and a throw in any of the 28
inline blocks kills every block below it in that script and reports nothing.

So: the library has a librarian. The panes have a probe. The ark verifies
itself daily and reflects through the gate. **The flagship has a stethoscope
that only works when someone is holding it.**

Every red finding above was found in about four minutes by a machine reading the
file. None of them required judgement. That is the definition of work an
instrument should be doing.

### MOVE — `probe-page1.mjs` → `PAGE1.json` → a pane
Same shape as the librarian. It walks `Page1.html` and reports what is
*actually* there:

| reading | why |
|---|---|
| duplicate `id`s | R2 and R3 were found this way |
| local assets referenced but **missing on disk** | the librarian's exact trick, applied to the flagship |
| unversioned local `src`/`href` | A1, as a number that shames itself |
| inline blocks in global scope | A4, trending to zero |
| `fetch(` without a reachable `.catch` | A6 |
| bare numerals in text nodes matching `\d+\s+(ENTRIES|SOULS|WORKS)` | the frozen-number audit, automated forever |
| bytes, line count, script/style block counts | drift over time is the signal |

Plus a ~20-line **beacon** in the head, next to the Flight Recorder:
`window.onerror` and `unhandledrejection` into `window.__AT`, so the recorder
carries correctness alongside performance.

- **Unblocks:** the flagship becomes a reading like everything else. The Atlas
  gets a row. The hardcoded-count audit (handoff #7) stops being a task and
  becomes a number that goes to zero.
- **Acceptance test:** delete a referenced JS file locally, run the probe, and
  `PAGE1.json` names it as missing. Introduce a duplicate id; the probe catches
  it. Then fix R2 and watch the count drop.

### Why this precedes the direct-push decision (SLIP #10)
The captain's stated objection to direct push is correct: *a faster workflow
carries faster mistakes, and the manual slowness has been an unplanned
checkpoint.*

An instrument that reads the flagship after every change **is that checkpoint,
made deliberate.** Right now the only thing standing between a bad push and a
broken flagship is how long it takes to upload a file — which is a checkpoint by
accident, and one that stops working the day the upload gets fast.

Build the probe first. Then the direct-push question is no longer *"do we
remove the safety net?"* — it is *"do we replace an accidental net with a real
one?"* That is a different question, and a much easier one.

---

## PROPOSED FOR THE STANDING SLIP

**#12 · Instrument the flagship** — `probe-page1.mjs` + `PAGE1.json` + a pane +
the error beacon. Ranked **above #10 (direct push)**, which should not be
decided until the flagship can report its own state.

**#13 · Close R1, R2, R3** — three small fixes, each with a test above. R1 first;
it is the only one that lies to a reader.

---

*Read of 25 Aug 2026. Every line number in this brief refers to `Page1.html` as
uploaded that evening; re-read before acting if the file has moved since. The
reading is cheaper than the guess.*
