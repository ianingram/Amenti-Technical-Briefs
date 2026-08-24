# AMENTI — BRIEF: ASCENSION · STAGE 2
**Ingram Manor LLC · 23–24 August 2026 · a shop-floor account**

## HOW TO USE THIS

An account of one long session — roughly seven in the evening to four in the
morning. It is not a manual and it will not be updated: it is correct about the
night it describes and makes no claim about today. **Its counts are of its own
night.** Every number in it was read from a register at the hour of writing,
and the register named beside each is the source thereafter.

The session began with a recovered brief about where a pose lives. It ended
with the building answering questions about itself in the flagship's nav. In
between it closed the last unversioned tier, gave the last hand-made register
an instrument, wrote the vocabulary down, and shipped a voice. The thread was
not planned. It emerged, and it is the title:

> **STAGE 1 TAUGHT THE SHIP TO BE READ.
> STAGE 2 TAUGHT IT TO SPEAK.**

---

## I · The third tier

It surfaced sideways, which is the tell. The pose brief names a table,
`rig_views`; the table appears in no repository; and the first reading of that
absence — that the table was gone — **was not available**, because the
repositories are not a register of Supabase. A table missing from the repo and
a table missing from the provider produce the same silence.

That opened the real finding. The application is three tiers — **Cloudflare
runs it, GitHub defines it, Supabase remembers it** — and two of the three were
held as text and bundled off-provider every Sunday. The third was not. The ark
reported six repositories verified, and the report was true; it was also a
backup of two tiers of three, and nothing said so. The economy's own laws —
*the browser never mints; every payout is idempotent; the ledger is the sum of
its rows* — were enforced by policies and functions that existed in one place,
behind one login, with no second copy.

**The fix: `tools/db-dump.sh` and `.github/workflows/db.yml`.** Schema only,
never rows. A credential scan that quarantines a flagged dump on a
non-committable path. A register, `db/SCHEMA.json`, that writes `state: FAILED`
and `counts: null` when a run does not read, rather than leaving the last good
reading looking current.

The first green run read what one login had been holding: **25 tables, 16
functions, 5 views, 10 policies, RLS enabled on 25 of 25, and `rig_views`
present** — the question that started it, answered. The store held the whole
economy, and it holds it in git now, re-read every six hours at :52.

### What the runs cost

Five failures before the green, and three of them were assertions made without
reading: a pooler host guessed as `aws-0` (it is `aws-1`); a diagnosis blaming
Ubuntu's package archive when the log on the table said `pgdg`; a `-t` pin
committed to fix a cause that did not exist. The captain then ordered probes,
and three readings — the `.deb`'s contents, `pg_wrapper`'s source, the
wrapper's newest-version rule — overturned the story entirely: the wrapper had
never run, something ahead of `/usr/bin` answered first, **and the cause of
that precedence was never established.** The fix stopped depending on knowing
it: the script resolves the newest `pg_dump` from disk and trusts PATH for
nothing.

Later the drift signal itself was audited and found to be noise: `pg_dump` 17
stamps every dump with a random `\restrict` guard token — same length every
run, different bytes — so five commits in one day each recorded a "change" that
was two lines of randomness. And the commit gate watched the whole `db/`
folder, whose register carries a timestamp, so it would have committed forever
regardless. Both fixed; the second cause would have survived a fix to the
first.

**And the credential was cut to size.** The dump connects as `amenti_reader`
now — `pg_read_all_data`, login, nothing else. A permanent unattended
credential should be able to do only what it does. The same ruling retired
token expiry on the index token: **an expiring credential in an unattended
workflow is a scheduled outage agreed to in advance**, and the failure it
invites — an instrument going quiet with nothing saying why — is the one this
project has actually suffered, repeatedly.

---

## II · The source index becomes an instrument

Every register on the ship had an instrument — plates.js, keyring.js,
probe-panes — except one. `SOURCES.json` was maintained by hand, in a project
whose law is that registers are never edited by hand, and its own traps block
said *a register read from this file is a memory; fetch it.* Nothing wrote it:
`tools/sources.js` 404, `probe-sources` 404, `BRIEFS.txt` — asked for by the
13 July handoff — 404. So it went stale the way hand-made things do. On 23
August it still pointed the prologue at `book/00-the-beach.md`, which had
become `preamble-02-the-beach.md`. Sixty-three of sixty-four paths were right.
The sixty-fourth was a 404 nothing could see.

**The fix is the Glass Gate's own shape applied to the index.** Structure
GENERATED — a repo walk. Semantics AUTHORED — `SOURCES.semantics.json`, the
meaning no walk can know. Live state PROBED — every path fetched and judged by
raw HTTP status. Merged with a drift report naming both directions:
`unreachable` (indexed, gone) and `unindexed` (present, undescribed — *not an
error; a document waiting for a sentence*).

§4 is enforced, not noted: the unauthenticated API returned its rate-limit
error object during testing, and the tool **refuses** rather than writing a
register from one. An absence from a source that was never asked is not an
absence.

### What the walk dragged back unbidden

The first full walk found **43 files nobody had ever described**, and the root
walk — added after `GLOSSARY.md` landed somewhere no walk looked — found
fourteen more. Among them:

- **Six briefs** the index never had, including THE ARK, THE SALVAGE, THE
  WATER BETWEEN and THE INSTRUMENT IS NOT EXEMPT — read and given sentences.
- **The whole written book** — five chapters, none indexed, including the
  moved prologue: both halves of the one standing 404 now visible in one
  register.
- **`MANUEL.md`** — a glossary of Page 2 that already existed, unfindable,
  three hours after this session concluded no glossary existed anywhere. The
  index's argument, made against its own author.
- **`HANDOFF.md`** — *not* the 13 July handoff the recovered-eight sort rules
  on. Two documents, one filename, distinguished now in writing.
- **`TODO.md`** — verified stale: its first item (Hume's three texts 404) is
  fixed and the list still says otherwise. A TODO nothing checks is a memory.
- **Twenty-six numbered probes and five tools**, of which more below.
- **The firing log**, `fleet-dispatch.json`, which nobody had indexed and
  which was carrying news: **THE WEEK fired 0** — the bell the 13 July handoff
  diagnosed, still unrung six weeks later; **ATLANTICA silent 18 days** after
  64 firings; **THE DAILY PLANET green on a last-fired date 76 days in the
  future** — a negative age passing a threshold test, a green lamp with a
  broken sensor.

The index closed at **121 authored entries, 120 reachable, 0 unindexed** across
six repositories, regenerated at :22. The one 404 is kept deliberately — a
tombstone recording that the prologue moved.

### The instruments, read

The named five (engine, gate, ordnance, production, voice) are live. **The
twenty-one numbered probes are stranded** — moved into `probes/` still
requiring `./amenti-chat.js`, which sits at the root; a one-character fix and
an unread pile of consequences. **Three can never run anywhere**: they read
`/mnt/user-data/uploads/`, an AI session's ephemeral folder, committed with
the sandbox's paths intact. **`probe5` existed and was removed unrecorded** —
probe11 names it. And **probe3 carries an assertion that cannot fail**: it
reads the same file into `orig` and `mine` and compares them — the guard on
the cache-key invariant, green for free, the Silent Signature wearing a
probe's coat. Recorded, not chased.

### The cache, and the instrument not being exempt

Three consecutive times this session, an upload was reported not to have
landed when it had landed every time. The reader was at fault:
`raw.githubusercontent.com` serves through a CDN that returns stale bytes with
a 200 for minutes after a commit. The verify fetches in `tools/sources.js` are
cache-busted now, with the incident in the comment — because a future session
would otherwise remove the buster as clutter.

---

## III · The vocabulary

Forty-odd briefs use *soul, key, plate, spell, register, probe, rung, ark,
empty glass, the Silent Signature, the water between, drift, stranded,
unindexed* — and not one defined them. **`GLOSSARY.md`** now does, in ten
sections, every count read at the hour of writing and marked as illustrative.
It separates the word *spell*'s two senses — the Book of the Dead's ~190
utterances, and this system's 21 drafted rules — which the corpus had been
using interchangeably. Three entries are flagged as inferred from usage and
await the proprietor's eye.

---

## IV · The hall

The captain's proposition, stated while stepping out the door: the primary
sources and the registers exist — *something should read the ship and give
back a correct answer and cite the briefs, instead of making users read
through them.* A chat-and-search surface, addressed not to a soul but to the
building. **Ask Amenti.**

Specified twice. Revision A treated it as an addition; the captain ruled it a
first-impression surface and one reading killed the retrieval layer entirely:
**the whole catalogue — every document with its description — is ~3,400
tokens.** It fits in the prompt. A retrieval pass can miss the right brief and
never say so; the whole catalogue cannot miss. Faster and more honest at once.

The architecture, ruled and built:

- **An answer is composed, never pre-loaded.** A pre-loaded answer is a memory
  — correct the day it is written, silently wrong after. Meaning comes from
  **`HALL.md`**, authored, holding *no numbers*; every count comes from
  **`HALL-STATE.json`**, ~600 bytes written by `probe-hall.mjs` from the
  registers, null when a register cannot be read. The hall answers *what is
  Amenti* at the hour of asking: the myth from the authored file, *a thousand
  and eleven souls* from the read.
- **One engine, second voice.** It calls `window.claude.complete` — the one
  door — with a different system prompt. Not a second chat engine. Every
  duplicated path in this system has cost a night somewhere.
- **Answer, then point.** Cite widely from the catalogue, quote narrowly —
  at most two briefs fetched per question. The briefs are the evidence;
  the hall is the doorway.
- **Search never spends.** Names and fragments are answered locally and
  instantly; only a genuine question, on Enter, reaches the model. The
  bombardment the captain enumerated — *who are you, are you hungry, is this
  legal, who made this, who am I* — is handled in `HALL.md`'s own voice:
  provenance, small talk, and the standing redirect. *The souls are the
  destination; I am only the door.*
- **Text only, stateless.** The captain's ruling: no voice, no mic, no
  conversation memory. A visitor who wants a conversation has eleven hundred
  souls for that.

**And the search found its own hole.** `find('caesar')` against the document
catalogue returned zero — a search over the documents is not a search over the
library. `probe-roster.mjs` now writes `ROSTER-INDEX.json`: 1,011 souls, 57 KB,
for the browser and never for the model. In building it, an off-by-one exposed
that **Albert Einstein answers to two keys** — exact and reversed — 53 keys
reaching 52 souls; an assignment that overwrote became a collection.

### Where it lives

The first plan put the box on Page1. **The captain refused it**, and was
right: a month of stabilisation does not end with a DOM injection into the
flagship. And the hall could not live in a separate repo either — the hall
answering questions about Amenti from outside Amenti is the water-between
fault with a lobby. The ruling: **`hall.html`, in the ship, its own door.**
It carries its own thirty-line proxy client — duplicated deliberately, marked
as such — so the flagship loads nothing new. Page1's entire change is one
anchor: `ASK AMENTI`, second in the nav, after ARENA.

Tested end to end with the model stubbed before anything shipped: a name
spends nothing; a question assembles HALL.md + the counts + the catalogue at
~6,100 tokens; a 429 is a sentence, not a broken box; a missing register is
named in the answer. The question log is a local tally (`amenti.hall.log`) —
a fleet-wide question register needs a Worker tube and is recorded as open,
not smuggled in. After a week, the four seeded questions should be replaced by
the four real ones.

---

## V · THE RUNGS, AS OF THIS NIGHT

| rung | instrument | writes |
|---|---|---|
| :07–:47 | the five strands | their registers |
| :22 | the source index | `SOURCES.json` |
| :42 | the hall | `ROSTER-INDEX.json`, `HALL-STATE.json` |
| :52 | the third tier | `db/schema.sql`, `db/SCHEMA.json` |

Two must never occupy one rung.

---

## VI · OPEN, RECORDED, NOT CHASED

In the order it will hurt:

1. **THE WEEK has never fired.** Diagnosed 13 July, rediscovered tonight in a
   register nobody had indexed. Probably still a three-line crons block.
2. **ATLANTICA dark since 6 August**, after 64 firings. Something stopped.
3. **THE DAILY PLANET is green on a future date.** The probe's age test passes
   a negative. Fix the sensor, then find the bad key.
4. **Twenty-one probes stranded** by the move into `probes/`; three more can
   never run; probe3's tautology; probe5's unrecorded removal. One session,
   with output read as it comes.
5. **One spell is CONTRADICTED** in the conformance register.
6. **`TODO.md` is stale** and says so nowhere on its face.
7. **The 27 undeclared files** in the fleet manifest await role lines — the
   captain's to name.
8. **The hall's first answer has not yet been judged by a human ear.**
9. **The schema drift signal** wants one more clean scheduled run observed
   before it is trusted.

---

## VII · THE LESSON, IF ONE NIGHT HAS ONE

The session's failures were all one failure. The pooler host was guessed. The
apt diagnosis contradicted the log it cited. The stale CDN was read as a
missing upload, three times. The conformance field was guessed and counted
zero. Each time, the correction was the same correction:

> **LOOK FIRST. The reading is cheaper than the guess,
> and the guess costs a run either way.**

And the night's work was all one work. The registers, the index, the glossary,
the counts — every instrument built this month points inward, so the builders
can see the building. Tonight they were turned outward for the first time:

> The registers were built so the ship could be read.
> **The hall is the ship, reading itself aloud.**

*The hall is a doorway; the souls are the destination.*
