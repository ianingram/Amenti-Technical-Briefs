# THE CHAMBER
### Ingram Manor LLC · 26 August 2026 · what a chamber is, and the vocabulary it runs on

A **chamber** is a named set of souls whose rooms are read together.

The library gives every soul a room. A chamber gives a reader a reason to open
several of them at once: every inaugural address in order, every proclamation
on one subject across two centuries, the same question put to men separated by
seventy years. That is a reading a per-soul room cannot produce, and it is the
only argument for the chamber existing.

**Nothing is built.** This document exists so that when it is, it is built on a
decision rather than a guess — and so that the schema work already done is not
undone by somebody who did not know why it was done.

---

## 1 · WHAT A CHAMBER IS NOT

**It is not a container.** A soul does not live in a chamber. The chamber holds
a list of keys and the souls carry on exactly as they were. This is the same
model `AMENTI_ERAS` already uses — a name and a list of members — and it is
chosen for a reason: a soul can belong to several chambers, or to none, and the
library is unbothered either way. Louis XIV is a king and could also be a
builder. A poet is in no chamber at all.

**It is not the Browse taxonomy.** `Page1.html` already rolls ~118 roster
titles into twelve groups by keyword — Rulers & Statesmen, Writers & Poets,
Faith & Pantheon. That mechanism is doing a different job and doing it well:
broad browsing by kind, over a roster of 1,011, without anybody maintaining a
list.

> **DO NOT ADD PRESIDENTS TO THE BROWSE TAXONOMY.**
> `'president'` is already a keyword under `rulers`. Forty-five presidents
> would land in one chip alongside kings, pharaohs, khans and senators, and
> that chip becomes the library. Worse, keyword matching would be asked to
> rediscover a closed, known list from free-text prose, and would then be
> patched forever for the president of a company, a university, or France.
>
> **A chamber is a closed list of souls. The taxonomy is a rule.** Two jobs,
> two mechanisms. Keeping them apart is the whole design.

---

## 2 · THE FIRST CHAMBER

**U.S. Presidents.** Chosen first because the documents justify it and nothing
else does yet:

- **The corpus is public domain by statute.** Works of federal employees in the
  course of their duties. No permission, no attribution, no licence to track.
- **It is complete and machine-readable.** Proclamations, executive orders,
  messages to Congress, inaugurals — stable public URLs.
- **The rooms already exist and are proven.** Washington, Jefferson and Lincoln
  are aboard with real primary sources behind them.

**Kings, popes and queens are NOT the next chamber by default.** The same
structure would deliver much less, because their corpora are thinner and far
more scattered. Generalise when something else has documents this good — not
because the shape happens to fit.

---

## 3 · THE TWO SHAPES OF ROOM, AND THE ONE TO PREFER

Read on 26 August across the three existing rooms:

| | works | sections | room note | modes |
|---|---|---|---|---|
| **Washington** | 5 | *The boy · The office · The letters* | yes | stored |
| **Jefferson** | 4 | *His own account · The correspondence · The office* | yes | stored |
| **Lincoln** | 82 | *Early Years · 1832–1853* … | **no** | stored + link |

**Washington and Jefferson are the same room, schema for schema.** Identical
fields, thematic sections, and a hand-written `note` that reads like a
curator's wall text. Five documents chosen so a reader can watch the reserve
being assembled.

**Lincoln is a different object** — an archive that happens to be complete.
Chronological sections, mixed modes, no note.

Neither is wrong. But a chamber presenting both has to decide which it is
showing, and the curated shelf is the better read.

> **The 82 cannot be edited into 5.** Selecting five IS the curation, and the
> notes on the other two shelves are the best writing in the library. A curated
> Lincoln is a NEW file beside the complete record, not a replacement for it —
> and his sections already end with *The Complete Record*, which suggests
> whoever built it was thinking the same way.

---

## 4 · THE TYPE VOCABULARY — A CONTRACT

Before 26 August, **no work in any room carried a `type` or a `year`.** The
only fields common to every work were `id`, `mode`, `section`, `title`, and the
only section string shared by more than one room was *The office*.

Which meant a chamber could only line up inaugurals by matching words inside
prose titles. That works for exactly that case and breaks on the next one.

**All 91 works across the three rooms now carry `type` and `year`.** Nothing
was removed, reordered or altered; both fields were added.

```json
{ "id": "03-first-inaugural",
  "section": "The office",
  "title": "First Inaugural Address — 30 April 1789",
  "type": "inaugural",
  "year": 1789,
  "mode": "stored", … }
```

### The eighteen terms

`inaugural` · `annual-message` · `message` · `proclamation` · `order` ·
`debate` · `reply` · `speech` · `address` · `remarks` · `appeal` · `letter` ·
`note` · `fragment` · `opinion` · `declaration` · `autobiography` · `journal` ·
`rules` · `collected`

**Room 46 must use these words.** A new term is a deliberate addition to this
list, not a local choice inside one file — the moment two rooms spell the same
thing differently, the chamber stops being able to line them up and nothing
announces it.

### Order is the decision

The vocabulary was derived from the titles themselves, not invented. Titles
overlap, so the rules are applied most-specific-first and the first match wins:

- *Reply to Douglas in the First Joint Debate* → **debate**, not `reply`
- *First Inaugural Address* → **inaugural**, not `address`
- *Annual Message to Congress* → **annual-message**, not `message`

**That ordering is the only real judgement in the whole pass.** Change the
order and the corpus re-labels itself silently.

### What was refused

Four works carry no `year`, and were left empty rather than filled:

| room | work |
|---|---|
| Washington | Rules of Civility and Decent Behaviour |
| Washington | Masonic Correspondence |
| Jefferson | The Draft Declaration, with the passages Congress struck out |
| Lincoln | Collected Works — the complete papers |

A year was only ever taken from the title's own text. The Draft Declaration is
1776 and everybody knows it — **and inventing it would make the field
untrustworthy everywhere else.** Two of the four are genuinely spans rather than
dates and may want a `years` field instead of a `year`.

---

## 5 · WHAT A CHAMBER FILE WOULD HOLD

Sketch, not a spec. The point is how little it is.

```json
{ "key": "us-presidents",
  "name": "U.S. Presidents",
  "note": "the curator's wall text, in the voice the shelves already use",
  "souls": ["george-washington", "thomas-jefferson", "lincoln"] }
```

**Keys, never indices.** `AMENTI_ERAS` groups with `chars:[2,6]` — positions in
an array. That was fine for fourteen hardcoded figures and is a fault waiting
at forty-five: insert a soul in the middle and every group silently regroups.

---

## 6 · THE ORDER OF WORK

1. **Rooms first, chamber second.** A chamber over full rooms is a comparison.
   A chamber over empty ones is a filtered list.
2. The chamber over the three that exist, before the other forty-two. Three is
   enough to know whether the reading is worth the corpus work.
3. The comparison view — every inaugural side by side. **This cannot be judged
   in the abstract.** Three is enough to see whether it reads as insight or as
   a list.
4. Only then the corpus.

---

## 7 · NOT ANSWERED

**The living ones.** The roster is explicitly the dead — *a soul is one of the
dead on the roster*. Presidents from Carter forward have no rule. This is the
same open question the handoff records about a living author's room, arriving
from a different direction, and a presidential chamber forces it.

**The unevenness.** Washington left comparatively little; a modern president
generates more in a year than a nineteenth-century one did in a term. Built
from "everything available", recent presidents look enormous and early ones
look thin — an artefact of record-keeping, not of the person. Curation is the
answer, which is another argument for the shelf over the archive.

---

*The `type` and `year` pass was run 26 August 2026 across
`george-washington.json`, `thomas-jefferson.json` and `lincoln.json`. Verified
work by work against the originals: 91 of 91 typed, 87 dated, nothing removed,
no existing field changed, order preserved.*
