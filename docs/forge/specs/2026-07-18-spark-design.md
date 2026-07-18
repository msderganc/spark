# Design spec: spark skill package

**Path:** `docs/forge/specs/2026-07-18-spark-design.md`  
**Scope tier:** medium  
**Date:** 2026-07-18  
**Amended:** 2026-07-18 (multi-model review — all suggestions accepted; see `design-review-accepted.md`)

## Context

**Problem / opportunity.** Generic LLM “brainstorm” prompts yield samey, path-of-least-resistance lists: weak category coverage, no fixation inhibit, premature crowning, and no durable steer loop. **Spark** is a standalone agent skill (this repo *is* the package) that encodes a research-backed Ideate/Solve workflow with scored shortlists, steer panel, iterations/milestones, and human lock — not an app, not a Forge product feature.

**Who is affected.** Authors installing the skill in Cursor, Claude Code, or Codex; end users who trigger brainstorm/ideate/design-exploration flows.

**Sources of truth:**

- `.forge/memory/sketch-decisions.md` — locked behavior (**H14 revised** by review acceptance)
- `.forge/memory/design-decisions.md` + **`design-review-accepted.md`** — principles R1–R7, screen layout, parallel hardening
- `.forge/memory/solutions.md` + `solution-validation.md` — **A+Modify-amended**
- `.forge/memory/investigator.md`, `investigation.md`, `investigation-rereview.md`
- `evals/golden.md` — G1–G9 + planned G10–G14

## Goals and non-goals

**Goals:**

1. Ship root skill package: `SKILL.md`, `references/*`, `README.md`, `LICENSE` (MIT), `evals/golden.md`.
2. Encode sketch behavior as amended by review (screen layout, iteration snapshots, parallel hardening).
3. Runtime **≤7 executable rules** (R1–R7) in `references/principles.md`; full P-catalog in research-notes.
4. README: quick start first; Method/Concepts as **appendix** (one short paragraph per concept).
5. Progressive disclosure; document **cross-host** frontmatter differences.
6. Pass goldens G1–G14 (G4/G9 mandatory; G10+ added by review).

**Non-goals (v1):**

- File-backed history; `diff:`; U/E steer axes; multi-provider model ensembles; fine-tuning; product UI; shipping inside Forge; automated originality scorer; claiming the model “is creative” without human evaluation.

## Constraints

**Hard:**

- MIT; omit `.forge/` from published skill.
- Conflict **decision table** + full command surface in SKILL (incl. `parallel:`, `help:`).
- Promote State/commands to `references/state-and-commands.md` if SKILL ≳ 400 lines.
- No mandatory web search; opportunistic grounding only.
- **Screen layout** mandatory (**Ideas** + fixed **Controls**).

**Soft:**

- Anti score-inflation; U as estimated familiarity + unverified when ungrounded.
- Expansion-friendly category bank; citations short in-skill.

## Candidate comparison snapshot

Unchanged: **A+Modify-amended** chosen; B = fallback if SKILL ≳ 400 lines; Combine / Fat / mode-split / YAML / CONCEPTS rejected.

## Chosen design

**Decision:** Implement **A+Modify-amended** + **review amendments** (`design-review-accepted.md`).

### Package layout

```
SKILL.md                      # procedure + SCREEN contract + conflict table + commands
references/principles.md      # R1–R7 executable rules only
references/pipeline.md
references/steering.md
references/categories.md
references/scoring.md         # N/U/E; U familiarity+unverified; dual Elegance; anti-inflation
references/research-notes.md  # P-catalog, biblio, contested claims, parallel≠Lu discussion
README.md                     # install/quickstart first; Method appendix
LICENSE
evals/golden.md               # G1–G14
.gitignore                    # excludes .forge/
```

### Screen output (normative)

```
=== Ideas ===
Mode / Frame / Iteration
Shortlist (N/U/E; U may be marked unverified)
Killed / Elaborations
Active categories only

=== Controls ===   ← always same place & field order
Milestones
State (+ iteration snapshot pointer / parallel labels)
Steer panel (omit=0)
Commands + help:cats|panel|commands
```

Full category bank: via **`help:cats`**, not dumped in Ideas every turn (**revises sketch H14**).

### Iteration snapshot + `J:`

Each shortlist turn includes compact record: `i#`, premise, active cats, shortlist ids/titles/scores, killed, last vector, parallel labels.  
`J:` exact restore if present; if compacted away → disclose approximate reconstruction.

### Parallel subagents

Default off; `parallel:2`…`5`; 4–5 line **sufficiently different** personas (self-check + rewrite); **merge-time dedupe**; **cap 6 candidates/subagent**; vary temperature when available; degrade + State note; README host support + cost/latency; single-round parallel ≠ Lu multi-round protocol (research-notes).

### Boundaries

| Artifact | Owns |
|----------|------|
| **SKILL.md** | Triggers; when-not; mode; Frame; **SCREEN contract (Ideas + Controls)**; conflict **table**; lock brief; commands; parallel rules; cross-host note; pointers |
| **principles.md** | **R1–R7** only |
| **pipeline / steering / categories / scoring** | As before + review amendments |
| **research-notes.md** | Full P-catalog, hedges, biblio, Lu vs parallel |
| **README.md** | Install + usage; Method **appendix**; parallel host/cost |
| **evals** | G1–G14 |

### Runtime rules (R1–R7)

R1 Frame & constraints · R2 Category diversity · R3 Diverge before evaluate · R4 Inhibit fixation/POLR · R5 Score cautiously / human locks · R6 Steer & premise · R7 Resist homogenization (hedged).

### Behavior (summary)

- Ideate/Solve; pipeline frame → diverge → inhibit → expand → score → converge → steer.
- Optional parallel before merge on regenerate turns.
- Scores advisory; U = familiarity estimate; human `lock:N`.
- SCREEN every return: **Ideas** then fixed **Controls**.

## Data / API / schema impact

- No DB/API.
- **State + Iteration snapshot** (above) in-conversation only.
- Category bank in `categories.md` (markdown).

## Error handling and operational behavior

| Condition | Behavior |
|-----------|----------|
| Harmful/illegal | Refuse; legal redirect |
| Command conflict | Stop; decision table; ask fix |
| Missing refs / invalid cats | Ask before re-run |
| Skip confirm ×2 | Generate with assumptions in State |
| Mode unclear | Recommend + confirm |
| Implement-already-chosen | Skip full Spark |
| `J:` missing snapshot | Disclose approximate restore |
| `parallel:` unsupported | Degrade; State note |
| Compaction | Re-emit Controls/State/snapshot every turn; README session limit |

## Test strategy

- **G1–G9** (G4, G9 mandatory) + **G10** parallel+degrade + **G11** jump/compaction + **G12** safety + **G13** ground + **G14** skip-confirm / invalid refs.
- Spot-check U unverified; merge dedupe on parallel.
- No automated originality scorer.
- Issue waves: screen/commands → pipeline/scoring → jump → parallel → polish (see `design-review-accepted.md`).

## Rollout / rollback

Author files → golden pass → install per host README. `.forge/` never published. Rollback = revert commits.

## Assumptions

1. Hosts differ in skill loading — document per host; do not assume identical frontmatter behavior.
2. Iteration snapshots in-thread are best-effort vs compaction; `J:` honesty required.
3. Domain-agnostic category bank for v1.
4. R1–R7 are what agents must execute; P-catalog is rationale.

## Decision record

| Date | Decision | By |
|------|----------|-----|
| 2026-07-17..18 | Sketch behavior locked | User + sketch |
| 2026-07-18 | Principles + README paras; A+Modify-amended; parallel personas; omit `.forge/` | User |
| 2026-07-18 | Design spec approved | User |
| 2026-07-18 | **Accept all multi-model review suggestions**; SCREEN layout for density; R1–R7; snapshot/`J:`; parallel harden; evals expand | User |
| 2026-07-18 | SCREEN zones renamed: **Ideas** + **Controls** (not Content/Chrome) | User |

## Open questions

1. Exact README appendix paragraph wording (implement).
2. Exact category-bank entries (implement).
3. ~~Omit `.forge/`~~ **LOCKED.**
4. ~~Parallel~~ **LOCKED** (+ review hardening).
