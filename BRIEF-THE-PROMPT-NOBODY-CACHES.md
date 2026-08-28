# BRIEF — THE PROMPT NOBODY CACHES
### Ingram Manor LLC · 27 August 2026 · the one lever that takes nothing away

The system prompt is **2,244 tokens**, byte-identical on every turn of a
conversation, and **re-sent in full every single time**.

BRIEF-WHAT-AN-HOUR-COSTS measured it and named this as the largest saving
available. Nobody has looked. This is the look.

**Caching as the prompt stands today saves 22%. Reordering the prompt first
takes it to 33%.** Neither removes a single word the figure says.

---

## 1 · WHY IT IS THE ONLY FREE LEVER

Every other way to cut the bill buys money with character:

| lever | saves | costs |
|---|---|---|
| the lean prompt | 25% | the conversation doctrine — drift, turn-taking, distress |
| window 14 → 6 | 22% | the figure's memory of the conversation it is in |
| Haiku instead of Sonnet | 73% | unknown — whether a Haiku Lincoln is worth talking to |
| **prompt caching** | **22–33%** | **nothing. Same prompt, same window, same figure.** |

Caching is not a smaller prompt. It is **the same prompt, not paid for twice.**

---

## 2 · THE MEASUREMENT

Anthropic prices a cache **write** at 1.25× input and a **read** at 0.1×.
Against the measured prompt:

```
  today, no cache        $0.0138 per turn
  turn 1, writing        $0.0155   +12%
  every turn after       $0.0076   −45%
```

**Break-even is turn two.** There is no visit long enough to matter and short
enough to lose.

| a visit of | uncached | cached | saves |
|---|---|---|---|
| 2 turns | $0.028 | $0.023 | 16% |
| 5 turns | $0.069 | $0.046 | 33% |
| 10 turns | $0.138 | $0.084 | 39% |
| 90 turns | $1.241 | $0.692 | 44% |

Those are the ceiling figures, for a prompt that is cacheable end to end. **Ours
is not, and that is §3.**

---

## 3 · THE PROMPT DIVERGES IN THE MIDDLE

Built twice for the same figure and two different readers, then compared:

```
  full prompt              8,078 chars   2,244 tokens
  identical across readers 4,546 chars   1,263 tokens   ← 56%
  diverges after           3,532 chars     981 tokens
```

**It diverges at `nameGuidance`** — the moment the reader's name appears:

> *You already know their name: **Roger**. Hold it in reserve…*
> *You already know their name: **Mary**. Hold it in reserve…*

And everything AFTER that point is shared again — the recollection block's
instructions, the threshold, the hall, the summoned line. **The per-reader
material sits in the middle, and a shared tail is stranded behind it.**

A cache prefix has to be a prefix. One personal line at character 4,546 costs
the 3,532 characters that follow it, most of which are the same for everybody.

---

## 4 · THE REORDER

Move the two per-reader blocks to the END of the system prompt:

- the known-name line from `nameGuidance()` — ~310 chars
- the recollection block from `recollectionGuidance()` — ~862 chars

Everything else is identical for every reader talking to that figure.

```
  cacheable prefix   1,263 tokens  →  1,918 tokens
                          56%      →       85%
```

| | ten-turn visit | per user / month |
|---|---|---|
| today | $0.1365 | $0.68 |
| cache as-is | $0.1067 | $0.53 |
| **cache after reorder** | **$0.0913** | **$0.46** |

### And the prose does not suffer

The recollection block already reads as a closing instruction — *you know these
things; you are not reciting them* — and sits naturally at the end. The name
line is one sentence. **Nothing about the figure's character depends on where in
the prompt these appear**, only that they appear.

That is worth stating because it is the reason this is safe: the reorder is a
change of ORDER, not of content, and the content is what the doctrine governs.

---

## 5 · THE CACHE IS PER-FIGURE, NOT PER-CONVERSATION

The most valuable thing in this brief, and the least obvious.

Once the personal lines are at the tail, the cached prefix contains **only the
figure**: persona, biography, voice, the conversation doctrine, the spell, the
hall. That prefix is identical for *every reader talking to that figure*.

**A hundred people talking to Lincoln in the same five minutes share one cached
prompt.** The saving is not bounded by how long one person talks; it compounds
with concurrency, which is the direction the business is trying to go.

---

## 6 · WHAT IT COSTS, HONESTLY

### The five-minute TTL

Anthropic holds a cache entry for five minutes, refreshed on each hit.

- a reader replying within five minutes: **hit**
- a figure nobody has spoken to in five minutes: **the next turn pays the write**

So the saving depends on CONCURRENCY, and at Amenti's current traffic **most
first turns will be writes.** The 33% figure is the busy case. A quiet site
saves less — though never less than nothing, because break-even is turn two.

**This is the number the visit reading will settle**, and it is another reason
that instrument was worth building before this one.

### The write premium

1.25× on the cached block, once. A site of single-turn visits would lose
marginally. Amenti's are not.

### It is a PROXY change, not a client change

`window.claude.complete` posts `system` as a plain string, and the proxy
forwards it as a plain string:

```js
body: JSON.stringify({ model, max_tokens: MAX_TOKENS, system, messages })
```

Caching requires the system block sent as an ARRAY with a `cache_control`
marker on the part to be cached. So the proxy has to split the prompt — and it
cannot split what it cannot see the seam of.

**Which means the client and the proxy must agree on a seam**, and that is the
one piece of real design here. Two options:

1. **The client sends two fields** — `system` (cacheable) and `systemTail`
   (per-reader) — and the proxy assembles them. Explicit, and the seam is where
   the client says it is.
2. **The proxy splits on a marker string** the client embeds. Fewer moving
   parts, more magic, and a marker that drifts silently breaks caching without
   breaking anything visible.

**The first is right.** A silent cache miss is exactly the class of fault this
yard keeps finding: nothing looks broken, the bill is simply higher than it
should be, and no probe would say so.

---

## 7 · AND IT MUST BE MEASURABLE

A saving nobody can read is a claim.

Anthropic returns `cache_creation_input_tokens` and `cache_read_input_tokens`
in `usage` on every call. **The proxy already reads `usage` and already meters
it** — `meterUsage()` records input and output and discards the rest.

So the instrument is nearly free: record the two cache fields alongside the
others, and a hit rate becomes readable rather than assumed. Without it, the
first question after shipping — *is it actually caching?* — has no answer.

**This is the same fault the cost brief opened with**: every cost figure in this
project was a guess while the true number sat in the response body being thrown
away.

---

## 8 · THE ORDER OF WORK

1. **Reorder the prompt.** Client-side, in `amenti-chat.js`. Changes nothing
   about behaviour; makes 85% of the prompt cacheable instead of 56%.
2. **Split the seam.** `defaultBuildSystem` returns two strings instead of one;
   `window.claude.complete` sends both.
3. **The proxy assembles them** with `cache_control` on the first.
4. **Meter the cache fields**, so the hit rate is a reading.
5. **Read it after a week**, against the visit reading, and find out whether the
   busy case or the quiet case is the real one.

Steps 1 and 2 touch `amenti-chat.js`, which is the most sensitive file in the
repo. **Diff before deploying.**

---

## 9 · WHAT IS NOT KNOWN

- **The real hit rate.** It depends entirely on concurrency per figure, which
  nothing has measured. The visit reading is the instrument; it has no data yet.
- **Whether the counsel and lean prompts have the same seam.** They were not
  measured for this brief. `leanBuildSystem` is a different assembly and may
  diverge in a different place.
- **Whether Gemini's TTS has an equivalent.** The voice half of the bill is
  still entirely unpriced, and this brief does not touch it.

---

*Measured 27 August 2026 by building the same prompt for different readers and
comparing the strings. Cache pricing is Anthropic's published 1.25× write and
0.1× read; token prices are Sonnet 4.6 list and will drift. The method is here
so it can be re-run rather than believed.*
