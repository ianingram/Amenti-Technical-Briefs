<!--
  RECOVERED 22 AUGUST 2026 — the thirteenth.
  Written 26 July 2026 for the engineering chat, Block 2. Not in
  Amenti-Technical-Briefs, not among SOURCES.json's forty, not on the list of
  twelve in HANDOVER-22-AUGUST.md. Found by looking.

  WHAT BECAME OF IT. Nothing yet, and that is the finding. It specifies
  skinning.py's PRESETS dict and audit.pose(); neither appears in any register.
  Section 1 was verified against the deployed worker, not memory — the brief
  says so itself, which is why it is safe to read now.

  AND THE METHOD IS RETIRED. Figures are now generated from an outside source
  via prompts. Sections 2–8 — MakeHuman, painted weights, the fifteen presets,
  audit.pose(), the poses table — describe work nobody will do. Read them as a
  record of a method, not as an order list. What does NOT retire with it is
  section 1's register gap, and the Art Director's armature (head cy=116, legs
  y=396–512, shared to the decimal by 20 of 33 drawings) is the same problem in
  the new medium: a figure spec with no home, held only in a handoff.

  VERIFIED 23 AUGUST. rig_views is PRESENT in Supabase — confirmed by the first
  run of tools/db-dump.sh, which put the schema under version control. So the
  lookup path is live: the worker's hardcoded &pose=eq.standing at line 479,
  with the three-quarter fallback at 483, queries a real table on behalf of a
  pipeline that no longer exists. Phase B remains unbuilt; scenes has no pose
  column. THIS IS AN OPEN ITEM, not a closed one.

  WHAT IT HAD EARLY. Its section 1 is a register gap of exactly the familiar
  shape: rig_views holds the products of a pose and no definition of it, scenes
  holds no pose at all, the worker holds none and fetches a row baked elsewhere,
  and the only true copy — the joint rotations — lived in a container that
  wipes. A fault in the water between registers, every one reporting truthfully
  about its own island. It survived four weeks only because someone typed it
  into a handoff by hand.

  And the same separation the other twelve keep arriving at, in a fifth room:
  the pose is the description, the skinning is the drawing, the join is a named
  rotation set. Separate the faculties, make the join explicit.

  ITS COUNTS ARE OF ITS OWN DAY. One approved pose, fifteen designed, one
  somatotype path, worker lines 479 and 483. Not errors to fix.

  OPEN WHEN WRITTEN AND STILL OPEN: the solo-card stature ruling (§6.5), and the
  ground-contact ruling the first time a pose lifts a foot (§4). It asks the
  proprietor for AMENTI_DESIGN_RETURN_v1.html, which has not been supplied.

  A BRIEF IS EVIDENCE, NOT A DRAFT. Nothing below this line is altered.
-->

# AMENTI — BRIEF: WHERE POSE LIVES
**Ingram Manor LLC · 2026-07-26 · for the engineering chat, Block 2**

## HOW TO USE THIS
Attach alongside `AMENTI_SESSION_HANDOFF.md`. This brief answers one question the
handoff leaves open — *where does a pose actually come from* — and specifies the
work. Read section 3 before writing any code. Nothing here is deployed; nothing
here requires the proprietor to run anything until section 7.

---

## 1. THE FINDING

**A pose currently has no home.** Verified against the deployed worker, not memory:

| layer | what it holds | what it does NOT hold |
|---|---|---|
| **Supabase `rig_views`** | keyed `(rig_key, pose, angle_name)`; stores the *products* of a pose — contour paths, clay `png_b64`, `body_layer` | any definition of what the pose IS. `pose` is a bare string; the only value ever written is `'standing'` |
| **`scenes`** | `angle`, `shot` | **no `pose` column at all** |
| **the worker (.js)** | a hardcoded lookup: line 479 `&pose=eq.standing`, fallback line 483 to `angle_name=three-quarter`. Its own comment: *"Scenes carry no pose column yet, so day one is 'standing'."* | zero pose data — it fetches a row baked elsewhere |
| **engineering Python** | the actual joint rotations, as literals in a script | persistence — the container wipes between sessions |

So the joint angles that define the one approved pose have survived only because
they were written into the handoff by hand. **That is the gap to close.**

---

## 2. THE RULING (proposed; proprietor may override)

Follow the path the somatotypes took: **measured in code first, canonized as data
once approved.**

- **Phase A — presets in `skinning.py`.** Build Design's fifteen poses as named
  rotation sets in the module. Fast iteration, no deploy cycle, judged against
  the proprietor's eye one at a time.
- **Phase B — promote to a `poses` table** once a pose stops changing, then add
  `scenes.pose` and retire the hardcoded `'standing'` in the worker.

Do not build the table first. Poses will change shape under review, and every
change would otherwise cost a SQL round trip through the proprietor.

---

## 3. THE ONE APPROVED POSE (canonical — do not re-derive)

Named `standing`. Applied through **MakeHuman's painted weights**
(`default.mhskel` + `default_weights.mhw`), FK down the bone hierarchy, linear
blend skinning. Never hand-rolled distance fields — that method produced four
successive failures and is retired.

```
upperarm01.L / .R    about Z, ∓ 0.7 × TOTAL
upperarm02.L / .R    about Z, ∓ 0.3 × TOTAL
      TOTAL = 48.7°  — SOLVED, not chosen: binary-searched until the wrist
      lands at |x| = 1.32 world, which reproduces the approved silhouette
lowerarm01.L / .R    about Z, ∓ 8°
wrist.L / .R         about X, + 14°

relaxed digits (same skinning path)
  finger2-5, phalanges 1/2/3   12° / 16° / 10°   curling toward the palm
  finger1 (thumb), 1/2/3       22° / 14° / 10°   at its own CMC chain
```

Acceptance metrics for this pose, for regression comparison:
- visible-edge stretch (posed ÷ rest, edges > 0.02 world): **max 1.43, p99 1.13**
- thumb-carpal zone p99 edge **0.231** vs the rest mesh's own **0.237**
- wrist lands card-y **287**, |x| **1.32** world
- proprietor's verdict on the hands: *"not perfect but much improved"* — closed

---

## 4. WHAT A POSE IS, AS A DATA SHAPE

Design this once and use it for all fifteen.

```json
{
  "key": "standing",
  "label": "standing, arms at sides",
  "reads_as": "upright figure, both arms hanging",
  "rotations": [
    {"bone": "upperarm01.L", "axis": "Z", "deg": -34.1},
    {"bone": "upperarm02.L", "axis": "Z", "deg": -14.6},
    {"bone": "lowerarm01.L", "axis": "Z", "deg": -8.0},
    {"bone": "wrist.L",      "axis": "X", "deg":  14.0}
  ],
  "digits": "relaxed",
  "solved_from": {"target": "wrist_x_world", "value": 1.32},
  "ground_contact": ["foot.L", "foot.R"],
  "priority": 1
}
```

Notes on the shape:
- **`axis` is a bone-local axis name, not a world vector.** Keep it symbolic so
  the same pose survives a somatotype change.
- **`solved_from`** records poses whose angles were solved to hit a landmark
  rather than chosen. Keep it — it is why the number is 48.7 and not 45.
- **`ground_contact`** names which bones must end on GROUND y=532. Poses that
  lift a foot (walking, mounting, kneeling) break the both-soles rule and must
  declare it; the frame law expects contact, and the validator may need relaxing
  for those poses. **Flag this to the proprietor before building any such pose.**

---

## 5. THE TABLE, FOR PHASE B ONLY

```sql
create table if not exists public.poses (
  key            text primary key,
  label          text not null,
  reads_as       text not null,          -- Design's silhouette test
  rotations      jsonb not null,
  digits         text not null default 'relaxed',
  solved_from    jsonb,
  ground_contact text[] not null default '{foot.L,foot.R}',
  priority       int  not null default 100,
  approved       boolean not null default false,
  created_at     timestamptz not null default now()
);
```

Then, and only then:
```sql
alter table public.scenes add column if not exists pose text
  references public.poses(key);
```
…and the worker's hardcoded `&pose=eq.standing` becomes the scene's pose with
`'standing'` as the fallback. **One worker edit, two lines (479 and 483).** Do
not touch the worker until poses are approved and the table exists.

---

## 6. VALIDATION EVERY POSE MUST PASS (build this as `audit.pose()`)

Run before showing any pose to the proprietor. Report the numbers with the image.

1. **Skin integrity** — visible-edge stretch p99 ≤ 1.20, max ≤ 1.60. Compare to
   the rest mesh; do not judge an absolute number without its baseline. (A false
   alarm was raised last session by a metric with no baseline; the rest mesh's
   own thumb webbing runs to 0.284.)
2. **Ground law** — every bone in `ground_contact` reaches y=532 ± 2px after
   frame normalization.
3. **Self-intersection** — nearest-neighbour distance between each hand's
   vertices and the rest of the body ≥ 0.055 world. This is the check that
   caught the crushed thumb.
4. **Silhouette test** — render at 160px tall, blur 1.5px, confirm the pose still
   reads as its `reads_as` string. Design's own test; apply it honestly.
5. **Frame fit** — nothing crosses the 320×560 viewBox; crown ≤ 83 unless the
   solo-card stature ruling changes (still open).

---

## 7. WHAT TO ASK THE PROPRIETOR FOR

- **`AMENTI_DESIGN_RETURN_v1.html`** — Design's D4 carries the fifteen poses with
  their silhouette tests and priority order. Do not invent pose names; use theirs.
- **A ruling on ground contact** the first time a pose lifts a foot.
- Nothing else. No SQL, no deploys, until Phase B.

---

## 8. ORDER OF WORK

1. `skinning.py` exposes `pose(V, preset)` and a `PRESETS` dict; `standing` from
   section 3 goes in first and must reproduce the approved body exactly — verify
   against the section 3 metrics before building anything new.
2. `audit.pose()` from section 6.
3. Build Design's fifteen in their priority order, one at a time, each with its
   audit numbers and a clay render for the proprietor's eye.
4. When a pose is approved, mark it; when several are approved, write the Phase B
   SQL and the two-line worker edit as one drop with a steps `.txt`.
