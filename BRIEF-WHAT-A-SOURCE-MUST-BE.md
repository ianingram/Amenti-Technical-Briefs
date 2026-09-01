# BRIEF · WHAT A SOURCE MUST BE
**The citation policy, its instruments, and the claim it holds up · Ingram Manor LLC · 1 September 2026**

Written from `probes/probe-citations.mjs`, `tools/cite.js`,
`.github/workflows/citations.yml` and the live `CITATIONS.json`. Where this
brief and a register disagree, the register is right and this has gone stale.

> **THE MACHINERY EXISTED FOR DAYS BEFORE THIS DOCUMENT DID.** A probe grading
> 550 works, a workflow that refuses a commit, a stamping tool, a reading, and
> an addendum listing what is left. What did not exist was the POLICY —
> what a source must be, why there are four grades and not two, and what the
> whole apparatus is protecting. It lived distributed across a workflow, a probe
> and a log. Seventy-two briefs on this ship and none of them was this one.

---

## 0 · WHY IT MATTERS MORE THAN IT DID LAST WEEK

The citation work was finished before Ask Amenti was built. It now carries a
weight it was not originally asked to carry.

The hall's entire claim is one sentence: **what the library holds can be
checked, and a model's memory cannot.** What a model has on Caesar is secondary
text about him, absorbed at a remove, unattributable. What the library has is
what he wrote, in a named edition, traceable back.

Strip the citations out and that distinction collapses. Ask Amenti becomes an
ordinary chatbot with a citation habit — which is worse than one without,
because the citation lends authority to whatever follows it.

So the policy below is not housekeeping. **It is the thing being sold.**

---

## 1 · THE POLICY, IN ONE LINE

> **A QUOTATION WITHOUT A SOURCE IS A THING SOMEBODY REMEMBERS.**

Everything else is the working out of that.

A source is not a gesture at provenance. It is an instruction for finding the
same words again. The test is not *does this look sourced* but **could a reader
who does not trust us reach the identical text?**

That is why the grades are what they are.

---

## 2 · THE FOUR GRADES, AND WHY NOT TWO

A boolean — sourced or not — would have declared this work finished months ago
and hidden most of what was wrong. `probe-citations` grades every work into
four states, and the middle two are the point.

**CITED — an edition that can be found again.** A Gutenberg number, an Internet
Archive item, a named scan. **The only grade that is done.**

**DATED — a work and a year, no edition identifier.** Findable by a person, not
by a machine, and ambiguous wherever a translator revised.

**THIN — a translator or a title and nothing to locate it by.** *"Jowett
translation"* names WHO but not WHICH. This grade exists because of a fact
specific to a library of translated primary sources:

> **For a text in translation the edition is half the citation.** A famous line
> can exist in one English text and not another. Naming the translator without
> the edition tells a reader which century they are reading and not which words.

**EMPTY — no source at all.** The only grade that fails a build.

### And one state that is not a fault

**LINKED — the room sends the reader out to the text, or to another shelf on
this site.** A url IS a citation. Musashi is link-out; Nimrod's Josephus entry
points at Josephus's own shelf here.

The probe's own comment on why this matters:

> *Counting those as faults would teach the reader to ignore the report, which
> is how a guard dies.*

That principle recurs below and it is the sharpest thing in this file.

---

## 3 · THE READING, TODAY

From `CITATIONS.json`, generated 31 Aug 18:50, over 52 rooms:

```
works        550
CITED        495     90%   an edition a reader can reach
LINKED         9      2%   sent out to the text, not a fault
DATED          7      1%
THIN          39      7%
EMPTY          0      0%   ← the number that matters
```

**Forty-two rooms of 52 are wholly clean** — every work either CITED or LINKED.
Ten are not, and the shape of what
remains is informative: `akhenaten`, `confucius`, `john-milton` and `plato` are
six-work rooms sitting entirely at THIN — a translator named, an edition not.
That is one decision per room, not thirty-nine separate problems.

`lincoln` holds 81 works with 79 CITED. `einstein-albert` has one DATED entry.
The tail is short and it is enumerated, which is the difference between work
remaining and work unknown.

---

## 4 · WHAT REFUSES A COMMIT

`citations.yml` fires **on every change to `library/`**, on a `:47` rung, and by
hand. Its own note on why change and not only clock:

> *the moment to ask where a text came from is the moment it arrives.*

The gate is narrow on purpose. **EMPTY fails the build. Nothing else does.**

```
exit 0   nothing empty        pass
exit 1   at least one EMPTY   ← a finding, gate on it
exit 2   the audit could not run   ← reported as a separate error
```

That third state is doctrine, not defensiveness. An early version of this
workflow ended a line with `|| echo empty=1`, so **a crash, a missing
`LIBRARY.json`, and a genuine empty source all produced the same signal.** An
instrument that cannot distinguish *broken* from *found a fault* is reporting
its own health as the ship's.

**Why THIN does not fail the build.** Thirty-nine works are THIN today. Gating
on THIN would make the build red for weeks over work that is scheduled and
understood, and a permanently red build is a build nobody reads. EMPTY is
different in kind: an empty source is not an incomplete citation, it is a
quotation with nothing behind it at all.

---

## 5 · THE TOOLS, AND THE RULE THEY BOTH OBEY

**`tools/cite.js` — the stamp.** Puts a source onto every STORED work in a room
manifest that has none. Report-only unless `--write`. **It never overwrites an
existing source, and never touches a link-out, because a url IS its citation.**

**`.github/workflows/cite-a-room.yml` — the bulk hand.** Give it a room key and
a citation from the Actions tab; it stamps every unsourced work in that room,
regenerates `LIBRARY.json` and `CITATIONS.json`, and commits. **Dry run is on by
default.**

Both obey the same rule, and it is the rule this section exists for:

> **NEVER OVERWRITE. ONLY FILL.** A tool that can improve a citation can also
> silently replace a correct one, and nothing would report the loss. The
> asymmetry is deliberate: filling a gap is safe to automate, judging an
> existing source is not.

---

## 6 · TWO FAULTS THE PROBE HAD, AND WHAT THEY TEACH

Both are recorded in the probe's own source, and both are the same lesson.

**It graded the proprietor's own works DATED.** *"Ian Ingram, The Siege of
Amenti (2026) · Ingram Manor LLC"* is a complete citation — author, title, year,
publisher — and the first version flagged all six for lacking a Gutenberg number
**that cannot exist for a work this project published itself.**

**It nearly tested for the publisher's name.** *"Project Gutenberg · public
domain"* has the words and no number, and the Hume room's thirteen entries all
read exactly that way. The test must be for the IDENTIFIER, never for the
publisher.

> **A RULE THAT FLAGS CORRECT WORK TEACHES THE READER TO IGNORE THE REPORT.**
> That is how a guard dies — not by being switched off, but by crying wolf until
> nobody opens it.

The same principle produced the LINKED state in §2. Three separate corrections,
one doctrine: **the cost of a false positive is the whole instrument.**

---

## 7 · WHERE THE POLICY NOW REACHES — THE HALL

The hall opens rooms and quotes from them. That extends the policy into two
places it did not previously have to reach, and both are recent.

### The quotation rule

`buildAnswer` tells the model to quote, and to quote **only** from the text it
was handed this turn. The reason is exactly the policy:

> The model knows famous passages from these authors in translations that are
> **not** the edition aboard. A remembered line printed under a real SOURCE line
> attaches a genuine citation to words the library does not contain.
> **That makes the edition a lie** — precisely what §2's THIN grade exists to
> prevent, arriving through the front door.

### The guard that does not exist yet

The rule above is a **promise, not a test.** Nothing checks that a quoted span
appears in the passage that was fetched.

> **A VERBATIM QUOTE MUST BE A SUBSTRING OF THE TEXT FETCHED THIS TURN.**

Mechanically checkable. Not built. **THE STANDING SLIP #13, move E, and the
largest open gap in this policy.** Every other rule here has an instrument; this
one has a sentence.

### And a hole the register cannot see

`library.js` declares four work modes. One of them, `recall`, **reconstructs a
public-domain passage through the AI bridge** — there is no file. So the
substring guard would have nothing to test against, and a passage arrives from a
model wearing a citation.

Worse: **`LIBRARY.json` keeps only `title`, `section` and `source`.** It drops
`mode`. From the aggregate register a stored primary source and a reconstructed
passage are **indistinguishable**, and nobody can currently say how many of the
550 are `recall` — it may be zero, in which case this is a latent trap rather
than a live one. SLIP #13, move G.

---

## 8 · WHAT IS OPEN

**Nine rooms name a translator and stop short of an edition.** Written up with
the method in `slip/SLIP-ADDENDUM-THE-EDITIONS.md`. Not urgent; nothing is
wrong. Read the addendum rather than planning it from this brief.

**The substring guard is a rule and not a probe.** §7. The one that matters.

**`mode` is dropped from `LIBRARY.json`.** §7. Until it is carried, no
instrument can tell a fetched text from a reconstructed one.

**And the policy had no document until today**, which is its own kind of
finding: every part of this was decided correctly, written into a comment or a
workflow header, and never gathered. The next thing decided about citations
should land here.

---

## 9 · THE SHORT VERSION

- A source is an instruction for finding the same words again.
- Four grades, because a boolean would have called this finished and hidden the
  translations.
- For a translated text, **the edition is half the citation.**
- EMPTY fails the build. Nothing else does, because a permanently red build is
  a build nobody reads.
- Tools fill gaps and never overwrite.
- A rule that flags correct work destroys the instrument that carries it.
- And the hall may quote **only** from the text it was handed — which is
  currently a promise, and should be a probe.

---

*Written 1 Sep 2026 because seventy-two briefs existed and none of them was
this one. Figures from `CITATIONS.json` generated 31 Aug 18:50 — 550 works, 495
CITED, EMPTY zero.*
