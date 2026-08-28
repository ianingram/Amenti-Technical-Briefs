# SPEC — SURFACES.json AND THE SURFACE MANIFEST
### Ingram Manor LLC · 28 August 2026 · the shape, before anything is built

Companion to BRIEF-NOTHING-MAPS-THE-SURFACES. That brief argues the gap; this
one says what fills it.

**Two decisions were taken on 28 August and they shape everything below.**

> **A SURFACE IS A USER INTERFACE POINT** — somewhere a person acts on the
> system and it responds. Not a file, not a page, not a route.
>
> **AND IT GETS ITS OWN REGISTER.** `FLEET_MANIFEST` already carries ships,
> crew, watches, engines, satellites, doctrine and 35 drift entries. Adding
> surfaces makes it the thing everything hangs off. Separate register, separate
> probe, separate pane — the fleet's own pattern, unbroken.

---

## 1 · THE PAGE IS NOT THE SURFACE

This is the distinction that makes the register worth building.

`hall.html` is a page. **The Ask box is the surface.** The page is what the
surface sits on.

Which sounds like a quibble until you ask the questions that were actually asked
on 27 August, six times in one day:

| the question | what it is really about |
|---|---|
| does the dial fire on counsel? | the counsel INPUT |
| does memory reach the reading vault? | the vault's CHAT BOX |
| is the visit reading measuring everything? | it watches the terminal input and nothing else |
| does the lean prompt carry the recollection? | every surface that speaks through the chat core |

**A page-level list could not have answered one of them.** An
interaction-level list answers all four.

And the flagship stops being "six sections". A walk of `Page1.html` on 28 Aug
found **27 named interaction points** — inputs, buttons, a textarea — before
counting anything unnamed.

---

## 2 · WHAT THE WALK CAN FIND

Measured against the real file, not assumed:

```
  Page1.html          6 inputs/textareas · 59 buttons · 152 ids
                     36 addEventListener('click') · 7 onclick
                      6 data-page sections
  NAMED interaction points (an id AND an input/button/textarea):  27
```

The walk names things like `cdx-q`, `cnsQ`, `quiz-listen`, `modeToggle`,
`hero-cta-quiz`. Those are surfaces. It also finds `mp-prev`, `mp-next`,
`dp-reader-close` — chrome on a surface rather than surfaces themselves.

**THE WALK CANNOT TELL THOSE APART, AND MUST NOT TRY.** Same division as
`SOURCES.json`: the walk finds, the authored semantics say what a thing IS. A
walk that guessed would be confidently wrong at scale.

### It found a bug on its first run

Two elements carry `id="quiz-close"`. That is STANDING SLIP #3, discovered by
hand weeks ago — and it fell out of a walk that does not exist yet, in the first
minute of testing whether the walk was feasible.

**A register that surfaces a known bug as a side effect is a register worth
having.** It also found `'+co.id+'` — a template literal, i.e. a surface built
at runtime, which the walk should report as UNRESOLVED rather than as an id.

---

## 3 · THE RECORD

```json
{
  "id": "hall-ask",
  "name": "Ask Amenti",
  "kind": "input",
  "audience": "reader",

  "where": {
    "repo": "Amenti.live",
    "file": "hall.html",
    "element": "#aa-input",
    "url": "https://ianingram.github.io/Amenti.live/hall.html"
  },

  "engine": "AmentiHall.ask",
  "costs": ["anthropic"],

  "reaches": {
    "counted":    true,
    "memory":     false,
    "dial":       false,
    "voice":      false
  },

  "linkedFrom": ["page1#nav", "qr"],
  "note": "The hall's one interaction. Everything else on the page is a link."
}
```

### The fields, and why each exists

| field | the question it answers | walked or authored |
|---|---|---|
| `id` `name` | what to call it | authored |
| `kind` | input · button · toggle · mic · link · scan | walked, confirmed |
| **`audience`** | **reader or operator** | **authored** |
| `where` | which repo, file, element, and the URL a person arrives at | walked |
| `engine` | `Amenti.chat`? the hall? an inline fallback? nothing? | authored |
| `costs` | anthropic · gemini · both · nothing | authored |
| **`reaches`** | **the four questions that were asked six times** | walked where possible |
| `linkedFrom` | can a person GET here, and from where | walked |
| `note` | what a walk can never know | authored |

**`audience` is a FIELD, not a category.** An earlier draft split the whole
register into reader and operator sets. Wrong shape: a captain reading the
Harbor is a person at an interface, so a pane IS a surface — it simply serves a
different person. One register, one field.

### `reaches` is the point of the whole thing

Four booleans, and each was an argument on 27 August:

- **`counted`** — does `AmentiVisits` see it? Today: the terminal, and nothing
  else. `BRIEF-WHAT-AN-HOUR-COSTS` prices one surface of many and says so.
- **`memory`** — is `AmentiMemory.load` called there? Today: `tune()` only.
- **`dial`** — is `AmentiDial.place` called there? Today: the speaker toggle.
- **`voice`** — does it reach `/speak`, and therefore the Gemini half of the
  bill that `/spend` now measures?

A walk CAN check three of these honestly: grep the serving file for
`AmentiVisits`, `AmentiMemory`, `AmentiDial`. Presence is not proof it fires on
THAT surface — so a walk reports `file-references` and the semantics confirm.

---

## 4 · THE QR CODE IS A SURFACE

It is a place a person acts: they point a camera and arrive. **It is the only
interaction point that begins entirely off the system**, which makes it the most
interesting record in the register and the only one a code walk can never find.

Authored, and trackable:

```json
{ "id": "qr-hall", "kind": "scan", "audience": "reader",
  "where": { "url": "https://ianingram.github.io/Amenti.live/hall.html?via=qr" },
  "reaches": { "counted": true } }
```

**`?via=qr` is the whole mechanism.** The hall ignores an unknown parameter, so
nothing changes for a reader, and `AmentiVisits` gains one field. Every scan
becomes countable.

Use `via=` and not `qr=1`, so the same field serves a printed card, a poster, a
placard, a business card — each with its own value, each separately counted.
**Which of them brings people in is a question nothing can currently answer**,
and it is exactly the evidence a museum or in-flight licence conversation wants.

> Recorded 28 Aug: **nothing is printed yet.** This costs one line now and
> requires reprinting later. Do it before the first print run.

---

## 5 · THE STAMPS

Same reconciliation as `tools/merge.js` does for ships — claims against a
reading, disagreements stamped:

| stamp | meaning |
|---|---|
| `CONFIRMED` | authored, and the walk found it |
| `UNDECLARED` | the walk found an interaction point nobody has described |
| `ADRIFT` | described, and the walk cannot find it — renamed, or removed |
| `UNREACHABLE` | a reader surface nothing links to. **A door that does not open.** |
| `UNRESOLVED` | built at runtime; the walk sees `'+co.id+'` and not an id |

`UNDECLARED` is the one that earns its keep. `SOURCES.json` has 24 of them today
and its own note is the right attitude: *not an error — a document waiting for a
sentence.* A surface waiting for a sentence is the same thing.

---

## 6 · WHERE IT RUNS

**In Actions, beside the probes. Not in a browser.**

Two of the seven repositories are private. `Admin` and `Amenti-Workers` cannot
be walked from a page, and operator surfaces live in exactly those repos — so a
browser-side instrument could only ever map half the subject **and would report
that half as the whole**, which is the fault this register exists to fix,
rebuilt as its own solution.

`probes/probe-surfaces.mjs`, writing `SURFACES.json`, on a free rung. The five
strands run ten minutes apart and two must never share one.

---

## 7 · THE PANE

**The Surface Manifest.** Reads `SURFACES.json` and renders it — holding no list
of its own, generated at open, like every pane before it.

What it shows, in order of what somebody would actually come to it for:

1. **The count.** How many surfaces exist. Nothing in the fleet can say this
   today.
2. **The four `reaches` columns.** Which surfaces are counted, remembered,
   dialled, voiced — and which are not.
3. **`UNDECLARED` and `UNREACHABLE`.** The findings.
4. Everything else, grouped by audience.

**It is the eighteenth pane, and it is a surface, and it must appear in its own
register.** A map that omits itself is the fault it was built to catch.

---

## 8 · THE ORDER OF WORK

1. **`?via=qr`** — one line, and free only until something is printed.
2. **The semantics file.** `SURFACES.semantics.json`, authored, starting with
   the ones already known: the hall's Ask box, the terminal input, the counsel
   input, the mic, the talk buttons, the speaker toggles, the gameroom, Page2,
   the QR.
3. **The probe.** Walks the four public repos, merges, stamps, writes.
4. **The pane.** Reads it.
5. **And then the questions that started this are lookups.** *Is counsel
   measured?* becomes a field, not an argument.

---

## 9 · WHAT IS STILL NOT KNOWN

**How many surfaces there are.** Twenty-seven named interaction points in the
flagship alone, before the hall, Page2, the panes, the gameroom, the reading
vaults, and the QR. The count is the first thing the register produces and no
file in the fleet can produce it today.

**And what the walk will find that nobody remembers building.** On the evidence
of one test run — which surfaced a known duplicate id in its first minute — the
answer is: more than expected.

---

*Written 28 August 2026 from two decisions taken in conversation: a surface is a
user interface point, and it gets its own register. The walk figures in §2 are
measured against Page1.html, not estimated. Nothing is built.*
