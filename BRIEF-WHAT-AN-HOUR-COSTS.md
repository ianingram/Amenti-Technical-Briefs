# BRIEF — WHAT AN HOUR COSTS
### Ingram Manor LLC · 27 August 2026 · a reading, not an estimate

Every cost figure in this project has been a guess. This one is not: the prompt
was BUILT and MEASURED, not counted by eye, and every number below comes from
running `defaultBuildSystem` and `leanBuildSystem` against a real figure.

**One hour of conversation, one person, text only: between $0.66 and $2.48.**
The spread is the whole brief.

---

## 1 · THE READING

Measured 27 Aug against Abraham Lincoln — a figure with a title, an era, a
voice line and an 880-character biography — in character mode, with three facts
remembered.

| | chars | ~tokens |
|---|---|---|
| **the full prompt** | 8,246 | **2,291** |
| the lean prompt | 4,064 | 1,129 |
| the full prompt with NO memory | 7,406 | 2,057 |
| counsel mode | 8,378 | 2,327 |
| *the memory block alone* | *840* | *234* |

Tokens are chars ÷ 3.6, the usual ratio for English prose with markup. Prices
are Sonnet 4.6 list: **$3 per million in, $15 per million out.**

### The shape of a turn

```
  system prompt      2,291 tokens     SENT ON EVERY TURN
  bounded history    1,750 tokens     ANCHOR 4 + WINDOW 10 = 14 messages
  ─────────────────────────────
  input              4,041 tokens
  output               111 tokens
                     $0.0138 per turn
```

**Fifty-seven per cent of the input is the system prompt, and it is re-sent
every single turn.** That is the finding. The conversation is the cheaper half
of the conversation.

### The window is why this is bounded at all

`ANCHOR: 4, WINDOW: 10` — fourteen messages, never more, however long the talk
runs. **A three-hour conversation costs the same per turn as the first one.**
Without that bound the payload grows with every exchange and an hour becomes
unpriceable. It is the single most important cost decision already in the code,
and it was made before anyone was counting.

---

## 2 · THE HOUR

| | per turn | 90 turns (typing) | 180 turns (spoken) |
|---|---|---|---|
| **full prompt, window 14 — TODAY** | $0.0138 | **$1.24** | **$2.48** |
| full prompt, window 10 | $0.0123 | $1.11 | $2.21 |
| full prompt, window 6 | $0.0108 | $0.97 | $1.94 |
| lean prompt, window 14 | $0.0103 | $0.93 | $1.85 |
| lean prompt, window 6 | $0.0073 | $0.66 | $1.31 |
| *full prompt, window 14, on Haiku* | *$0.0037* | *$0.33* | *$0.66* |
| *lean prompt, window 6, on Haiku* | *$0.0019* | *$0.18* | *$0.35* |

Ninety turns is an hour of typing at roughly one exchange every forty seconds.
A hundred and eighty is an hour of talking.

---

## 3 · WHAT IS NOT IN THOSE NUMBERS

**VOICE.** Gemini TTS is billed separately and is the other half of the bill for
any spoken conversation. It is not modelled here because `/speak` is
**content-hash cached in R2** — a line anyone has ever heard is free forever
after — so the marginal cost depends entirely on how much of a conversation is
novel prose, which nothing currently measures. **First conversations pay;
repeats do not.**

Worth measuring separately. It is the only remaining unpriced surface.

**THE MEMORY WRITER**, on the other hand, is priced and is a rounding error:

```
  ~3,889 in + 33 out   =   $0.0122   once, per figure left
```

Under one cent, or about **two turns' worth of chat, per conversation.** It fires
only on leaving a figure, only when a signed-in reader has spoken at least four
turns, and it speaks through the same proxy as everything else so its spend
already lands in `window.AmentiCost`.

**And the memory it reads back costs 234 tokens a turn** — the block in §1.
About 6% of the input, or **thirteen cents on a 180-turn hour**. That is the whole
running cost of a figure remembering somebody.

---

## 4 · THE LEVERS, HONESTLY

### The lean prompt — a 51% smaller prompt, a 25% smaller bill

The arithmetic is not intuitive and is worth stating plainly, because it is easy
to overclaim (and was overclaimed in conversation before it was measured):
**halving the prompt does not halve the bill**, because the prompt is only 57%
of the input. 8,246 chars → 4,064 saves 1,162 tokens of 4,041.

```
  $0.0138  →  $0.0103      $1.24/hr  →  $0.93/hr
```

**AND IT IS NOT FREE MONEY.** `leanBuildSystem` keeps the persona, the voice,
the biography, the recollection and the hall. What it drops is precisely the
material that makes a figure a companion rather than a kiosk: *go with them when
they wander, take your turn, read the person and not the words, treat distress as
the human.* Five sections of CONVERSATION_DOCTRINE.md live in the part that gets
cut.

**The lean prompt is cheaper because it is a thinner character.** Thirty cents an
hour is the price of the doctrine, and that is a product decision, not an
optimisation.

### The window — cheaper, and it costs memory instead of character

Dropping WINDOW from 10 to 6 saves more than swapping the prompt does, and costs
something different: the figure holds less of the immediate conversation. It will
lose the thread of what was said four exchanges ago.

For a rambling, drifting conversation — which the doctrine explicitly invites —
that is a real loss. **Whether it is a worse loss than the lean prompt's is a
judgement nobody has made yet, and it should be made by listening rather than by
arithmetic.**

### The model — the only lever that is nearly free

Haiku 4.5 is roughly a quarter the input price and a quarter the output price
— 3.7× cheaper per turn once the output ratio is folded in.
**Full prompt, full window, on Haiku: $0.33 an hour.** A quarter of today's bill
with no doctrine removed, no window shortened, and no character thinned.

It is already in the proxy's `ALLOWED_MODELS` and already selectable through
`window.AmentiModel`. What is unknown is whether a Haiku Lincoln is a Lincoln
worth talking to — and that is a listening question, not a pricing one.

**RECOMMENDED FIRST EXPERIMENT: the same conversation, twice, on both models,
read side by side.** It costs about a dollar to find out and it is the only lever
here that does not trade character for money.

---

## 5 · THE BREAKER, AND WHAT IT IMPLIES

The proxy's wall stands at:

```
  DAILY_TOKENS: 2,000,000     across everything, every day
```

At 4,041 tokens a turn that is about **495 turns a day** before the hall goes
quiet and every visitor gets *the hall has answered a great many questions this
hour.*

**That is three to five real conversations.** Not three to five hundred.

The breaker was sized as scar tissue from a $118 overrun, at a time when nobody
had measured a turn. It is doing exactly what it was built to do; it simply
implies a much smaller day than it looks like it does. **Anyone reading
"two million tokens" as generous should read it as five conversations.**

Nothing here argues for raising it. The standing order on the wall is explicit —
*if a surface 413s here, CHUNK THE SURFACE, do not raise this* — and that order
was written after real money was lost. But the number should be understood
before it fires on a good day rather than after.

---

## 6 · WHAT WOULD ACTUALLY MOVE THE BILL

In order of return, and none of them is a prompt tweak:

1. **Model choice.** 3.7× on Haiku, nothing else changed. Costs only a
   listening test.
2. **Prompt caching.** The system prompt is 2,291 tokens, IDENTICAL on every
   turn of a conversation, and re-sent every time. Anthropic bills cached input
   at a fraction of the normal rate. This is the largest single saving available
   and it removes nothing — same prompt, same character, same window. **NOT
   INVESTIGATED. It is the first thing to look at.**
3. **The window**, at the cost of conversational memory.
4. **The lean prompt**, at the cost of the doctrine.

The first two take nothing away. The last two both buy money with character.

---

## 7 · WHAT IS STILL UNMEASURED

- **Voice.** The other half of a spoken hour, and the only unpriced surface left.
- **Prompt caching.** §6 item 2 — potentially the largest saving in the system
  and nobody has looked.
- **A real conversation.** Every figure here is modelled: 450 chars a message,
  400 a reply, 90 or 180 turns an hour. `window.AmentiCost` records the TRUTH,
  turn by turn, and has since the usage field stopped being discarded.
  **One real hour read out of `AmentiCost` beats this entire brief**, and it
  costs a dollar to obtain.

---

*Measured 27 August 2026 by building the prompts and counting them. Prices are
Sonnet 4.6 and Haiku 4.5 list rates at the date of writing and will drift. The
method is in the brief so it can be re-run rather than believed.*
