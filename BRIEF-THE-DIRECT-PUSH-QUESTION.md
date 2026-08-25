# BRIEF — THE DIRECT-PUSH QUESTION
### Should the assistant write to the repositories directly, and if so, how?
**Ingram Manor LLC · Amenti Fleet · 25 August 2026 · status: PROPOSED, not adopted**

---

## STATUS

**This is a proposal and a decision record — nothing here is live.** No token has
been created. No direct-push mechanism exists yet. This brief exists so the
change is decided deliberately, with its risks named, before any switch is
flipped. The captain raised the correct instinct — that a faster workflow can
carry faster mistakes — and this document is the answer to that instinct, not a
way around it.

---

## THE PROBLEM

Every change to the site today travels the same manual road: the assistant
writes a file, presents it, the captain downloads it, then uploads it through
GitHub's web UI. For a 525 KB monolith like `Page1.html`, that is slow, and it
has its own failure mode — the **stale-upload gremlin**, where re-uploading a
same-named file commits an old copy. Hours have been lost this way.

The captain's requirement is explicit: **hand-editing is not an option**, and the
download/upload loop is a tax on every session.

---

## WHAT WAS CONSIDERED, AND REJECTED

Two tempting answers were examined and set aside, each for a real reason.

### Rejected: break `Page1.html` into smaller files (a build step)
At first this looked like the "correct" fix — a 525 KB monolith assembled by CI
from parts, so a small change ships a small file. **It was rejected on the
captain's own architectural insight**, which is correct and worth recording:

> The application is *already fragmented by design* — multiple repos, six
> Cloudflare Workers, Supabase, GitHub Actions. Fragmentation is the
> architecture, not an accident. In that context, `Page1.html` being ONE
> consolidated file is a **virtue** — it is the one place a whole surface lives
> in a single graspable artifact instead of being scattered across five
> services. Breaking it up would take the one coherent thing and dissolve it
> into the fragmentation that already makes the system hard to hold in the head.

So the monolith stays whole. The problem was never that Page1 is a monolith —
the monolith is correct. The problem is **only the mechanism by which changes
reach it.** Do not fragment the one coherent artifact to solve an upload problem.

### Rejected: local git (clone / commit / push from the Mac)
The standard developer flow. Rejected because the captain's Mac is macOS 11.7 Big
Sur with no dev tooling, and hand-editing is off the table. This is the right
answer for a developer at a workstation; it is the wrong answer for this
captain's setup.

---

## THE PROPOSAL: DIRECT PUSH VIA THE GITHUB API, WITH CHECKPOINTS

The assistant commits files to a repository directly through the GitHub API,
using a **fine-grained personal access token** the captain creates. No download,
no upload, no hand-editing. The monolith stays whole; the manual step disappears.

But — and this is the heart of the brief — **speed is the danger.**

---

## THE RISK, NAMED HONESTLY

The manual loop is slow, but its slowness has been an **unplanned safety
feature.** Every upload is a checkpoint: the captain sees the file, chooses to
commit it, and there is a beat in which a mistake can be caught. Direct push
removes those beats. A wrong edit can reach the live flagship in one motion, with
no pause. **Faster iteration means faster mistakes**, and on `Page1.html` — the
525 KB file that runs the whole front door — a bad push has a real blast radius.

The manual method has served the entire history of the project. "Slow, but it has
never lost me the flagship" is a legitimate thing to weigh. The nervousness is
correct data, not an obstacle.

**The key realisation:** the manual upload conflated two different things — the
*checkpoint* (valuable) and the *hand-labour* (waste). The goal is to keep the
first and drop the second. Not "fast instead of safe" — **fast AND checkpointed.**

---

## THE SAFETY RAILS (non-negotiable for adoption)

Any direct-push mechanism MUST preserve a checkpoint. The following are the rails,
strongest first:

1. **Branch, not `main`.** Direct pushes land on a `staging` branch. The captain
   views the live preview, and merges to `main` only when it is right. **The
   flagship never changes without an explicit human merge.** A bad push literally
   cannot reach the live site unattended. This is the strongest rail.

2. **Diff-then-approve.** For any push, the assistant first states exactly what is
   changing — the file, the specific edit, the reason — and the commit does not
   happen until the captain says push. This preserves the catch-a-mistake beat
   while removing the download/upload labour.

3. **Every push is a commit — every mistake is one-click reversible.** Git history
   means any bad push can be reverted instantly from the repo. This is strictly
   better than the manual flow, which offers no such history at the file level.

4. **Start small, earn trust.** Use direct push first for LOW-STAKES files — CSS,
   registers, briefs — where a mistake is trivial to fix. Keep `Page1.html` on
   the careful path until the flow has proven itself on small files. Earn
   confidence before pushing the monolith.

**Rule:** never push straight to `main` on `Page1.html` unattended. Ever.

---

## THE TOKEN — SECURITY POSTURE

The token is a real credential and is treated like one.

- **Fine-grained**, not classic.
- **Scoped to a SINGLE repository** (begin with the lowest-stakes repo, not
  `Amenti.live`, during trust-building).
- **`Contents: Read and write` ONLY.** Every other permission: No access.
- **Short expiration** (7–30 days). It must expire on its own.
- **Never stored.** It lives only in the working session; pasted per session, gone
  when the session or the token ends. A fresh one each time.
- **Revocable in one click** from Developer settings the instant anything feels
  off. The captain is always in control.

Blast radius by construction: read/write files in one repo, nothing else, for a
bounded time. That is the safe posture — a tiny, expiring, single-repo key.

---

## STAGED BUILD PLAN

Do NOT flip the whole workflow at once. Stage it, each step earning the next.

**Phase 0 — decide (this brief).** Adopt or reject the proposal. If adopt, choose
the primary rail: branch-then-merge (strongest) or diff-then-approve. No token
yet.

**Phase 1 — prove on a low-stakes file, low-stakes repo.** Create a token scoped
to a single non-flagship repo (e.g. a register or a brief repo), Contents-only,
7-day expiry. Push one trivial change. Confirm: the commit lands, the diff was
shown/approved first, the revert works. Delete the token.

**Phase 2 — CSS and registers on `Amenti.live`, to a `staging` branch.** New token
scoped to `Amenti.live`. Push CSS/register changes to `staging`, never `main`.
Captain merges. Run for a few sessions. Confirm the rhythm feels safe.

**Phase 3 — the monolith, still to `staging`.** Only once Phases 1–2 have earned
trust: push `Page1.html` itself, still to `staging`, still merged by hand. The
flagship never receives an unattended push.

**Phase 4 — review.** After a few weeks, decide whether any rail can be relaxed
(e.g. small CSS straight to `main` with diff-approval). Relax nothing until the
history justifies it.

Each phase is a gate. If a phase feels wrong, stop there — the manual road is
always still open and has never failed the ship.

---

## THE DECISION TO MAKE

1. **Adopt direct push, or keep manual?** (The captain's caution is valid; "not
   yet" is a legitimate answer.)
2. **If adopt: which primary rail** — branch-then-merge, or diff-then-approve, or
   both?
3. **Which repo and file class goes first** in Phase 1?

Until these are answered, the manual loop continues unchanged. Nothing here is
live.

---

## THE PRINCIPLE

> The tedium was never the point — the checkpoint was, even if it was never named
> as one. Keep the checkpoint; drop the tedium. And build the fast path the same
> way everything else on this ship was built: slowly, deliberately, with the
> instrument proving itself before it is trusted. A workflow that can change the
> flagship in one motion must be harder to fire by accident than the thing it
> replaces, not easier.
