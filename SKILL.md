---
name: spark
description: |
  Brainstorm ideas for any topic/domain. Invent solutions when stuck on a problem.
  Use in design sessions to explore options before locking a direction.
  Produce scored shortlists (novelty / uniqueness / elegance), not one best guess.
  Steer and iterate (panel, milestones, jump-back).
  Trigger words: brainstorm, ideate, ideas, alternatives, options, angles, concepts,
  solutions, unblock, stuck, spark, creative, invent, riff, blue-sky, diverge,
  design exploration, product ideas, feature ideas, naming, positioning — even if
  they never say Spark.
---

# Spark

Research-backed ideation skill: scored shortlists, fixation inhibit, steer loop, human lock. **Ideas** + **Controls** every return — never Content/Chrome.

---

## When NOT to trigger

Skip the full Spark loop when the user wants to **implement, debug, review, or refine an already-chosen approach** with no ideation ask.

| Primary ask | Action |
|-------------|--------|
| Implement / fix / ship chosen design | Help directly; no shortlist |
| Mixed task | Follow primary intent; Spark only when they want options |
| "Go with #2" after prior Spark | `lock:2` if in loop; else honor choice without re-ideating |

---

## Mode: Ideate vs Solve

| Mode | Route when |
|------|------------|
| **Ideate** | Topic, domain, concepts, naming, positioning, exploration |
| **Solve** | Problem, failure, constraints, "how do we fix / unblock" |

- **Clear** → select automatically; label `Mode:` on every return.
- **Unclear** → recommend one mode, ask confirm, then continue.
- Shared pipeline; **Elegance** rubric differs by mode (see `references/scoring.md`).

---

## Frame & confirm

Establish Frame (topic/problem, audience, constraints, success) **before the first shortlist**.

| Prompt richness | Behavior |
|-----------------|----------|
| **Thin** | Ask **1–3** framing questions → propose Frame → **require confirm** |
| **Rich** (artifact + audience + constraints + success) | Propose Frame, **no questions** → **require confirm** |

Re-confirm Frame only when the ask changes materially (**P+** counts).

### Skip-confirm (H6)

Accept clear proceed signals (`yes`, `go`, `confirmed`, `proceed`). One nudge if ambiguous. **Second** non-confirm without clarification → generate with stated assumptions recorded in **State**.

---

## Before first shortlist — mandatory read

On the **first** shortlist generation (after Frame confirm or H6 skip), read:

1. `references/principles.md` — R1–R7 runtime rules
2. `references/pipeline.md` — internal stages
3. `references/scoring.md` — N/U/E rubrics
4. `references/steering.md` — steer panel
5. `references/categories.md` — active categories + bank

Pipeline is **internal** — do not print stage names in Ideas.

---

## Normative SCREEN (every shortlist return)

```
=== Ideas ===
Mode: Ideate | Solve
Frame: … (confirmed)
Iteration: i# · auto-title

Shortlist
1. Title — one line [category]  N/U/E
…
(U may be marked unverified when ground: not used)

Killed (fixation)
K1. …
K2. …

Elaborations
… (2–3; no crowned winner)

Active categories: … (6–10 task-specific only)

=== Controls ===
Milestones
m1. title → i#  (or "none")

State
mode · original ask · premise · i# · milestones · last vector
Iteration snapshot: i# | premise | cats | ids/titles/scores | killed | vector | parallel labels

Steer panel omit=0: I+/0/- S+/0/- A+/0/- E+/0/- B+/0/- P+/0/- C+/0/- T+/0/-

Commands: M:i# title | J:i#|m# | lock:N [!M] | cats:… | name:i# title | parallel:2…5 | n:N | compact: | ground:repo|none | mode: | help:cats|panel|commands
```

Field order in **Controls** is fixed. Full category bank via **`help:cats`**, not dumped into Ideas.

---

## Counts & output rules

| Element | Default |
|---------|---------|
| Shortlist | **8–12** (honor explicit counts; soft cap ~20) |
| Killed / fixation | **2–3** (`K1`, `K2`, …) |
| Elaborations | **2–3** top picks |
| Active categories | **6–10** task-specific; tag every item |
| Winner | **None** — scores advisory; human **`lock:N`** only |

**Count overrides:** `n:6` (or any 4–20) sets shortlist length for that turn. Prefer **≥10** when unconstrained.

**Compact mode:** `compact:` (or `compact:on`) — shortlist only (honor `n:` or default **6**), **1** killed, **1** elaboration, still emit full **Controls** (State / snapshot / panel / commands). `compact:off` restores defaults. Use for exec/quick sessions; goldens expect full SCREEN unless the fixture says otherwise.

Scores: **Novelty / Uniqueness / Elegance** (1–5 each). Mark **U unverified** when `ground:` not used. Do not inflate; U=5 is rare and hedged. On **naming / title-only** Frames, keep most U at **≤3** (see `references/scoring.md`).

---

## State (every return)

Compact block in Controls:

| Field | Content |
|-------|---------|
| `mode` | Ideate or Solve |
| `original ask` | User's first intent (immutable anchor) |
| `premise` | Current working brief (changes on **P+**) |
| `i#` | Current iteration id + auto-title |
| `milestones` | Pinned iterations (`M:`) |
| `last vector` | Last steer/command applied |

---

## Iteration snapshot (every shortlist turn)

Emit compact snapshot in Controls for honest **`J:`** restore:

- `i#` · auto-title
- premise
- active categories
- shortlist ids / titles / N-U-E scores
- killed list
- last steer vector
- parallel persona labels (if used)

Re-emit every shortlist turn (best-effort vs compaction).

---

## Commands

| Command | Effect |
|---------|--------|
| `mode: ideate` / `mode: solve` | Switch mode; may require Frame re-confirm |
| `M:i# title` | Pin iteration as milestone `m#` |
| `J:i#` / `J:m#` | Restore iteration or milestone snapshot |
| `lock:N` / `lock:N !M` | Exit loop; emit lock brief; auto-milestone unless `!M` |
| `cats:` | Show active categories |
| `cats:+name` / `cats:-3` / `cats:1,4,7` / `cats:reset` | Edit categories (see `references/categories.md`) |
| `name:i# title` | Rename iteration auto-title |
| `parallel:2`…`5` | Enable parallel subagents (default off; see Parallel) |
| `n:N` | Shortlist length override (4–20) for this turn |
| `compact:` / `compact:on` / `compact:off` | Compact Ideas density (see Counts); Controls stay full |
| `ground:repo` / `ground:none` | Opportunistic repo context vs none |
| `help:cats` | Full category bank |
| `help:panel` | Steer axis legend |
| `help:commands` | This command card |

**Item refs:** shortlist `1…n`, killed `K#`; `T+3`, `C+2+5`, `C-4`. Invalid ref → **ask** before re-run.

**Steer:** axis letter + `+` / `0` / `-`. Omit axis = `0`. Free-text overlay OK (`I+ focus on teachers`).

**Empty steer / all omitted:** regenerate with same vector as last turn.

---

## Conflict decision table

Do **not** silently resolve mixed commands. **Stop**, describe conflict, ask user to fix.

| OK — run | STOP — ask first |
|----------|------------------|
| Steer-only (`I+ E+`) | `J` + `lock` in same turn |
| Jump-only (`J:i2`) | `lock` + any steers |
| Milestone-only (`M:i3 title`) | Two jumps (`J:i1 J:i2`) |
| Lock-only (`lock:3`) | Same axis twice with different values (`I+ I-`) |
| Clearly sequenced (`J:i2 then I+`) | Jump + lock + steers pile-up |
| Jump + milestone (`J:i2 M:i2 title`) | `lock` + milestone of different iteration without clarifying winner |
| Free-text alone | Ambiguous multi-intent with no sequence |

---

## Lock brief (`lock:N`)

Ends steer loop. Emit:

1. **Title**
2. **One-liner**
3. **Why it fits** (Frame + premise)
4. **Scores** N/U/E
5. **Next step** — one action; do **not** implement unless asked

Auto-milestone from item title unless **`lock:N !M`**.

---

## Parallel subagents

**Default off.** Enable with `parallel:2`…`5` on regenerate turns.

1. Spawn N subagents with **4–5 line sufficiently different personas** — self-check similarity; rewrite if too alike.
2. Each produces up to **6** candidates (cap enforced).
3. Vary temperature/sampling per subagent when host allows.
4. **Merge-time dedupe** before inhibit → score → converge.
5. Label personas in Controls snapshot.

**Degrade:** if parallel unsupported → single-agent path + note in State. Single-round parallel ≠ Lu multi-round protocol (`references/research-notes.md`).

---

## Jump (`J:`)

- **`J:i#`** or **`J:m#`** restores iteration snapshot (premise, shortlist, cats, killed, vector).
- Jump-only → restore + Controls; **no** new shortlist unless user also steers or says go.
- **`J:` ≠ `P-`:** jump restores a prior iteration; **P-** snaps premise to original ask.

### Missing snapshot (compaction)

If snapshot was compacted away → **disclose approximate reconstruction** from available context. Do **not** fake fidelity. Note uncertainty in State.

---

## Grounding (`ground:`)

- **`ground:none`** (default if unset): invent freely; mark all **U unverified**.
- **`ground:repo`:** skim available repo context when it sharpens **Solve** (or Ideate about this codebase). **Do not** block on empty results.
  - If no relevant artifacts (e.g. no tests when asked about coverage): State `ground:repo empty · <what was scanned>` and treat **U as unverified** — do not fabricate file-specific claims.
  - If artifacts exist: note `ground:repo consulted` in State; U may be partially grounded where items cite real paths/patterns.
- Never require web search.

---

## Safety

- **Refuse** harmful, illegal, or clearly abusive creative asks.
- Stay expansive for legal edgy / business ideation.
- **Redirect** to a legal adjacent Frame when possible instead of flat refusal.

---

## Cross-host note

Cursor, Claude Code, and Codex may differ in skill frontmatter loading, subagent support, and temperature control. Do not assume identical behavior across hosts. Document install per host in `README.md`.

---

## References

| File | Owns |
|------|------|
| [`references/principles.md`](references/principles.md) | R1–R7 executable rules |
| [`references/pipeline.md`](references/pipeline.md) | Internal stage recipes + parallel insert |
| [`references/scoring.md`](references/scoring.md) | N/U/E rubrics, anti-inflation |
| [`references/steering.md`](references/steering.md) | Steer panel legend + examples |
| [`references/categories.md`](references/categories.md) | Active categories + reference bank + `cats:` grammar |
| [`references/research-notes.md`](references/research-notes.md) | P-catalog, bibliography, contested claims |
| [`evals/golden.md`](evals/golden.md) | Golden fixtures G1–G14 |

If this file grows past ~400 lines, promote State/commands detail to `references/state-and-commands.md`.
