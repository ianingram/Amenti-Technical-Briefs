# AMENTI — BRIEF: THE UNVERSIONED STORE
**Ingram Manor LLC · 2026-08-23 · found while sorting the recovered documents**

## HOW TO USE THIS

This brief names a defect and specifies the fix. It is written from documents,
not from a reading of Supabase — **no probe has looked, and I could not look.**
Section 1 is what is known. Section 2 is what is unknown and must be read before
anything in section 6 is trusted. Nothing here requires the captain to run
anything until section 7.

---

## 1. THE FINDING

**This application is three tiers, and one of them is not under version
control.**

Amenti is not a program with a database attached. It is distributed across the
stack, and the three tiers together *are* the application:

> **Cloudflare runs it. GitHub defines it. Supabase remembers it.**
> Remove any one and there is no degraded application. There is no application.

Two of those three are legible — held as plain text, diffable, bundled
off-provider every Sunday. The third is not.

| Tier | Where its truth lives | Under version control | In the ark |
|---|---|---|---|
| **The repos** | themselves | yes, by nature | **yes** — six, weekly |
| **The Workers** | Cloudflare | yes, via `mirror.yml` | **yes** — the mirror is a repo |
| **The store** | **the Supabase console** | **no** | **no** |

The Workers row is the precedent. A Worker's only copy was with the provider,
that was recognised as a fault, and a mirror was built to close it. **The same
fault is live for the database and no mirror was built.** The lesson was learned
in one tier and not carried to the next.

### What the ark actually guarantees

The ark reports six repositories bundled, verified, off-provider. **That report
is true.** It is also not what a reader takes from it.

> **THE ARK IS NOT A BACKUP OF THE APPLICATION.**
> It is a backup of two tiers of three, and nothing says so.

An instrument reporting completely about its own island while a third of the
system sits outside its walk — at the top level this time.

### How it surfaced

Sideways, which is the tell. The recovered brief `where-pose-lives` specifies a
table `rig_views`; `rig_views` does not appear in any repository. The first
reading of that absence was that the table is gone. **That reading is not
available**, and the reason is the defect itself:

> **The repositories are not a register of Supabase.**
> A table missing from the repo and a table missing from the provider produce
> exactly the same silence, and nothing in the system can tell them apart.

§4 of the standing orders in a new place: absence read as data when the source
cannot report absence.

### The consequence that only shows up in tiers

The three tiers are **coupled by contract.** The Worker's `&pose=eq.standing` is
a query against a schema. The surfaces render shapes the database defines. The
economy's laws are enforced by RLS policies and Postgres functions, not by any
code in a repo.

When one side of a contract lives only in a console, **the contract cannot be
diffed.** A column renamed on a Tuesday breaks a Worker held in git, and no
reconcile can see it, because only one side is readable. The water between
registers again — except the water is now between tiers.

### It contradicts the first key

> **AMENTI persists, and refuses loss.** Plain text, one place, under version
> control. No fallback, because this *is* the fallback.

The store holds the ledger, the court, the scenes and the rig. It also holds the
economy's constitution — *the browser never mints; every payout is idempotent;
the ledger is the sum of every row.* **Those three laws are enforced nowhere
else.** They are not in a repo. They are policies and functions behind one
login, and they are the part of this system with no second copy.

### And the smaller consequences

| | |
|---|---|
| **No history** | No record of when a column was added, a default changed, or a policy altered. A change made in the console on a Tuesday is indistinguishable from the original design. |
| **No probe** | Nothing reads it, so nothing can report on it. Every other strand has an instrument writing a register. This tier has neither. |
| **No review** | A schema change cannot be read in a diff, discussed, or reverted. It is applied and it is done. |

### What this brief is not

It is not an argument to reduce the dependency. **A distributed application
depends on its tiers; that is what distribution means**, and portability is a
much larger conversation with far less return per hour. The claim here is
narrower and the whole of it:

> **Make the third tier as legible as the other two.**
> Same standard, same repo, same Sunday bundle.

---

## 2. WHAT IS NOT KNOWN — READ BEFORE ACTING

Do not size this work from this document. Four things are unread, and the fix
changes shape depending on the answers:

1. **What tables exist.** One stale table is a footnote. The ledger, the court,
   `scenes`, `rig_views` and the roster is an unwatched register with the
   economy inside it.
2. **Whether `rig_views` is still there.** Unknown in both directions.
3. **What still reads it.** The worker's hardcoded `&pose=eq.standing`
   (line 479, fallback 483) is in a repo and readable. Whether it resolves is
   not.
4. **What Supabase's own backup retention is on this plan.** This determines how
   urgent section 6 is, and it is a two-minute check in the dashboard.

> **This brief asserts the defect, not its extent.**
> The extent is section 5's output.

---

## 3. WHAT SOFTENS IT

Stated so the fix is not over-built:

- **The rows are not the exposure.** Supabase runs its own backups; a dropped
  table is recoverable through them. **The schema is the exposure** — the
  definitions, the policies, the functions. Those are what nobody else holds.
- **The fix is small.** A schema dump is one command and its output is a text
  file. Once it is a text file in a repo, every instrument this project already
  has applies to it for free.
- **The shape is known.** This is the Workers mirror again. There is a working
  precedent to copy rather than a pattern to invent.

---

## 4. WHAT CAN ACTUALLY BE TAKEN

The Workers mirror exists because a Worker's only copy is a deployed bundle that
has to be pulled back down from the provider. **Postgres is not in that
position.** It has had a canonical text-export tool for thirty years, and
Supabase ships a CLI on top of it. This is the easier of the two problems, not
the harder one.

### What comes out as plain text

| What | How | Notes |
|---|---|---|
| **Schema** | `pg_dump --schema-only` | Every table, column, type, default, constraint, index — as `CREATE` statements. **This is the exposure and this is the fix.** |
| **Functions** | in the schema dump | `settle_argument_pool`, `cast_argument_vote` — the economy's logic, as source. |
| **RLS policies** | in the schema dump | The rules that enforce *the browser only ever reads*. |
| **Triggers, views, sequences** | in the schema dump | |
| **Migrations** | `supabase db pull` | Writes a timestamped migration file rather than one flat dump. |
| **Edge Functions** | Supabase CLI, separate | Only if any are running. Unknown — section 5 answers it. |

### Two forms, and they are different tools

- **A flat `schema.sql`** is one file, easy to diff, easy to read. **Best for
  watching** — it is what Phase B compares against.
- **A migrations directory** is a sequence of dated changes. **Best for history**,
  and it is what lets the database be rebuilt from zero.

They are not alternatives. The flat dump is generated from the migrations. Take
both if the reading in section 5 shows enough there to warrant it.

### What is deliberately not taken

**The rows.** Data is Supabase's backup problem, it may hold user content, and
including it destroys the file's use as a diff — **every dump would differ
because somebody earned an emerald.** Schema only.

### The one real difference from the Workers mirror

`mirror.yml` runs unattended on a Cloudflare API token. A schema dump needs a
Postgres connection string, **which is a stronger credential than an API token —
it can write.** So the scheduled version in Phase B wants a read-only role, not
the service key. Five minutes of setup, and it must be done before this goes on
a rung.

---

## 5. THE FIRST STEP — READ IT

Before any instrument is designed, take one reading and write it down.

- Connect with the service credentials and list every table, view, function and
  policy.
- Record the count and the names. Nothing else.
- Note whether `rig_views` exists and whether it holds rows.

**This is a probe, not a console script.** It belongs in `probes/` with the
others and its output belongs in a register file, because a reading taken by
hand in a chat is a memory the moment the chat ends — which is the fault this
whole brief is about.

Its output sizes everything below it.

---

## 6. THE FIX, IN ORDER

**Version control first, watching second.** A dump you can restore from is worth
more than an alarm about a thing you cannot restore. Do not invert these.

### Phase A — get the schema into git

1. **Dump schema only, no data.** `supabase db dump` with the schema-only flag,
   or `pg_dump --schema-only` against the connection string. Data is excluded
   deliberately: it is Supabase's backup problem, it may hold user content, and
   it would make the file useless as a diff.
2. **Commit it as plain text** to `Amenti.live` — proposed `db/schema.sql`.
   One file, human-readable, in the repo the ark already walks.
3. **Confirm the ark picks it up.** No new work: it is a file in a bundled repo,
   so Sunday's run carries it off-provider automatically. **Verify this on the
   first Sunday rather than assuming it.** That assumption is exactly the kind
   that reports green.
4. **Check the dump for secrets before committing.** Connection strings, keys or
   role passwords in a schema dump must not enter a repo. Read the file.

At the end of Phase A the defect is closed. Everything after this is detection.

### Phase B — make it watched

5. **A probe that dumps and diffs.** Re-dump on a schedule, compare against the
   committed file, write the result to a register — proposed `SCHEMA.json`:
   table count, function count, policy count, and the diff status.
6. **Give it a rung.** The five strands run ten minutes apart and **two must
   never occupy one rung.** :07, :17, :27, :37, :47 are taken. Pick a free one
   and say so in the file.
7. **Empty glass on failure.** If the dump fails, the register says so. It does
   not report the last successful diff. A schema watch that reports clean when
   it could not connect is the Silent Signature with a new name.

### Phase C — close the loop

8. **Drift is a finding, not an error.** A diff means the console and the repo
   disagree. Per §3 the repo wins for the conversation — but for a live
   database, the *provider* is the truth and the repo is stale. Re-dump, commit,
   and record why it changed. Do not "fix" the database to match the file.
9. **Then rule on `rig_views`.** With the schema in git and read, the pose
   lookup path can be judged. Not before.

---

## 7. WHAT TO ASK THE CAPTAIN FOR

- **The Supabase service credentials**, held wherever the other secrets are
  held. Not in a chat.
- **A ruling on which repo takes `db/schema.sql`** — `Amenti.live` is proposed
  because the ark already walks it and the surfaces already read from it.
- Nothing else. No SQL, no deploys, until section 5 has been read.

---

## 8. WHAT THIS COSTS IF LEFT

Not the data — Supabase holds that. What is lost is **the definition**: the
policies that decide who may read, the functions that mint and settle, the
constraints that make a balance the sum of its rows. Those are design, they took
weeks, and they exist in one place behind one login.

And the smaller cost, which is the one that compounds: **six weeks from now
somebody reads a table's absence from a repo and concludes something about the
database.** That already happened once, in this session, and it is why this
document exists.

> **A SOURCE THAT CANNOT BE REACHED IS NOT A SOURCE.**
> It is a thing somebody remembers.

---

## 9. ONE LINE FOR THE OPEN FAULTS TABLE

Until this is done:

| # | What | Cost of leaving it |
|---|---|---|
| 6 | **The third tier is unversioned and unwatched.** Cloudflare and GitHub are held as text and bundled weekly; **Supabase is not.** No schema in any repo, no probe reads it, not in the ark. The economy's laws are policies and functions that exist behind one login. Extent unknown | **the ark is a backup of two tiers of three and does not say so.** Schema contracts cannot be diffed against the Workers that query them. Same class as the Worker found off version control in the salvage |
