# Design spec: spark skill package

**Path:** `docs/forge/specs/2026-07-18-spark-design.md`  
**Scope tier:** medium  
**Date:** 2026-07-18

## Context

**Problem / opportunity.** Generic LLM “brainstorm” prompts yield samey, path-of-least-resistance lists: weak category coverage, no fixation inhibit, premature crowning, and no durable steer loop. **Spark** is a standalone agent skill (this repo *is* the package) that encodes a research-backed Ideate/Solve workflow with scored shortlists, steer panel, iterations/milestones, and human lock — not an app, not a Forge product feature.

**Who is affected.** Authors installing the skill in Cursor, Claude Code, or Codex; end users who trigger brainstorm/ideate/design-exploration flows.

**Sources of truth (do not contradict without a changed-decision note):**

- `.forge/memory/sketch-decisions.md` — locked behavior
- `.forge/memory/design-decisions.md` — locked principles + README paragraph rule
- `.forge/memory/solutions.md` + `solution-validation.md` — **A+Modify-amended**
- `.forge/memory/investigator.md`, `investigation.md`, `investigation-rereview.md`
- `evals/golden.md` — G1–G9 acceptance shapes

## Goals and non-goals

**Goals:**

1. Ship root skill package: `SKILL.md`, `references/*`, `README.md`, `LICENSE` (MIT), `evals/golden.md`.
2. Encode **all locked sketch behavior** (modes, Frame/confirm, internal pipeline, N/U/E rubrics, panel I…T, cats, iterations/milestones/jump, lock brief, State, conflicts, grounding, safety, when-not).
3. Runtime principles **P1–P9, P12–P14, P16** in `references/principles.md`.
4. README Method/Concepts: **one short paragraph per method/concept** (~12 Must + ~3 parked + ~4 named methods + parallel-subagents).
5. Progressive disclosure: thin procedural SKILL; depth in references.
6. Pass subjective structural goldens G1–G9.

**Non-goals (v1):**

- File-backed history; `diff:`; U/E steer axes; multi-model ensembles; fine-tuning; product UI; shipping inside Forge; automated originality scorer; claiming the model “is creative” without human evaluation.

## Constraints

**Hard:**

- Behavior SoT = sketch-decisions (chrome not re-litigated here).
- MIT license.
- Conflict short lists + full command surface in SKILL (Amendments 1–2).
- Promote State/commands to `references/state-and-commands.md` if SKILL ≳ 400 lines (Amendment 3).
- No mandatory web search; opportunistic grounding only.

**Soft:**

- Compact every-turn chrome (mitigate panel fatigue).
- Anti score-inflation guidance in scoring.md.
- Category bank expansion-friendly (not industry-cliché-only).
- Citations short in-skill; full biblio in research-notes.

## Candidate comparison snapshot

| Direction | Summary | Trade-off |
|-----------|---------|-----------|
| **A+Modify-amended (chosen)** | Thin SKILL + five core refs + research-notes; conflict/commands in SKILL; golden return template | Best progressive disclosure; SKILL length watched via promote-to-B |
| B | Split `state-and-commands.md` | Cleaner if SKILL grows; extra file by default |
| Combine | Merge steer+score+state into `controls.md` | Fewer files; worse authorability |
| Fat SKILL / mode-split / YAML bank / CONCEPTS.md | Rejected | Undertrigger, duplication, or violates README lock |

## Chosen design

**Decision:** Implement **A+Modify-amended**.

### Package layout

```
SKILL.md
references/principles.md      # Must: P1–P9, P12–P14, P16
references/pipeline.md
references/steering.md        # full legend + examples; may repeat conflict examples
references/categories.md      # mint rules + fuller numbered bank
references/scoring.md         # N/U/E + dual Elegance + anti-inflation
references/research-notes.md  # biblio, parked P10/P11/P15, contested claims
README.md                     # install + usage + Method/Concepts paragraphs
LICENSE                       # MIT
evals/golden.md               # G1–G9 (exists; refine if needed)
```

Optional later: `references/state-and-commands.md` if SKILL exceeds ~400 lines.

### Boundaries

| Artifact | Owns |
|----------|------|
| **SKILL.md** | Triggers; when-not; mode route; Frame/confirm; return-shape; compact panel; State; conflict lists; lock brief; commands incl. `parallel:2`…`5`; persona-diversity rule for parallel mode; pointers |
| **principles.md** | Runtime Must principles (do/don’t + one citation hook each) |
| **pipeline.md** | Internal stage recipes (not user-visible chrome) |
| **steering.md** | Full axis legend, examples, cats grammar, free-text |
| **categories.md** | Task-specific generation + fuller reference bank content |
| **scoring.md** | Locked rubrics + anti-inflation |
| **research-notes.md** | Biblio, parked concepts, contested claims (Guzik vs Zhao, LLM-as-judge) |
| **README.md** | Install (Cursor / Claude Code / Codex); how to use (process/iteration); modes; Method/Concepts (~19 short paragraphs) |
| **evals/golden.md** | Subjective acceptance |

### Behavior (summary — full detail in sketch-decisions)

- One skill, Ideate/Solve; shared pipeline frame → diverge → inhibit → expand → score → converge → steer.
- Scores: Novelty / Uniqueness / Elegance (dual Elegance rubrics).
- Panel: I Innovation, S Scope, A Abstraction, E Expansion, B Breadth, P Premise, C Combine, T Target (+/0/-, omit=0).
- Human lock; advisory scores; resist homogenization (P16).

### Principles (runtime Must)

P1 Novel ∧ Appropriate · P2 Separate diverge/converge · P3 Dual pathway · P4 Generate→inhibit→refine · P5 Force category expansion · P6 POLR is the enemy · P7 Constraints catalyze · P8 Human owns final filter · P9 Steerable dimensions · P12 Premise as editable object · P13 Uniqueness ≠ Novelty · P14 Elegance mode-relative · P16 Resist homogenization.

Parked (document, not Must): P10, P11, P15.

## Data / API / schema impact

- **No** database, network API, or migration.
- **Session schema (conversation State block):** mode; original ask; current premise; current `i#`; milestone titles; last steer vector; active category ids.
- **Iteration/milestone:** in-conversation only (v1); no file-backed store.
- **Category bank:** markdown numbered lists in `categories.md` (not YAML).

## Error handling and operational behavior

| Condition | Behavior |
|-----------|----------|
| Harmful/illegal ask | Refuse; redirect to legal adjacent Frame when possible |
| Command conflict | Stop; describe; ask user to fix (no silent precedence) |
| Missing item ref (`T+` without id) | Ask before re-run |
| Skip Frame confirm | One nudge; second non-confirm → generate with assumptions in State |
| Mode unclear | Recommend + confirm |
| Already-chosen implement/debug | Skip full Spark loop |
| Compaction risk | Re-emit State every turn; document session-memory limit in README |

## Test strategy

- Subjective fixtures **G1–G9** in `evals/golden.md` (structure/behavior, not identical idea text).
- Spot-check scores against rubrics (not all 5s; U=5 rare/hedged; killed look like fixation).
- No automated originality scorer in v1.
- After authoring: run goldens manually (or agent-assisted) and fix SKILL/refs until checklists pass.

## Rollout / rollback

**Rollout:**

1. Author package files per this spec.
2. Manual golden pass.
3. Users install by copying/cloning repo into agent skills path (documented in README).
4. `.forge/` is design scaffolding — not required to *use* the skill.

**Rollback:** Revert package commits; skill is file-based with no remote state.

## Assumptions

1. Host agents load `SKILL.md` frontmatter for triggering and will follow progressive-disclosure pointers.
2. Conversation memory is sufficient for iterations/milestones in typical sessions.
3. Domain-agnostic category bank can be authored without per-vertical forks in v1.
4. README Method paragraphs teach *why*; agents still need `principles.md` at runtime for compliance.

## Decision record

| Date | Decision | By |
|------|----------|-----|
| 2026-07-17..18 | Sketch behavior locked (incl. H1–H15, gap pass) | User + sketch |
| 2026-07-18 | Principles Must set + P16; park P10/11/15; README concept paragraphs | User |
| 2026-07-18 | Solution **A+Modify-amended** | User (after validation) |
| 2026-07-18 | Parallel subagents 2–5 + distinct 4–5 line personas; omit `.forge/` from publish | User |
| 2026-07-18 | **Design spec approved** | User |

## Open questions

1. Exact wording of the ~19 README Method paragraphs (author at implement; content constrained by locked principle list).
2. Exact fuller category-bank entries (author at implement; must be expansion-friendly).
3. **LOCKED:** Omit `.forge/` from published skill distribution (gitignore / package exclude) — user 2026-07-18.
4. ~~Optional multi-persona~~ → see **Parallel subagents** proposal (awaiting confirm).

## Parallel subagents — locked 2026-07-18

Optional **2–5** same-host parallel subagents on shortlist-regenerate turns.

| Item | Locked rule |
|------|-------------|
| Default | **Off** (`parallel:0` / omit) |
| Enable | `parallel:2` … `parallel:5` |
| When | Shortlist regenerates only (after Frame confirm; after steers/`cats:`/`go`). Not jump-only / milestone-only / conflict-stop / lock |
| Personas | Parent authors **one 4–5 line persona per subagent** before dispatch. Personas are **task-specific** from the Frame. |
| **Diversity (required)** | Personas must be **sufficiently different**: distinct cognitive lenses / priorities / forbidden habits (not near-paraphrases). Parent **self-checks** before dispatch — if two personas could produce the same thought process, rewrite until pairwise distinct. Prefer orthogonal axes (e.g. constraint-hawk vs category-expander vs analogical transfer vs persistence digger vs wild-card), adapted to the Frame. |
| Dispatch | Each subagent: Frame + its persona + optional category slice → **candidates only** (no crowning, no full chrome) |
| Merge | Parent: pool → inhibit → expand check → score → shortlist 8–12 + killed + normal chrome |
| State | Note `parallel:N` and one-line persona labels |
| Degrade | No subagent API → single-agent (optional sequential persona passes); State: `parallel:requested but unsupported` |
| Out of scope | Multi-provider model ensembles still v1 out-of-scope |

Add `parallel:` to SKILL command surface (Amendment 2 extended). Document briefly in README Method (named method / parallel ideation) as one short paragraph.
