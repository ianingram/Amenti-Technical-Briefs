# BRIEF · THE WALL AND THE PROMPT
**How Ask Amenti is assembled, and how it was built · Ingram Manor LLC · 1 September 2026**

Written from measurements taken against the live registers by
`probes/probe-hall-wall.mjs`, which lifts the hall's own functions out of the
shipped `amenti-hall.js` and runs those. Where this brief and a register
disagree, the register is right and this has gone stale.

> **THE HALL IS A NEW SURFACE, AND IT IS NOT A NEW BUILD.** It stands on the
> citation campaign that produced 550 sourced works, on the register that
> describes 191 documents, on the roster of 1,011 souls, and on a probe corps
> whose doctrine is to accuse the system before it can lie to its captain.
> None of that was built for the hall. All of it is what made the hall
> possible in a night and a day.

---

## 1 · THE WALL

The hall speaks through one door: `window.claude.complete`, into the Amenti
proxy. The proxy enforces a ceiling on the system prompt:

```
SYSTEM_CHARS = 20,000
```

Three things about it are load-bearing and are regularly misremembered.

**IT REFUSES. IT DOES NOT TRUNCATE.** An overrun comes back as
`system_too_long` — a 413 with a named reason in the body. So a prompt that is
one character too long does not produce a slightly worse answer. It produces
**no answer at all**, on every question, until the prompt is smaller. A silent
hall, not a degraded one.

**IT IS THE WORKER'S, NOT THE HALL'S.** `SYSTEM_CHARS` is enforced in
`Amenti-Workers`, which is private. Nothing in `amenti-hall.js` declares it; the
number appears only in comments. Every measurement in this brief is therefore
taken against a DECLARED wall, and `probe-hall-wall` labels it so in every
report. `--wall=N` overrides it. A number that is measured against and never
observed should never be mistaken for a reading.

**AND THE POLICY IS NOT TO RAISE IT.** The Worker's own rule, written after a
real overrun: *if a surface 413s here, CHUNK THE SURFACE.* This brief does not
argue with that, and §3 shows why raising it would not have helped anyway.

---

## 2 · HOW THE HALL WENT SILENT

The original design was correct and it is worth stating before its replacement,
because the replacement inherits its ethic.

**The hall declared every document on every question.** All 191, one line each,
because a retrieval pass can miss and never say it missed. Nothing could be
invisible. That is the Silent Signature refused at the level of a prompt.

It stopped being possible by being used successfully:

```
the catalogue was sized when the index held      106 documents
the index held, on 31 August                     191 documents
```

Nobody wrote a bad line. Documents were added, each costing ~85 chars of prompt,
and one of them crossed a wall nobody was watching. Measured on 31 August:

```
HALL.md          5,751
the counts         599
the catalogue   16,160     191 entries
the rules        1,698
                ──────
SYSTEM PROMPT   24,138     wall 20,000 — OVER by 4,138
```

**The Ask Amenti box had been answering nothing, on every question, for an
unknown period.** It was found by building an instrument, not by a visitor.

---

## 3 · WHY TRIMMING WAS NEVER THE ANSWER

The obvious fix is to shorten each gloss. It buys weeks:

```
trim 90 -> 139 documents fit    already over
trim 40 -> 232 documents fit    ~42 headroom
trim 24 -> 301 documents fit    ~111 headroom
```

And it dies immediately against what the box is FOR. Ask Amenti must reach the
architecture, the library and the roster:

```
the architecture      190 documents
the library           550 works
the roster          1,011 souls
                    ─────
                    1,751 entries

at 85 chars each   148,835      7.4x the whole wall
at a hard trim      87,550      4.4x
at BARE IDS          36,771     1.8x the wall — 3.1x the space actually free
```

**Every description deleted still overruns three times.** There is no trim, no
compression and no larger wall that reaches it. The declare-everything design
was finished, and the only question was what replaced it.

---

## 4 · THE DOORS

The corpus has a shape that solves this for free. The library is not 550 loose
works — it is **52 rooms**, one per figure. The documents are not 191 loose
files — they are **8 sections**, already declared in `SOURCES.json`.

So the hall declares DOORS, not leaves:

```
-- THE ARCHITECTURE: 8 sections --
· the surfaces — 10 documents, e.g. codex-html, page1, page2, court
· the instruments — 45 documents, e.g. workflow-citations, probe-citations
  ...

-- THE LIBRARY: 52 rooms, 550 works --
· brutus — Brutus, 5 works: The disguise; The overthrow; The price
· dante-alighieri — Dante Alighieri, 9 works: Inferno; Purgatorio; Paradiso
  ...
```

**And it barely grows.** A new work adds no room. A new brief adds no section.
The growth that broke the hall is no longer charged to the prompt at all — the
probe reports it plainly: *a new document inside an existing section costs
nothing.*

### The section titles are the whole point

Each room shows up to three of its own section titles, and each ship section
shows a few of its document ids. That costs 3,444 chars over a bare list, and it
is the difference between a lookup and a search:

> Asked *which of the people aboard wrote about betrayal*, the hall reached
> Brutus. **The word "betrayal" appears nowhere in the doors.** It arrived
> through *The overthrow* and *The price*. Fragment search could not have done
> it; there is no fragment to match.

Pay for reach where reach happens. When the door list is sent for any other
purpose, it goes BARE — see §5.

---

## 5 · TWO CALLS

```
CALL ONE  · route     the doors + a question   ->  JSON: which rooms, which sections
CALL TWO  · answer    what was opened          ->  the answer to the visitor
```

**Call one is deliberately starved.** It gets the doors and nothing else — no
HALL.md, no counts, no rules about how to write. It is not addressing the
visitor; it is pointing. Small keeps it cheap and keeps it from starting to
answer.

**Call two does not carry the door list.** That is the arithmetic that makes
everything else possible: ~6,400 chars leave the prompt the moment the choice is
made, and the passages move into the space.

### Three kinds of door, and they behave differently

**A LIBRARY ROOM OPENS.** Fetch `library/{key}.json`, select the works whose
section the router named, fetch up to `MAX_WORKS` bodies sliced to
`WORK_SLICE`. The library's primary source is the WORK, so the gloss points and
the text must be fetched.

**A SHIP SECTION DOES NOT OPEN — IT IS ALREADY OPEN.** The ship's primary source
IS the gloss: an authored sentence per file, already in `SOURCES.json`, already
loaded on every question. Fetching 1.5 MB of `Page2.html` to learn it holds a
helix would be absurd when someone already wrote the line. So a section pick
costs **no fetch at all**; it means *include these entries*, trimmed, under
`SECTION_BUDGET`.

**NOTHING FOUND sends the bare door list**, so the hall can name the nearest
rooms without inventing one — and only the bare form, because naming a room
needs a name, not its section titles.

### The authored notes

Room catalogues carry a `note` per room and per work, written by hand. They were
discarded until 31 August, and one of them is load-bearing:

> The room `brutus` is **LUCIUS** Junius Brutus, who overthrew the monarchy in
> 509 BC — not Marcus, who killed Caesar. A visitor asking about betrayal may
> mean either. Without the note the hall opens Lucius's room for a Marcus
> question and its own training supplies the assassination **under a Livy
> citation.** The librarian saw it coming: the note opens *FIRST, WHICH BRUTUS.*

Carried under one shared `NOTE_BUDGET`, room notes first — being wrong about
WHO is worse than being thin about WHAT.

---

## 6 · WHAT THE PROMPT IS MADE OF

Measured 1 September, live:

```
CALL ONE   routing                                     8,047
   the doors                                           6,390
   the framing                                         1,657

CALL TWO   answering — the worst of its shapes        17,961   of 20,000
   HALL.md                                             5,751     29% of the wall
   the counts (HALL-STATE.json)                          599
   THE NAV                                               832
   the rules                                           5,221
   passages · 4 works x 830                            3,320
                                                      ──────
                                                       2,039 to spare
```

The other shapes of call two, all measured:

```
the ship's register   17,895    5,800 of section glosses
nothing found         14,103    2,368 of bare doors
```

### The budgets trade against one another

```
MAX_ROOMS 3   MAX_WORKS 4   WORK_SLICE 830
SECTION_BUDGET 5,800   SECTION_GLOSS 90   SECTION_IDS 4
NOTE_BUDGET 900   ROOM_NOTE 500   WORK_NOTE 250
ROOM_SECTIONS 3
```

Ten constants against one wall across four prompt shapes. **Every attempt on
1 September to change one by reasoning produced a warning or a breach.** Writing
the quoting rule properly cost ~750 chars and the passages paid. Giving the hall
the nav cost 832 and the passages paid again. Sending bare doors in the fallback
returned 3,444 and the passages took it back.

> **DO NOT TUNE A CONSTANT HERE BY REASONING. RUN THE PROBE.**

### Where the budget grows back

`HALL.md` is 5,751 chars — 29% of the wall — and it is the ship's meaning. It is
exactly right for *what is a spell* and largely wasted on *what did Caesar
write*. Scoping the meaning to the lane is the single largest saving available
and it is not built. THE STANDING SLIP #13, move F.

---

## 7 · THE RULES, AND WHY THEY READ AS THEY DO

Every rule in `buildAnswer` is a scar. Four are worth stating.

**QUOTE — AND ONLY FROM THE TEXT ABOVE.** This rule was corrected twice in one
day, in opposite directions. First it was a warning and nothing else, every
clause about the danger of a false quotation and none asking for a true one; the
safest way to obey it was never to quote at all, and the hall paraphrased Caesar
and Livy and quoted neither. Then it was rewritten to demand quotation, which
called a summary the thing any chatbot produces — wrong about the work this hall
does. **The hall is building a scene: the elements are the primary source and
must be exact and cited; the summary is the staging.** Livy's sentence about the
embassy to Delphi is inert until someone says why a man would play the fool at a
tyrant's court. The rule now asks for both, and forbids only one thing: letting
either wear the other's clothes.

**SAY WHAT YOU READ AND WHAT YOU DID NOT.** The coverage statement is assembled
in code from what actually happened — the rooms really opened, the works really
read — and handed to the model as something it must pass on. The hall declared
every document for its whole life because a retrieval pass can miss and never
say it missed; **retrieval keeps that promise only if the miss is declared.**
This is not a footnote on the design. It is the design, and it is the reason
retrieval was allowed to replace declaring everything.

**DO NOT SAY AMENTI LACKS SOMETHING UNLESS YOU LOOKED.** Asked whether the site
has a timeline, the hall opened two figures' rooms and answered *there is no
timeline as a standalone feature.* There is. Telling a visitor the ship lacks a
thing is a claim about the register, and may only be made with the register in
front of you.

**THE REGISTER IS THE AUTHORITY, NOT YOUR MEMORY.** What a model has on Caesar
is secondary text about him, absorbed at a remove, unattributable. What the
library has is what he wrote, in a named edition, traceable. **One can be
checked.** A remembered quotation under a real citation makes the edition a lie,
which is precisely what the citation campaign was fought to prevent — arriving
through the front door.

---

## 8 · THE SURFACE KNOWS THE ROOM IT STANDS IN

Late addition, 1 September, and the smallest change with the largest effect on
how the box reads.

The hall knew the register and not the site. Asked where the timeline is, it
correctly named Page2 and then sent the visitor to *the Harbor* — a different
repo, on a branch, behind a `fleet-nav.js` that 404s. The real door was one word
to the right of the box they had typed into.

Eleven nav labels and their addresses now sit in the prompt, read out of
`Page1.html`. Page1 has a hash router, so the tabs are real addresses —
`Page1.html#codex`, `#terminal`, `#counsel`, `#bookstore` — and `#terminal/lincoln`
opens the terminal on a figure. `linkMap` publishes the labels UPPERCASE, which
is the guard: `INTERFACE` links, *the interface was rebuilt* does not.

The answer that came back:

> *The timeline lives next door — literally the next door in the bar above you.
> INTERFACE is the label to click.*

**Two warnings in the same breath.** The nav is authored by hand and will go
stale exactly as Page2's gloss did — a probe should read it off Page1 instead
(SLIP #28). And `data-page="timeline"` on Page1 is **not** a timeline; it is
BROWSE, a roster browser, wearing a name that outlived its pane (SLIP #27).

---

## 9 · THE INSTRUMENT IS WHAT MAKES THIS AFFORDABLE

`probes/probe-hall-wall.mjs`, 30 KB, on the rung in `hall.yml`.

It does not reimplement the hall. It lifts `doorsText`, `sectionText`,
`pickRooms` and `buildAnswer` out of the SHIPPED file and runs those, and it
checks its own lift against the hall's exported `_flatten` before it says one
word about the wall. A function it cannot lift, a register it cannot read or a
catalogue of the wrong shape is **UNREAD** — it exits non-zero and reports no
margin, because not finding something means the instrument could not see.

**It has fired both ways in production**: red at 12:24 on 31 August when the
hall did not fit, green at 22:32 when it did.

### What attacking it found, and the lesson that generalises

- A **gate that could not fire** — it exited non-zero only under a flag no
  workflow passed.
- A **green light on a decoy** — a compiling fake `catalogueText` measured
  11,060 chars and PASSED.
- A **crash instead of a report** on a constant the lift did not take. Five
  times since, a new private constant has broken it, and each time it said
  UNREAD rather than passing.
- A **truncated library passing**, because it took its expected room count from
  the file it was measuring.
- And **three separate under-reports** — 160 chars, then 477, then 285 — each
  because it measured a MODEL of the prompt instead of the prompt. The last was
  the worst: call two has four shapes and it counted three, and the missing one
  was the largest.

> **A PROBE THAT CONSTRUCTS ITS OWN WORST CASE IS MEASURING ITS AUTHOR'S
> IMAGINATION.** It now builds every worst case from the real functions on the
> real registers, and probe and live agree to the character.

---

## 10 · WHAT IT COST, AND WHAT IT STOOD ON

Two working sessions. The Ask Amenti box went from refusing every question to
opening a figure's room, quoting Livy in the Spillan translation with the
edition printed beneath, declaring what it had not read, and naming the door in
the bar above.

Roughly 110 KB of source across three files — the engine, the box, the probe.

**And almost none of the value is in that 110 KB.** It works because 550 works
were already cited to findable editions with a workflow that fails the build on
an empty source. Because 191 documents already had authored sentences. Because
1,011 souls already had dates and regions. Because `find()` already searched the
registers for free. Because the probe corps already had a doctrine that says
accuse yourself first.

**That is why a surface this capable could be born in two days.** The hall is
not a new system. It is a door onto systems that were already true, and the
reason it can be trusted is that they were built to be checked.

---

## 11 · WHAT THIS BRIEF DOES NOT KNOW

- **The proxy is private.** `SYSTEM_CHARS`, the cache key, and whether tools are
  supported are unread. The wall is declared and measured against, never seen.
- **Nothing tests the quotation.** The hall is told to quote only from the text
  it was given. Nothing checks that it did. The substring guard exists as a rule
  and not yet as a probe — SLIP #13 move E, and the single largest gap here.
- **`recall` works have no file.** `library.js` declares four work modes and one
  reconstructs a passage through the AI bridge. `LIBRARY.json` drops `mode`, so
  a stored primary source and a reconstructed passage are indistinguishable in
  the aggregate register — SLIP #13 move G.
- **The nav and this brief both go stale by hand.** Whoever changes the
  navigation must change `NAV` in `amenti-hall.js`, and whoever changes the
  budgets must re-run the probe and correct §6.

---

*Written 1 Sep 2026. Every figure was taken from `probe-hall-wall` against the
live registers, not from memory — because the first measurement of this wall was
done by hand, looked authoritative, was never run against the real code, and was
wrong by 342 characters.*
