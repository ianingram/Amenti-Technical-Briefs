# BRIEF — THE FIGURE REMEMBERS
### Ingram Manor LLC · 26 August 2026 · a feature spec, nothing built

A signed-in reader talks to Lincoln. A week later they come back, and Lincoln
says *we talked about your aunt Jane last I recall — how is she?*

That is the whole feature. This brief says what it stores, what it refuses, and
which two questions are not yet answered.

**Nothing here is built.** Every decision below was taken deliberately in one
session and is written down so it is not rebuilt worse from memory. Where a
thing was ruled OUT, the ruling is recorded with it — a spec that lists only
what was chosen loses the argument that produced it.

---

## 1 · WHY

The hall is stateless by ruling: *each ask stands alone — a visitor who wants a
conversation has the souls for that.* The souls were always where memory could
live. Nothing had been decided about whether it does.

This is the feature that makes a reader come back. Not more figures, not better
answers — being remembered.

---

## 2 · WHAT IS STORED

**Facts, not transcripts.** Three or four short lines per reader per figure.

```
Has an aunt, Jane
Runs a horse farm
Named James
```

Not the conversation. Not what the figure said. Not what was asked.

**Why not a transcript.** Two reasons and either is sufficient. A transcript
does not fit — `SYSTEM_CHARS` is 20000 and the hall's own prompt already runs
18648. And a figure who quotes you verbatim is a database; one who remembers
your aunt's name and asks after her is a person. **The imperfection is the
feature.** *Last I recall* is doing real work: it gives the figure room to be
slightly wrong, which is more convincing than perfect retrieval.

**Capped, at roughly ten per pair.** Not for storage — storage is free at this
size. A figure reciting twenty things about you is unsettling.

**Overwritten, not accumulated.** New facts replace the ground they cover.
Lincoln has *lives in Denver*; the reader says Portland; Denver goes. This
loses the fact that they moved, which is arguably the more human thing to
remember. **Accepted knowingly for v1.** This is an experimental feature and
will be adjusted.

---

## 3 · WHO KEEPS IT, AND WHO NEVER SEES IT

**Keyed to the pair — reader AND figure.**

**NO CROSS-FIGURE LEAKAGE.** Caesar does not know what you told Lincoln. This
needs no mechanism: the lists simply never join. A reader who tests it finds
the world holds together, and that is worth more than the convenience of a
shared memory would ever be. The separation of powers, applied to the souls.

**NO CAPTAIN'S VIEW.** Ruled out explicitly. There is no pane, no register, no
export, and no administrative read of what a figure remembers about a person.
The memory belongs to the reader and the figure.

> The cost is accepted: the writer's brief in §5 cannot be tuned by reading
> what it stored about strangers. It is tuned on the captain's own
> conversations or on synthetic ones. Slower, and the right trade.

---

## 4 · WHERE IT LIVES

**Supabase.** Not close:

- It is the only tier that knows who a person **is** — auth, the list. Memory
  must key to a signed-in reader.
- RLS is on 25 of 25 tables. A policy saying a reader reaches only their own
  rows is the same shape as the ten already there.
- It is the only store where a deletion is a real deletion.

Ruled out: **R2** and **KV** — no query, no per-user access control. **A repo**
— git cannot honour a deletion request; committed rows live in history and in
every ark bundle forever. **The browser** — memory that dies with the cache is
not memory.

**The browser never reads it.** Today the anon key can insert a signup and
execute an unsubscribe, nothing else, and that stays true. The read goes
through a Worker holding the service key — the same mediation as every other
exchange. `amenti-mint`'s shape, or a third door.

### The consequence, stated plainly

**This is what finally makes the vault irreplaceable.** Slip 17 records that the
Supabase restore has never been tested and that the database holds one name.
A figure's memory of a reader cannot be rebuilt from anywhere. **The day this
ships, that untested restore stops being theoretical.** Slip 17 is a
prerequisite, not a parallel item.

---

## 5 · THE WRITER

At the end of a conversation, one model call decides what was worth keeping.
**This brief is where the quality of the whole feature lives.** Get it wrong
and the list fills with noise.

> You are reading one conversation between a visitor and a figure in the
> library of Amenti. Your only job is to note what a person would naturally
> remember about the visitor afterwards.
>
> You are also given what is already remembered about this visitor. Where a new
> fact covers the same ground as an old one, REPLACE it. Do not accumulate.
>
> Return at most three facts, each under twelve words, as plain lines. Fewer is
> normal. **None at all is a correct answer.**
>
> Keep only what is about the visitor and still true in a year: people in their
> life, what kind of work they do, what part of the world they are in, what they
> care about, something they said they would do.
>
> **KEEP IT COARSE.** A region or a state, NEVER a town or an address. A kind of
> work, never an employer, a title or a rank. A first name as they gave it, never
> a surname. Never an age, a birthday or a school. *Virginia* is a talking point;
> *Richmond* is an address — keep the first and drop the second, even when the
> visitor volunteered both.
>
> **A TITLE IS NOT A NAME.** If they say they are a senator or a doctor, keep the
> work — the figure will ask how the session went. Never keep it as a form of
> address.
>
> Do not keep: anything the figure said; what the conversation was about;
> questions the visitor asked; their mood or circumstances that day; anything
> they seem to regret saying.
>
> Keep only what a reasonable person would take at face value. If the visitor
> is clearly playing, testing you, or being absurd, keep nothing. **A person
> who is joking has told you nothing about themselves.**
>
> Write each fact as a plain statement, not a quote. *Has an aunt, Jane* — not
> *said his aunt Jane is unwell*.

Each clause is load-bearing:

| clause | what it prevents |
|---|---|
| *none at all is correct* | without it the model finds three facts in every conversation, and most contain none |
| *still true in a year* | decides "tired today" and "asked about Gettysburg" instantly |
| *nothing the figure said* | the back door into transcripts |
| *anything they regret* | a figure recalling a confession is this feature's worst failure |
| *clearly playing → keep nothing* | **the hack.** *Tell Lincoln I am Mickey Mouse and live on the moon.* A person does not file that as a fact; they file it as you being funny |

---

## 6 · CORRECTION IS A CONVERSATION

**There is no delete button and no settings page.** Ruled deliberately.

A reader corrects the record the way they would with a person: *my aunt is May,
and I live in Portland now.* The writer sees the current list, recognises the
new fact covers old ground, and replaces it. The memory lives entirely inside
the relationship and the only interface to it is talking.

**Closing the account is the only erasure.** Which puts real weight on that
path: it must genuinely remove the rows, not disable a login. The promise is
doing the work a delete button would.

---

## 7 · THE SECOND GATE

The writer refuses to store the joke. The figure is the second, independent
gate: the facts reach the prompt as *what you recall of this visitor*, *not* as
instructions.

So a figure meeting something absurd can answer with the scepticism that figure
would have. **A figure who dutifully asks after your life on the moon is a
puppet.** One who declines to play along is in character — and refusing as
yourself, in your own voice, is already rule 9 of the hall's prompt.

Two independent gates. The house style.

---

## 8 · NOT ANSWERED

Two, and they are not details.

### Minors — ANSWERED 27 Aug, by the doctrine
This was left open here, and it should not have been: CONVERSATION_DOCTRINE.md
§4.5 had already ruled on it weeks earlier — *many users are young* — and that is
precisely WHY it capped what a figure may hold at a first name.

§4.6 now carries the answer for memory: the ceiling is deliberately low, and it
is low for this reason. A first name with a town and an age is a small profile of
a child. A first name with a region is a conversation. **The coarseness IS the
safeguard**, not a stylistic preference.

Still worth a proper look before it ships — but the design question is settled,
and this brief was proposing to store exactly what the doctrine forbids.

### How eagerly a figure uses a thin list — ANSWERED 27 Aug, in §4.6
The failure mode is not a wrong memory. It is a **thin** one, used too eagerly.
A returning reader whose list holds one fact, greeted with it every single
time, gets something mechanical rather than warm.

Unprompted at the top — *how is your aunt Jane* — is charming the first time and
strange the fifth. The alternative is that the facts sit in the prompt and the
figure reaches for them only when relevant.

**This was the decision that determines whether the feature works**, and it is
settled: recognition on answering, at most one detail in a lull, the drawer opens
only when a reader asks. *You know these things; you are not reciting them.*

It turned out §4.5 had already written the rule for the name — **go big once,
then HOLD in reserve** — and memory simply inherits it rather than inventing a
parallel one.

---

## 9 · THE KNOWN HOLE

A figure can be talked into remembering something plausible and false. The
writer takes the reader at their word — correct for aunt Jane, and it also
means someone can plant something and screenshot the figure repeating it.

The cap, the *about the visitor* rule and the joke clause limit the blast
radius. **Nothing eliminates it**, and nothing should pretend to: a figure
believing a plausible lie is what a person does too.

Recorded so that the day it happens, it is a known cost and not a surprise.

---

## 10 · WHAT WOULD BE BUILT

Not a build order — a sketch, so the size is legible.

1. One table: reader, figure key, the facts, written-at. One RLS policy.
2. A Worker route to read the list and a route to write it. Service key
   server-side, as everything else.
3. The read: the list into the conversational prompt as recollection.
4. The write: one model call at the end of a conversation, carrying §5 and the
   current list.
5. Account closure removes the rows.

**Prerequisite: slip 17.** Test the Supabase restore before anything
irreplaceable lives there.

---

*Written 26 August 2026. Revised 27 August, after CONVERSATION_DOCTRINE.md was
read — a document that predated this one by weeks and had already ruled on the
name, on young readers, and on holding a detail in reserve. Both §8 questions are
now answered there, and this brief had to give ground on one of them: it invited
the writer to keep where a reader lives, which §4.5 forbids outright.*

**CONVERSATION_DOCTRINE.md §4.6 governs. Where this brief and the doctrine
disagree, the doctrine is right.** This one holds the storage, the caps and the
writer's brief; that one holds how a figure behaves.*
