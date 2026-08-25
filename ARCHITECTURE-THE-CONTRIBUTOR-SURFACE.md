# AMENTI — ARCHITECTURE: THE CONTRIBUTOR SURFACE
**Ingram Manor LLC · 24 August 2026 (rev. B) · an architecture, not a build**

This document architects one idea: **how a stranger approaching Amenti gets up
to speed and begins to help.** It is a plan to react to and hand to a builder,
not code to deploy. Nothing here is built.

> **Rev. B corrects a real error in rev. A.** Rev. A put a self-checking probe
> on the slip, importing the fleet's verify-against-reality pattern. That was
> wrong, and the correction is the governing principle of this document:
>
> **THE SLIPWAY IS SOFT. THE INSTRUMENTS LIVE AT SEA.**
>
> You do not inspect a thing while it is still on the slipway. Verification
> belongs to what is launched and running. The slip is the workbench — its
> nature is that things there are unfinished, provisional, changing. A probe
> demanding they be done would flag work-in-progress as failing: noise, not
> signal. The slip is authored and human-kept. Probes wait for launch.

---

## 1 · THE PROBLEM

The open work lives in prose (`THE-STANDING-SLIP.md`, static) and in chat
(vanishes). Neither serves a newcomer. A person approaching the project cannot
see what needs doing, judge where they could help, or tell what "done" looks
like. The backlog lives in the captain and in disappearing conversation — the
illegibility the whole project has spent a month retiring, now applied to the
work itself.

---

## 2 · WHY THE SLIP IS NOT THE FLEET

The fleet earned a probe because it is **launched infrastructure**: a schedule
that lies about itself is dangerous, so an instrument checks it against reality.
`TODO.md` rotted for the same reason — it hand-tracked whether *live* files
resolved, a claim about running things that a human should never have
maintained by hand. The lesson of `TODO.md` is not "all lists need probes." It
is **"do not hand-track what is launched."**

The slip tracks the opposite: things **not yet launched** — half-decided,
in-progress, provisional. There is no settled reality for a probe to check
against, because the truth of an in-progress move is "in progress," and that is
a judgment only the worker holds, not a state a machine can measure. A probe on
the slip would not catch lies; there are no lies yet, only unfinished things. It
would flag "unfinished" as "failing." That is why the slip is soft.

**When a move graduates — becomes live infrastructure — it earns a probe THERE,
in the fleet or wherever it launched. The probe watches the sea, never the
workbench.**

---

## 3 · THE SHAPE — authored, ranked, permission-gated

Three properties. Note what is absent: no probe, no machine-written state, no
hard rules.

**Authored and human-kept.** The moves — what they are, why, what they unblock —
are written and marked done by a person, because judgment is the right
instrument for work-in-progress. The acceptance test on each move is a **note to
that human** ("you will know it's done when…"), not a gate a machine enforces.

**Ranked by what hurts.** Each move carries how painful it is to leave undone, so
a newcomer sees the order to help in without being told.

**Permission-gated.** Each move declares who may do it. This is the one hard
distinction the slip keeps — not because a rule enforces it, but because it is
**the safety rail that lets the backlog be public.** Some work is open to help;
some is captain-only (money, legal exposure, undelegatable judgment). A stranger
must be able to see which is which.

---

## 4 · THE DATA — `slip.json`, soft by design

The standing slip becomes structured data beside its prose so a pane can render
it. Every field is authored or human-set. **None is written by a machine.**

```
{
  "id": "wire-ordnance-to-fleet",
  "title": "Wire probe-ordnance to read fleet.json",
  "why": "one-line reason it matters",
  "unblocks": "what becomes possible when it's done",
  "hurtsRank": 1,                 // lower = more painful to leave undone
  "permission": "open" | "captain-only",
  "acceptanceTest": "a NOTE to the human: how you'll know it's done",
  "state": "open" | "doing" | "done",   // a HUMAN sets this, by judgment
  "graduatesTo": null            // slipway name if it grows its own phases
}
```

`state` is set **by a person**, not a probe. That is the whole difference from
the fleet, and it is deliberate: on the workbench, the worker's judgment is the
only honest instrument. There is no `probeKey`, no `SLIP-STATE.json`, no
`probe-slip.mjs`. Those were rev. A's error.

---

## 5 · THE BUILD — one phase, small

There is no phase two. Rev. A's phase two *was* the mistake.

**`slip.json`** authored from the standing slip. **`slip.html`** — a pane in the
shape of `fleet-status.html` — renders it: moves ranked by `hurtsRank`,
acceptance tests visible as guidance, permissions marked, state shown by the
color a human set. That is the whole build. A window on the workbench, legible
to a stranger. No infrastructure, no probe, no rung.

The window is the deliverable. The slip stays soft forever; it is only ever a
window and an authored file.

---

## 6 · THE CONTRIBUTOR PATH — orient → survey → contribute

The pane is the last of three steps, the first two already built:

1. **Orient** — *what is this?* — **the hall** (`hall.html`), answering.
2. **Survey** — *what state is it in?* — **fleet-status** (`fleet-status.html`),
   showing the launched systems. (This is where instruments live — the sea.)
3. **Contribute** — *what can I do?* — **the slip pane** (`slip.html`), the
   workbench, soft.

The architecture is a **path**, not a lone pane — and it neatly embodies the
governing principle: steps 1–2 show launched, verified things; step 3 shows the
soft workbench. The newcomer walks from the running ship to the open work.

---

## 7 · THE PERMISSION MODEL — the one hard line

- **`open`** — a contributor may take this up: drafting briefs, describing
  files, writing or fixing probes and tools, proposing fixes as files the
  captain deploys.
- **`captain-only`** — undelegatable: arming crons, the `dailyplanet:`
  mechanism, the sacred frames, which deck cards are wrong. The pane shows these
  so the shape of the work is visible, marked not-for-delegation.

This is the standing slip's closing footnote promoted to a field. It is enforced
by *display and trust*, not by a probe — consistent with a soft slip. The rail
is that a stranger can *see* the boundary, not that a machine stops them at it.

---

## 8 · WHERE IT LIVES

`slip.json` and `slip.html` at **`Amenti.live` root**, beside `fleet.json`. The
prose `THE-STANDING-SLIP.md` stays in `Amenti-Technical-Briefs`. Two forms:
reasoning in the briefs, data with the ship. Kept in step by hand — and because
the slip is soft, "kept in step by hand" is not a defect here; it is the nature
of the workbench.

If ever surfaced as a Fleet-Documents pane, reading `slip.json` cross-repo is a
deliberate fetch to rule on then, not wire quietly.

---

## 9 · WHAT TO DECIDE BEFORE BUILDING

1. **Public or captain-facing first?** A "help wanted" surface is a different
   posture than a private backlog window. The permission model supports either.
2. **Does `slip.json` supersede `THE-STANDING-SLIP.md` or complement it?** Rev. B
   assumes complement (prose + data). If the prose is redundant once the data
   exists, choose that simplification deliberately.

---

## 10 · SEQUENCING — one line

Author `slip.json` from the standing slip, build `slip.html` to render it in
fleet-status's form, mark each move's state by hand — and stop there, because
the slip is the workbench and the workbench stays soft, so a stranger arriving
reads the open work ranked by what hurts and gated by what they may touch,
without a probe pretending the unfinished is broken.

> Orient at the hall. Survey at the status. Contribute at the slip.
> **The slipway is soft; the instruments live at sea.**
> Verify what has launched. Leave the workbench free to be unfinished.
