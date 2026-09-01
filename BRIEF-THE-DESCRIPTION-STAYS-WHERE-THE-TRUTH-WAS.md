# BRIEF · THE DESCRIPTION STAYS WHERE THE TRUTH WAS
**A fault with no error message, five instances in one night · Ingram Manor LLC · 1 September 2026**

Written from five faults found on 31 August and 1 September, none of which was
looked for. Where this brief and a register disagree, the register is right and
this has gone stale — which is, unavoidably, the subject.

> **NOBODY WROTE A BAD LINE.** Every description in this brief was TRUE when it
> was written. Every one of them was still sitting there, unchanged and
> confident, after the thing it described had moved. No test failed. No build
> went red. Nothing threw. The system carried on being correct in the code and
> wrong in the account of itself, and the gap widened at the speed of good work.

---

## 1 · THE SHAPE

A thing is built. Someone writes down what it is — in a gloss, a comment, a
nav list, a probe, a folder name. **The writing is accurate.**

Then the ship moves. The file grows a new capability, the engine is extracted
into a bundle, a pane is repurposed, a section fills up.

**And the description stays where the truth used to be.**

It does not decay. It does not warn. It reads exactly as authoritative on the
day it becomes false as on the day it was written — more so, because it has
been sitting there longer and nobody has questioned it. The only signal is a
reader acting on it and being wrong.

**This is not carelessness.** It is what happens in a system built by doing
rather than by specifying. Nobody forgets to update a description; the
description is simply not where the work is happening, and the work is what
demands attention.

---

## 2 · THE FIVE

### ① The gloss that said *microphone*

`Page2.html` is 1.5 MB. It holds nine views, a double helix of sovereigns and
events over a Truth Axis, a years-per-revolution control, a hash router, and an
events register pulled from a published Google Sheet.

Its entry in `SOURCES.json` read, in full:

> *THE SOVEREIGN INSTRUMENT. The second application, reachable from the
> flagship — its own microphone, its own chunker (MAX_CHARS 1100) and its own
> daily generation path.*

199 characters. **Accurate when Page2 was a voice instrument.** The helix
arrived afterwards and nothing updates a gloss when a file grows.

**The cost was not abstract.** The hall answers from these lines. Asked whether
the site has a timeline, it said there was none. There is. It reasoned
correctly from what it had.

### ② The engine that moved out from under its probe

`probe3` tests whether the figure can be interrupted. It reads
`window.AMENTI_VOICE` out of `Page1.html` and checks for `_seq`, the mechanism
that orphans an in-flight fetch.

The voice engine was later extracted into `amenti-core.bundle.js` as
`Amenti.conversation` — **the right repair, and the doctrine records why.** What
remains in Page1 is a façade that forwards.

So `probe3` reports seven failures. All seven are its own. `_seq` appears six
times in the bundle and zero in Page1. **It is testing the place the repair
moved away from**, and it has been for weeks — invisibly, because nothing runs
it.

### ③ The pane whose name outlived it

Page1's `BROWSE` tab is `data-target="timeline"`. The pane behind it reads
*THE CODEX · BROWSE BY ORDER — every legend in the archive, gathered by their
order*, indexed `AMENTI/BRW/v1.0`. **It is a roster browser. It is not a
timeline.**

Anyone grepping Page1 for "timeline" finds a tab and concludes the flagship has
one. On 1 Sep the assistant did exactly that, and had to be corrected by
reading the pane.

### ④ The navigation that lived nowhere a reader could find it

Eleven labels sit in the flagship's markup. Nothing else knew them. So the hall
— which answers questions about this ship — could name `Page2` from the register
and had no idea that `INTERFACE`, one word to the right of the box the visitor
had just typed into, *is* Page2.

It sent them to *the Harbor* instead: a different repo, on a branch, behind a
`fleet-nav.js` that 404s. **Inference from two glosses sitting near each other**,
which is what a system does when the true answer is written nowhere it can read.

### ⑤ And the register's own furniture

The index groups documents into eight sections. One of them is named:

```
the briefs — 41 files, 8 of them linked anywhere
```

**It holds 75.**

The label that organises the register carries a count that rotted, and it is
printed into every door list the hall sends. **The instrument built to catch
this fault has the fault in its own furniture** — which is the most honest thing
in this brief, and the reason §4 is written the way it is.

---

## 3 · WHY THE REGISTER IS THE ANSWER, AND WHY IT IS NOT ENOUGH

`SOURCES.semantics.json` exists for exactly this. Its own law:

> **A SOURCE THAT CANNOT BE REACHED IS NOT A SOURCE. It is a thing somebody
> remembers.**

That is the right principle and it caught most of what it was built for. But
notice what the register can currently tell you about a file:

```
is it REACHABLE      yes, by walking it
is it DESCRIBED      yes, by checking for a gloss
IS THE DESCRIPTION STILL TRUE      — nothing. no mechanism. no field.
```

**A gloss is `described: true` forever.** The walk cannot read it. Nineteen
entries have no gloss at all and the drift report names every one — that fault
is watched. A gloss that is present and false is invisible, and it is the more
dangerous of the two, because a missing description makes a reader look and a
wrong one makes them act.

> The register is the answer to this fault, and **the register only holds what
> someone thought to put there.** It is a promise kept by hand, in a system whose
> whole method is not to keep promises by hand.

---

## 4 · WHAT WOULD ACTUALLY CATCH IT

Three things, in order of how much they buy.

**① A FRESHNESS READING, NOT A FRESHNESS RULE.** Git already knows when a file
last changed and when its gloss last changed. A probe comparing the two would
have flagged Page2 months ago: 1.5 MB of commits against a description untouched
since it was written. **This does not need to judge whether a gloss is true** —
only that the file has moved a long way since anyone looked at the sentence.
That is a reading a machine can take, and it is the whole of what was missing in
①, ②, ③ and ⑤.

**② DERIVE WHAT CAN BE DERIVED.** ⑤ is stale because a count was typed into a
name. ④ is stale because a nav was typed into a prompt. Both are readable from
the source: a section's count is `length`, and the flagship's nav is its
`<a class="mn-*">` tags and `<section data-page>` targets. **A derived
description cannot rot.** Where a fact can be computed, computing it is not an
optimisation — it removes a class of fault entirely.

**③ AND WHERE A DESCRIPTION MUST BE AUTHORED, SAY SO IN IT.** Some things cannot
be derived: intent, authority, warnings, *which* Brutus. Those must be written
by hand and will go stale. The mitigation is not discipline, it is **honesty in
the entry** — record what was read to write it, and what was not:

> *This sentence was written on 1 Sep from the workflow that runs it and the
> file it produces, NOT from the probe's own source.*
>
> *WALKS THE FLAGSHIP — and NOTHING IN THIS ENTRY WAS READ FROM ITS SOURCE.
> Replace this sentence with what it does.*

Both are real entries added on 1 Sep. **An entry that names its own limits is
still useful when it is wrong**, because the next reader knows which part to
distrust. A confident wrong sentence gives them nothing.

---

## 5 · THE COROLLARY FOR PROBES

② is the same fault wearing an instrument's coat, and it generalises past
descriptions.

`probe3` tests `_seq`. `_seq` was an implementation of an intent — *the figure
can be interrupted*. The implementation moved and the probe broke.

> **A TEST WRITTEN AGAINST AN IMPLEMENTATION BREAKS WHEN THE IMPLEMENTATION
> MOVES. A TEST WRITTEN AGAINST THE INTENT WOULD HAVE SURVIVED THE EXTRACTION
> UNTOUCHED.** The engine moved. The intent did not.

Its replacement, `probes/probe-interrupt.mjs`, asks the doctrine's question
instead: can the figure be interrupted on the flagship today? It checks the page
loads the core, the core has brakes, and — the part nobody was watching — that
calling the page's `stop()` actually reaches the engine's. That last one is the
joint where the intent can fail while every existence check passes, which is the
doctrine's own last law in a new coat: **being loaded is not being used.**

---

## 6 · HOW TO SEE IT AT ALL

None of the five was found by looking for it. Each was found the same way:
**something read a description and acted on it, and the result was wrong in a
way that had to be explained.**

- The hall said there is no timeline. There is.
- A probe reported seven failures. The ship was fine.
- A grep for "timeline" found a tab. It was a roster browser.
- The hall sent a visitor to a repo instead of the tab beside them.
- A section named `41 files` was printed into every prompt while holding 75.

**The hall did most of this work without being asked to.** A surface that
answers about the ship from the ship's own registers is a continuous audit of
whether those registers are true. It has no opinion and no memory; it simply
uses what is written, and when what is written is false the answer comes out
visibly strange. That is worth more than the feature.

> **BUILD THINGS THAT READ THE REGISTERS OUT LOUD.** They will embarrass the
> registers, which is the point.

---

## 7 · THE SHORT VERSION

- A description does not decay. It stays confident and becomes false.
- The register catches `undescribed`. It cannot catch `described and wrong`.
- Compare a file's age to its gloss's age — that alone would have caught four
  of the five.
- Derive every fact that can be derived. A derived description cannot rot.
- Where a description must be authored, **name what it was written from and
  what it was not.**
- Test intents, not implementations. The engine moves; the intent does not.
- And build surfaces that read the registers aloud, because a wrong answer in
  public is the only alarm this fault has.

---

*Written 1 Sep 2026 at the captain's instruction, after the same fault appeared
five times in two sessions. Nothing in it was searched for. Every instance was
tripped over while doing something else, which is the argument of §6 and the
reason this brief exists rather than a probe — the probe in §4① is the thing to
build, and it is not built.*
