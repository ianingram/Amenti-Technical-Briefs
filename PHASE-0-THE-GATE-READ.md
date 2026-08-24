# PHASE 0 · THE GATE, READ
**Ingram Manor LLC · 24 August 2026 · the reading before the build**

Read from the deployed `amenti-proxy` source (2,823 lines), brought out of the
private `Amenti-Workers` by the captain. This is the reading the build order's
Phase 0 required. **Nothing below is designed — it is what the code says.**

---

## WHAT THE 413 WAS

Not the model's limit, not a token limit. A hard **character** cap the proxy
enforces on itself:

```
SYSTEM_CHARS: 20000     // line 156
if (system.length > LIMITS.SYSTEM_CHARS) return wall("system_too_long", 413)
```

The hall's original prompt — HALL.md + counts + catalogue + two 6 KB brief
slices — was ~24,000 characters. It overran the wall. The trimmed prompt
(slices removed) is ~17,800 characters and clears it.

**And the wall carries an order, in the captain's hand, three lines up:**

> *If a surface 413s here, CHUNK THAT SURFACE. Do not raise this.*

The hall fix obeyed it exactly: it chunked the surface — cite, don't quote —
rather than raising the wall. The comment in `amenti-hall.js` should say so, so
no future session raises `SYSTEM_CHARS` and reopens what these limits closed.

## WHY THESE LIMITS EXIST — THE $118 HOLE

The `LIMITS` block is scar tissue, and the code says from what:

> *max_tokens already bounds the OUTPUT at 1024. Nothing bounded the INPUT —
> the expensive half of a long conversation, and the whole shape of the $118
> hole.*

The proxy was hardened after a real \$118 overrun. **The lanes ruling must not
be read as loosening this.** It adds a per-surface dimension to limits that are
already load-bearing; it does not raise them.

---

## WHAT IS ALREADY BUILT

This is not a bare proxy. The gate the build order imagined is **half-present**:

| Mechanism | Where | State |
|---|---|---|
| **Per-field hard caps** | `LIMITS`, lines 142–162 | speak 1500, style 600, system 20000, chat 60 msgs / 80000 chars |
| **Refusals as sentences** | `wall()`, `denyRate()`, `denyBreaker()` | every 413/429 returns a named error and a detail line |
| **Per-IP rate limit** | `rateLimited()`, line 256 | keyed `rate:${kind}:${ip}:${bucket}`, per 60s window, on KV |
| **Daily budget breaker** | `meter()` / `DAILY_TOKENS: 2000000` | a day's ceiling across everything |
| **Origin allow-list** | `corsHeaders()`, line 289 | `ALLOWED_ORIGINS` env var, comma-separated |
| **Usage metering** | `meterUsage()`, line 251 | reads `data.usage`, already returns it to clients |
| **KV, optional** | `watchGet/Put` | eventually-consistent; hard caps hold when no KV bound |

**The `kind` parameter is the seam the lanes attach to.** `rateLimited()`,
`meter()` and the caps already branch on `kind` (`"speak"` vs `"chat"`). A lane
is one more axis on the same key: `rate:${kind}:${lane}:${ip}:${bucket}`,
and a per-lane row in a budget table. **The lanes are not new machinery — they
are a dimension on machinery that is proven and already carrying the ship.**

---

## TWO HONESTIES THE CODE VOLUNTEERS

The proxy is candid about its own weak points, in comment. Both bear on the
outward probe:

1. **The origin check *can* fail open — but does not.** Line 121: *if
   `ALLOWED_ORIGINS` was never set, the allowlist falls through to `"*"` and
   EVERY origin is allowed while the code reports that it checked.* **VERIFIED
   24 Aug: it is set**, to five real origins — `amenti.live`, `www.amenti.live`,
   `ianingram.github.io` (where the hall serves), `amenti-ai.com`,
   `www.amenti-ai.com`. The Silent Signature the code warned of is not live.
   The consequence for the outward probe is decisive: **an embed on a
   stranger's wall is blocked by default** — a new placement's origin must be
   added deliberately. The opt-in-per-placement control the ad plan needs
   already exists and already works.

2. **The rate/budget layers ride on eventually-consistent KV.** Line 134: they
   can undercount briefly under a burst. The hard per-request caps do not — they
   hold regardless. So the *character* walls are firm; the *rate* walls are
   soft. An outward probe on a hostile surface leans on the rate walls, so this
   matters: the embed lane wants a tight hard cap, not only a rate limit.

---

## WHAT THIS CHANGES IN THE BUILD ORDER

- **Phase A shrinks.** Lanes are a `kind`/`lane` axis on existing caps, rate
  keys and budget — not a new gate. Origin allow-list already exists; it needs
  per-lane entries and, first, the fail-open closed.
- **The kill switch is nearly free.** A per-lane `open: false` is one check
  beside the caps already there.
- **The hall's ceiling question is answered.** It stays under 20000 by citing,
  not quoting. Restoring brief-quoting is not a proxy change — it is a
  *chunking* change: fetch and send one short slice, well under the cap, only
  when a question clearly needs it. That can be done today, within the wall.

---

## FOR THE NEXT STEP

1. ~~Confirm `ALLOWED_ORIGINS` is set.~~ **DONE 24 Aug** — set to five
   origins, verified in the dashboard. The origin check is real. Adding a
   placement's origin is how an embed is authorised; removing it is a per-
   placement kill switch that already exists.
2. **Read the router** — which paths (`/speak`, `/chat`, `/listen`) exist and
   where a `lane` field would be parsed. (Not yet read; the request-dispatch
   section is the remaining Phase 0 reading.)
3. Then design Phase A against the real seam, not the imagined one.

> **The wall said: chunk the surface, do not raise me. The hall obeyed.
> The gate was already standing; the lanes are its second dimension, not its
> foundation.**
