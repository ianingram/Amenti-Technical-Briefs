<!-- BRIEF-WHAT-AN-ANSWER-COSTS.md
     →  Amenti.live/BRIEF-WHAT-AN-ANSWER-COSTS.md -->

# WHAT AN ANSWER COSTS
## the cost architecture of the hall and the ground, and where the money is
### 9 September 2026

---

## THE ONE THING TO KNOW FIRST

> **THERE IS EXACTLY ONE PAID DOOR ON THIS SHIP AND IT IS THE ASK BOX.**

Everything else — the map, Attica, the glass, the cues, the tours, the lives
pane, the frame picker, the reading list — is `fetch` a file and draw. No model,
no charge, no latency beyond a CDN.

`amenti-hall.js` says it in its own error text: *the hall speaks through the
one door*. Anything that adds a second paid door is a change to the ship's
economics and should be argued for as one.

---

## THE DOOR, TRACED

```
hall.html          window.claude.complete  →  POST amenti-proxy.ingram-ian.workers.dev
                   MODELS  claude-haiku-4-5-20251001 · claude-sonnet-4-6
                   MODEL   claude-sonnet-4-6            ← the default in force
                   records window.AmentiCost { turns, inputTokens, outputTokens, last }

amenti-hall-box.js the box. SEARCH FIRST — names and fragments never reach the
                   model. Only a genuine question does.
amenti-hall.js     builds the prompt, calls the door, renders the answer
amenti-meter.js    reads AmentiCost, prices it against RATES.json, shows it
RATES.json         dollars per million tokens, per model
```

**THE SEARCH-FIRST RULE IS A COST CONTROL AND SHOULD BE READ AS ONE.** Type
`Caesar` and the box searches the local index for nothing. Type `what did
Caesar think of Cato` and it spends. A change that sends more strings to the
model is a change to the bill, however it is framed.

---

## THE WALL · what the hall actually sends

`amenti-hall.js` budgets its prompt to the character and states the wall in its
own comments. This is not an estimate.

```
HALL.md + the counts + the rules      8,600 chars   (its own figure)
MAX_WORKS 4 × WORK_SLICE 780          3,120         primary source
SECTION_BUDGET                        5,800
NOTE_BUDGET                             900
                                     ------
                                     18,420 chars against a declared wall of 20,000
```

Roughly **5,100 input tokens** on the answer call, plus a smaller router call.
`probes/probe-hall-wall` is the instrument that measures against the wall, and
the file says plainly: *raising any of these without re-running probe-hall-wall
is how the hall goes silent again.*

**AND THE BUDGET IS A SET OF TRADES, EACH RECORDED.** WORK_SLICE went 2,000 →
1,750 → 1,500 → 780 as rules were rewritten and the séance epigraph moved to
the top of HALL.md, and each move names what it bought. The file also names
where the room grows back: *HALL.md, at 5,751, is 29% of the wall spent
carrying the ship's architecture into a question about Livy.*

---

## THE NUMBER

Priced from that budget, at rates read 9 Sep 2026:

```
claude-sonnet-4-6     ~$0.025 per ask     $25 per 1,000     $254 per 10,000
claude-haiku-4-5      ~$0.008 per ask     $8.45 per 1,000    $85 per 10,000
```

**AND THE FIRST ESTIMATE OF THIS WAS WRONG BY TWENTY-FIVE TIMES.** It totalled
the files the hall READS — `SOURCES.json`, `LIBRARY.json`, `ROSTER-INDEX.json`,
452 KB between them — and assumed they went to the model. They do not. The hall
opens three rooms and four passages out of that and sends the selection.

> **READ THE BUDGET BEFORE PRICING THE PROMPT. THE HALL HAD ALREADY SOLVED THE
> PROBLEM THE ESTIMATE WAS ALARMED ABOUT.**

---

## THE REGISTERS THIS RESTS ON

**`RATES.json`** — dollars per million tokens, per model. A register and not a
constant, so a price change is an edit. Its own law: *a rate here is a claim
about a bill and must be checked against the Console. If the meter and the
invoice disagree, THE INVOICE IS RIGHT and this file is wrong.*

Three refusals are written into it and must survive any edit:

- **A model with no entry is UNPRICED BY NAME, never priced at zero.** The
  meter shows tokens and withholds dollars, because a price from a stale
  constant looks like a measurement.
- **Cached reads and batch discounts are not modelled.** Both make the real
  bill lower, so the meter reads HIGH — the safe direction for a number
  somebody is budgeting against.
- **The rates came from third-party trackers, not from an invoice**, and the
  file records that in `source`.

**`window.AmentiCost`** — written by `hall.html` on every proxy reply since it
was written, and read by nothing until 9 Sep. Turns, input tokens, output
tokens, and the answering model. **THIS BROWSER, THIS PAGE LOAD, AND NOBODY
ELSE.**

---

## WHAT NO BROWSER CAN SEE

A visitor's tokens are counted in the visitor's browser and never arrive here.
`amenti-meter.js` says so on its own face, at the bottom of the panel, because
a meter that looked like a business total and was one person's session would be
the worst instrument on the ship.

> **THE PROXY IS THE ONLY PLACE THAT SEES EVERY REQUEST, AND IT COUNTS
> NOTHING.**

`amenti-proxy.ingram-ian.workers.dev` answers `405` to a GET; it is POST-only.
Its source is **not in this repository**, which is itself a finding: every other
load-bearing piece of this ship is plain text under version control, and the one
component that could answer *what am I paying this month* is not.

That work is SLIP #87 and is unstarted. What it needs:

- tally `input_tokens` and `output_tokens` per model and per day into KV
- `GET` returns the totals as JSON, so the meter can show this page load AND
  all time side by side
- **COUNT, NEVER CONTENT.** Tokens and model only \u2014 no questions, no answers,
  no addresses. A proxy that logs what people asked is a different product with
  different obligations.
- KV loses writes under concurrency; at this traffic that is a rounding error
  and the file should SAY SO rather than leave it to be discovered. The fix, if
  it ever matters, is a Durable Object.

**AND EVERY ASK BEFORE THE PROXY STARTS COUNTING IS GONE.** The counter has
reset on every page load since it was written. No total exists for any period
before that work is done.

---

## THE OTHER HALF · why the ground is free

The map answers WHERE and the lives pane answers WHY, and neither calls a
model. That is not an accident of implementation; it is the point.

**A HOVER THAT WOULD HAVE BEEN AN ASK IS NOW A FETCH OF A CSV.**

```
ATTICA-LIVES.csv   the ore      terse dated claims, each with what it rests on
ATTICA-TOLD.csv    the telling  the prose, written ONCE from the ore and stored
```

The prose could have been generated on hover. It is not, for three reasons and
the third is the one that matters:

1. it would cost a model call per hover, for ever
2. it would arrive slower than a fetch
3. **IT WOULD READ DIFFERENTLY EVERY TIME, SO A SENTENCE COULD NEVER BE
   CORRECTED AND STAY CORRECTED**

The generation happened once, at authoring, by a model. The serving is a file.
That is the shape every future feature of this kind should take: **generate at
authoring time into a register, serve the register.**

`standing` on each ore line records what the claim rests on — `corpus` for a
claim in a named room of this library, `record` for general history that is not
checkable here, `inference` for a join somebody made. A `corpus` line names its
document, so a probe can open the file and check it. **THE LIBRARY BECOMES THE
CHECKER AND NOT ONLY THE POINTER**, which is what lets volume and rigour rise
together instead of trading against each other.

---

## THE LEVERS, IN THE ORDER THEY BITE

1. **Model.** Haiku 4.5 is already configured in `MODELS` and is a third of the
   price. Whether the hall's answers survive it is a real question and not an
   obvious one: one switch, one evening of comparison.
2. **The model string is a generation behind.** `hall.html` defaults to
   `claude-sonnet-4-6`; Sonnet 5 replaced it in June. Confirm the proxy still
   resolves it before assuming today's price.
3. **Prompt caching — CONDITIONAL, AND THE CONDITION IS NOT MEASURED.** The
   fixed 8,600 characters are identical on every ask and are re-billed every
   time. Marking them as a cached prefix bills a later call at roughly a tenth
   of input price. The prefix must be byte-identical, must come first, must
   clear a minimum of about a thousand tokens (8,600 chars is ~2,400, so it
   does) — **AND IT EXPIRES IN ABOUT FIVE MINUTES.**

   ```
   no caching     $0.0254 per ask
   cache write    $0.0271   the first ask, and any after the window lapses
   cache read     $0.0189   an ask inside the window
   break-even     22% of asks must land within five minutes of another
   ```

   **BELOW THAT IT COSTS MORE THAN IT SAVES.** On a quiet site where asks
   arrive an hour apart, every one is a cache write at +7%. On a site where a
   visitor asks four questions in a sitting, three read cheap and the saving is
   around 20%.

   Whether asks cluster is a fact about traffic that ONLY THE PROXY CAN SEE.
   **COUNTING COMES BEFORE CACHING**, not after — turning this on without the
   hit rate is guessing with the bill.

   *An earlier draft of this brief called caching `the largest single saving
   available`. That priced the discount and not the hit rate.*
4. **The wall itself.** `HALL.md` spends 29% of the budget carrying the ship's
   architecture into questions about Livy. Scoping it per lane is SLIP #13 move
   F and returns thousands of characters at once.
5. **Move answers into registers.** Every question that gets pre-written into a
   file is a question nobody pays for again.

---

*Registers: `RATES.json`, `ATTICA-LIVES.csv`, `ATTICA-TOLD.csv`.
Modules: `amenti-meter.js`, `amenti-hall.js`, `amenti-hall-box.js`,
`amenti-attica-hall.js`. Slip #87.*
