# AMENTI — BUILD ORDER: THE OUTWARD PROBE
**Ingram Manor LLC · 24 August 2026 · a build document, not an account**

## HOW TO USE THIS

This sequences the work that turns ASK AMENTI into the ship's first outward
probe — the hall's doorway, sent ahead into other people's walls, taking the
one reading no inward instrument can take: *what does the world ask,
unprompted?*

It is a build order in the manner of the emerald build order: phases, each
shipping something that works alone, each verified before the next begins.
**The preamble is reserved.** The closing conversation of the Stage 2 session
— the throttle recognised before the section was found, the lanes ruled, the
outward probe named — precedes this document in the eventual brief, THE TWO
THROTTLES, written from the shop floor when the work is done. This document is
the plan; that brief will be the evidence.

Two standing rulings govern everything below:

> **ONE ENGINE. SEPARATE LANES. SEPARATE BUDGETS.**
> Engines are for capability; lanes are for blast radius.

> **NO AD RUNS BEFORE THE GATE CAN SAY NO.**
> An outward probe you cannot recall is not a probe. It is the hull.

---

## PHASE 0 · READ THE GATE AS IT IS

**Nothing in this document contains a reading of `amenti-proxy`'s code.**
Every estimate below can move once someone looks. First step of the first
session, before any design hardens:

1. Fetch the Worker's source from `Amenti-Workers` (private — the captain
   holds the passage).
2. Read: how it parses a request, what it forwards, what it returns, whether
   any origin/limit/logging logic already exists, and where a lane check would
   sit.
3. Read `wrangler.toml`: bindings, KV namespaces, routes. If no KV namespace
   exists for counting, one dashboard visit creates it — do this early, it is
   the tonight's-secrets-dance of this build.
4. Write the reading down before changing anything. The build brief's first
   section is this reading.

**Exit test:** a paragraph in the working notes describing the Worker's
current request path, verified against the source, not remembered.

---

## PHASE A · THE GATE LEARNS TO SAY NO

The lanes. One session, on the one Worker.

### A1 · The lane declaration
Every caller declares its lane in the request body — `lane: "ship"`,
`lane: "hall"`, `lane: "embed"`. A request with no lane is the ship lane
(everything deployed today keeps working unchanged). An unknown lane is
refused.

### A2 · The lane table
One structure at the top of the Worker — the lanes, their budgets, their
limits. Something with the shape:

    ship    no per-IP limit today; daily ceiling generous
    hall    per-IP per-minute limit; hourly and daily ceilings
    embed   tightest per-IP limit; modest daily ceiling; origin-checked

Numbers are the captain's to set and one line to change. The structure is the
deliverable; the values are policy.

### A3 · The counting
Per-IP and per-lane counters in KV (or Cloudflare's rate-limit binding if the
Phase 0 reading shows it available). Windowed, cheap, and **failing open is
forbidden**: if the counter store cannot be read, the gate refuses the
discretionary lanes and says why. A limit that cannot count is not a limit.

### A4 · Origin
An allow-list per lane. The ship lane accepts the ship's own origins. The
embed lane accepts the origins the captain has approved for placements —
added one line at a time, as deals are made.

### A5 · Every refusal is a sentence
No bare 429s, no empty bodies. Each refusal returns a short reply the surface
can show verbatim — the hall already renders one: *the hall must catch its
breath.* Rate-limited, over-budget, wrong-origin, unknown-lane: four
sentences, written once, in the hall's voice.

### A6 · The kill switch
One value per lane — `open: true/false`. A lane set false refuses everything
with its sentence, instantly, without deploy. **This is the probe's recall
line.** Test it before anything else ships: flip the hall lane off, watch the
box degrade to search-only with the sentence showing, flip it back.

**Exit tests for Phase A:**
- The ship lane behaves byte-identically to today for existing surfaces.
- The hall lane refuses the N+1th request in a window with its sentence.
- The embed lane refuses a disallowed origin.
- The kill switch works from the dashboard with no deploy.
- `db`-style failure honesty: counter store unreachable → discretionary lanes
  refuse, ship lane's behaviour is the captain's ruling to make in Phase 0.

---

## PHASE B · THE PROBE LEARNS TO REPORT

The question log — deferred from Stage 2 because the browser may not write.
The Worker writes; that law holds.

### B1 · The log tube
On every hall/embed request the gate appends one record to KV:
lane, question (truncated), timestamp, origin, answered/refused, and which
refusal. No IP addresses stored — the counting uses them transiently; the log
does not keep them. What strangers type is market research; who they are is
not the ship's business.

### B2 · The register
`probe-ordnance` gains a sibling or a section: read the log tube, write
`HALL-QUESTIONS.json` — counts by lane, the top questions verbatim, refusal
rates, per-day volume. **A register, not a dashboard.** The ship's own
instruments read it; the captain reads it; after a week, the four seeded
questions on the box are replaced by the four real ones.

### B3 · Cost truth
The gate already returns `usage`; the log keeps per-lane token totals so the
register can state what each lane actually costs. *Measured, not modelled* —
the same correction Page1's client already made for the ship.

**Exit tests for Phase B:**
- Ask the hall three questions; find all three in the register with the right
  lane, none carrying an IP.
- Refuse one deliberately; find the refusal counted.
- Token totals in the register match `window.AmentiCost` for the same turns.

---

## PHASE C · THE EMBED — THE PROBE ITSELF

The projection of the hall that stands in a stranger's wall.

### C1 · `embed.html`
A slimmed hall: the box, the roster search, the document search — **the ask
path disabled or lane-limited per the captain's ruling below.** Footer:
*enter the hall to ask* → `hall.html`. Self-contained like its parent,
declaring `lane: "embed"` in anything it sends.

### C2 · The open ruling, for the captain
Two shapes, decided per placement, not globally:

- **The ad invites** — search only, zero cost per impression, every click a
  funnel to the ship. Ships the day Phase A lands.
- **The ad answers** — the ask path live on the embed lane's tight budget.
  More powerful, costs per interaction, and only sane because A6 exists.

The build supports both; the ruling is which placements get which.

### C3 · Sizing for other people's walls
Iframe-clean: no assumptions about viewport, dark/light from the host if
possible, nothing that escapes the frame. One test page that iframes it at
three sizes.

### C4 · Where it lives
`Amenti.live`, beside `hall.html` — the projection stays with the ship, per
the standing ruling (*why separate the hall from itself*). If marketing
iteration later demands its own churn rhythm, a satellite repo holds a **copy
built for that purpose**, and the hall itself never moves.

**Exit tests for Phase C:**
- The embed iframed on a foreign test page searches instantly and spends
  nothing.
- With the ask path enabled, it answers on the embed lane and is refused when
  that lane's budget is spent — with the sentence visible inside the iframe.
- The kill switch silences it from the dashboard while `hall.html` continues
  answering.

---

## PHASE D · THE INSTRUMENT IS NOT EXEMPT

The gate is new code on the money path. It gets a probe before it gets
traffic.

### D1 · `probe-lanes.mjs`
Knocks on each lane and reads the limits back: sends a compliant request per
lane (expects an answer or a clean lane-refusal), sends a deliberately
over-limit burst at the hall lane (expects the sentence), sends a
wrong-origin request at the embed lane (expects refusal). Writes
`LANES.json`: each lane, its observed behaviour, its configured state.

> **A LIMIT NOBODY HAS TESTED IS A PRAYER.**

### D2 · A rung
`:32` is free. The probe runs there; two must never occupy one rung.

### D3 · The brief
**THE TWO THROTTLES**, written from the shop floor after D1 is green: the
preamble reserved from the Stage 2 closing conversation, Phase 0's reading,
the build with its failed runs (there will be some; they always earn their
table), and the lineage — the voice throttle metering what the ship says, the
gate metering what the crowd asks, one engine with a throttle at each end.

---

## ORDER OF WORK, FLAT

1. Phase 0 — read the Worker. Nothing before this.
2. A1–A6 — the lanes, kill switch tested first among the exit tests.
3. D1 first draft — even rough, before traffic; the gate is not exempt.
4. B1–B3 — the log tube and the register.
5. C1, C3 — the embed, search-only.
6. C2 — the captain rules invite-vs-answer per placement.
7. First placement. The probe goes out. The register fills.
8. D2, D3 — the rung, and the brief.

## WHAT TO ASK THE CAPTAIN FOR

- **The passage to `Amenti-Workers`** for Phase 0. Not in a chat.
- **The lane numbers** — per-IP rates and daily ceilings for hall and embed.
  Proposals will be offered from the Phase 0 reading; the ruling is the
  captain's.
- **The Phase 0 ruling on counter-store failure** for the ship lane: refuse
  like the others, or stay open for the ship's own surfaces.
- **The first placement**, when C is green — where the probe first stands.
- Nothing else. No deploys until Phase 0 is read and written.

---

*The hall is a doorway. The gate decides who may keep asking.
The probe is the doorway sent ahead — launched with the line that recalls it.*
