# Spark

Research-backed agent skill for ideation and problem-solving: scored shortlists (Novelty / Uniqueness / Elegance), fixation inhibit, steer loop, and human lock — not one best guess.

---

## Quick start / Install

Spark is a **skill package** (this repo). Copy or symlink the repo contents so `SKILL.md` sits at the root of a skill folder named `spark`. Include `references/` and `evals/` alongside it. Hosts differ in how they load frontmatter and triggers; behavior is otherwise the same contract.

### Cursor

**Project skill** (recommended for teams):

```text
.cursor/skills/spark/
├── SKILL.md
├── references/
└── evals/
```

**Personal skill** (all projects):

```text
~/.cursor/skills/spark/
```

Clone or copy this repo into that path. Cursor discovers skills from `SKILL.md` frontmatter (`name`, `description`, trigger phrases). Subagent support for `parallel:N` depends on your Cursor version and agent mode.

### Claude Code

**User skill:**

```text
~/.claude/skills/spark/
├── SKILL.md
├── references/
└── evals/
```

**Project skill** (if your setup supports it):

```text
.claude/skills/spark/
```

Claude Code loads skills from `SKILL.md` YAML frontmatter. Trigger matching uses the `description` field; keep trigger words there current.

### Codex

**Default install location:**

```text
$CODEX_HOME/skills/spark/    # usually ~/.codex/skills/spark/
├── SKILL.md
├── references/
└── evals/
```

Copy the package into `$CODEX_HOME/skills/spark` (or `~/.codex/skills/spark` when `CODEX_HOME` is unset). Codex may also install curated skills via its skill-installer; for Spark, a manual copy from this repo is the supported path until published to a registry.

**Cross-host note:** Frontmatter parsing, subagent APIs, and temperature control vary. If `parallel:N` is unsupported, Spark degrades to a single-agent path and notes that in Controls State.

---

## How to use

Trigger with brainstorm / ideate / stuck / alternatives / spark-style asks. Spark returns two zones every shortlist turn:

### Ideas

- **Mode**, **Frame**, **Iteration** (`i#`)
- **Shortlist** (8–12 items) — title, one line, `[category]`, N/U/E scores
- **Killed (fixation)** — 2–3 POLR items (`K1`, `K2`, …)
- **Elaborations** — 2–3 expanded picks; no crowned winner
- **Active categories** — 6–10 task-specific tags

### Controls

- **Milestones** — pinned iterations (`M:i# title`)
- **State** — mode, original ask, premise, iteration, milestones, last vector, iteration snapshot
- **Steer panel** — `I S A E B P C T` axes (`+` / `0` / `-`; omit = 0)
- **Commands strip** — see table below

Confirm the Frame before the first shortlist (or accept after clear proceed signals). Lock a direction with `lock:N` when ready. For a shorter Ideas block: `compact:` or `n:6`.

Design-with-hard-constraints asks are often **Solve** (lean fit rubric); pure naming/exploration is **Ideate**. If unsure, Spark recommends a mode and asks you to confirm.

### Steer examples

| Input | Effect |
|-------|--------|
| `I+` | Push toward more innovative directions |
| `E+ B+` | Ban dominant categories; spread across more |
| `I+ E+ T+3` | More innovative, ban stale buckets, deepen item 3 |
| `P+` | Reframe the working brief (updates premise) |
| `T+3` | Elaborate shortlist item 3 |
| `C+2+5` | Hybridize items 2 and 5 |

Empty steer or all axes omitted → regenerate with the same vector as last turn.

### Commands

| Command | Effect |
|---------|--------|
| `mode: ideate` / `mode: solve` | Switch mode |
| `M:i# title` | Pin iteration as milestone |
| `J:i#` / `J:m#` | Restore iteration or milestone snapshot |
| `lock:N` / `lock:N !M` | Exit loop; emit lock brief |
| `cats:` / `cats:+name` / `cats:-3` / `cats:reset` | View or edit categories |
| `name:i# title` | Rename an iteration’s auto-title |
| `parallel:2`…`5` | Parallel subagents on regenerate (default off) |
| `n:N` | Shortlist length for this turn (e.g. `n:6`) |
| `compact:` | Shorter Ideas (fewer items/elaborations); Controls stay full |
| `ground:repo` / `ground:none` | Opportunistic repo context vs none |
| `help:cats` / `help:panel` / `help:commands` | On-demand reference |

Full steer legend: [`references/steering.md`](references/steering.md). Full command and conflict rules: [`SKILL.md`](SKILL.md).

---

## Modes: Ideate vs Solve

| Mode | Route when |
|------|------------|
| **Ideate** | Topic, domain, concepts, naming, positioning, exploration |
| **Solve** | Problem, failure, constraints, "how do we fix / unblock" |

Spark picks automatically when clear and labels `Mode:` on every return. When unclear, it recommends one mode and asks you to confirm. The pipeline is shared; **Elegance** scoring uses a different rubric per mode (see [`references/scoring.md`](references/scoring.md)).

---

## Appendix: Method & concepts

Short pointers for the ideas behind Spark. Runtime agents execute **R1–R7** only ([`references/principles.md`](references/principles.md)); the full P-catalog lives in [`references/research-notes.md`](references/research-notes.md).

### Runtime rules (R1–R7)

**R1 — Frame & constraints.** Establish topic, audience, constraints, and success before the first shortlist; in Solve, treat hard constraints as creative fuel rather than obstacles to ignore.

**R2 — Category diversity.** Force 6–10 task-specific categories and tag every item so the shortlist spans buckets instead of one POLR cluster.

**R3 — Diverge before evaluate.** Generate a protected candidate pool before scoring, killing, or elaborating; scores are advisory and only `lock:N` ends the loop.

**R4 — Inhibit fixation / fight POLR.** Explicitly kill 2–3 path-of-least-resistance completions for *this* Frame; score Novelty against the obvious answer, not generic "creativity."

**R5 — Score cautiously; human locks.** N/U/E on 1–5 with anti-inflation; Uniqueness is estimated and marked unverified without grounding; human lock is final.

**R6 — Steer & premise.** Multi-axis panel plus editable premise (`P+` / `P0` / `P-`); preserve session via iterations, milestones, and `J:` jump-back.

**R7 — Resist homogenization.** Vary categories, premises, and steers across iterations so outputs do not collapse to one fluent centroid (hedged: within-session transfer is plausible, not proven).

### Parked principles (P10, P11, P15)

These inform optional depth via axes and grounding but are **not** mandatory runtime rules. **P10 (conceptual combination)** — hybridize remote concepts when stuck in local optima (maps to **C+** steers). **P11 (abstraction ladder)** — move concreteness deliberately without equating "more abstract" with "more innovative" (maps to **A** axis). **P15 (ground lightly, invent freely)** — use repo or world facts when they sharpen Solve; never block ideation on research theater (maps to `ground:repo` / `ground:none`).

### Named methods

**SCAMPER** — Substitute, Combine, Adapt, Modify, Put to other uses, Eliminate, Reverse: operator checklist for systematic variants when you want structured divergence beyond free brainstorm.

**Morphological analysis** — Decompose the problem into attribute dimensions and recombine cells to force non-obvious combinations across the full possibility space.

**Cross-domain analogy** — Structure-map from a remote source domain to break local fixation and import workable patterns under new constraints.

**Stokes-style constraints** — Paired or tightened constraints that catalyze search within the feasible set; especially useful in Solve when "remove a constraint" would only produce generic answers.

**Parallel subagents (`parallel:2`…`5`)** — Default off. When enabled, Spark spawns N sufficiently different personas (each up to ~6 candidates), merges with dedupe, then runs inhibit → score → converge. Host support:

| Host | `parallel:` |
|------|-------------|
| **Cursor** | Supported when Task/subagent tools are available; otherwise degrade |
| **Claude Code** | Supported when Task/subagent tools are available; otherwise degrade |
| **Codex** | Depends on agent/subagent config; often degrade to single-agent |

Degrade path: single-agent generation + note in Controls State. Cost and latency scale roughly linearly with N (`parallel:5` ≈ 5× generation work for one round). This is **single-round parallel diversity**, not Lu-style multi-round debate ([`references/research-notes.md`](references/research-notes.md)).

---

## Local planning memory

The `.forge/` directory is **local Forge planning memory** used during skill authoring. It is **not** part of the published skill package and is excluded via [`.gitignore`](.gitignore). Do not copy `.forge/` when installing Spark.

---

## Further reading

- **Golden eval fixtures:** [`evals/golden.md`](evals/golden.md) (G1–G14)
- **Reference docs:** [`references/`](references/) — principles, pipeline, scoring, steering, categories, research notes
