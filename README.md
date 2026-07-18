# Spark

An agent skill for brainstorming and getting unstuck. You get a shortlist of options with scores, a few "obvious" ideas deliberately thrown out, and dials to push the next round — instead of one polished "best" answer.

---

## Quick start / Install

This repo *is* the skill. Put `SKILL.md` at the root of a folder named `spark`, with `references/` and `evals/` next to it. Hosts load skills differently; the behavior contract is the same once it's loaded.

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

Clone or copy this repo into that path. Cursor picks it up from the frontmatter in `SKILL.md`. Whether `parallel:N` works depends on your Cursor version and agent mode.

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

Claude Code reads the YAML frontmatter in `SKILL.md`. Triggers come from the `description` field.

### Codex

**Default install location:**

```text
$CODEX_HOME/skills/spark/    # usually ~/.codex/skills/spark/
├── SKILL.md
├── references/
└── evals/
```

Copy the package there (or to `~/.codex/skills/spark` if `CODEX_HOME` isn't set). Manual install is the supported path until Spark is in a registry.

**Note across hosts:** Frontmatter, subagents, and sampling settings differ. If `parallel:N` isn't available, Spark falls back to a single pass and says so in Controls.

---

## How to use

Ask the way you normally would: "brainstorm names for this," "I'm stuck on X — what are some angles," "give me alternatives." You don't have to say "Spark."

Each shortlist reply has two sections:

1. **Ideas** — the options themselves  
2. **Controls** — where you are, and how to steer the next round  

### Ideas

What's in the Ideas block:

- **Mode & Frame** — Whether it's brainstorming (Ideate) or solving a constrained problem (Solve), plus a plain restatement of what it thinks you want. Read this first. If it misunderstood you, fix it here before you argue with the list.
- **Round label** — Something like `i3` so you know which pass you're on. Useful when you want to jump back later.
- **Shortlist** — Usually 8–12 options. Each has a title, one-line pitch, a category tag, and three scores (Novelty, Uniqueness, Elegance — see below). Nothing is crowned the winner.
- **Killed ideas** — Two or three answers Spark threw out on purpose because they're the first, laziest things anyone would say. Useful as a reality check that the list isn't all filler.
- **Elaborations** — A bit more detail on two or three strong picks so you don't have to dig.
- **Active categories** — The buckets it's trying to cover (for example pricing, onboarding, positioning). If everything piles into one bucket, you'll see it here.

### Controls

What's in the Controls block:

- **Milestones** — Rounds you pinned so you can return to them.
- **State** — A short status line: mode, your original ask, the current working brief (it can change if you reframe), which round you're on, and the last steer you sent.
- **Steer panel** — Eight letter dials for the next round. Each letter is defined under [Steer axes](#steer-axes) below.
- **Commands** — Typed actions: jump back, lock a pick, change length, and so on. Full list under [Commands](#commands).

On the first turn, Spark usually confirms the Frame (topic, who it's for, constraints, what "good" looks like) before generating — unless you already spelled all that out.

When one option is good enough, lock it: `lock:2` (use the real number). That ends the loop and returns a short write-up. Want a shorter list? `compact:` or `n:6`.

### Steer axes

You can talk normally — "make these weirder," "fewer ideas, go deeper," "go back to what I originally asked" — and Spark will map that onto the panel. Or type the shorthand yourself.

Each dial is one letter:

| Letter | Means | `+` | `-` |
|--------|--------|-----|-----|
| **I** | Innovation | More surprising / less expected | More conventional / safer |
| **S** | Scope | Broader | Narrower |
| **A** | Abstraction | More abstract / conceptual | More concrete / literal |
| **E** | Expansion | Ban the category that's dominating the list | Lean into what's already working |
| **B** | Breadth | Cover more categories | Go deeper on fewer |
| **P** | Premise | Reframe the working brief | Snap back to your original ask |
| **C** | Combine | Merge two options (use their numbers) | Split one option into variants (use its number) |
| **T** | Target | Deepen one option (use its number) | Reshuffle the whole shortlist |

Leave a letter out and that dial stays put (same as `0`). You can combine letters in one message: `I+ B+` = "more innovative, and spread across more categories."

An empty steer (or all letters omitted) regenerates with the same settings as last time.

Details that trip people up:

- **C** and **T** need numbers: `T+3` deepens idea 3; `C+2+5` merges 2 and 5; `C-4` splits idea 4.
- **P−** is not the same as **J:**. `P-` resets the brief to your original ask but stays on this round. `J:i2` restores round 2's whole shortlist.
- **I** (the dial) is not the same as the **Novelty** score on each idea. `I+` nudges generation; Novelty grades the result.

Full legend with more examples: [`references/steering.md`](references/steering.md).

### Scores

Each shortlist item has three 1–5 scores:

- **Novelty** — How far this is from the obvious first answer to *your* ask.
- **Uniqueness** — How rare it seems. Marked unverified unless you use `ground:repo`, because by default nothing is checked against outside sources.
- **Elegance** — How cleanly it fits the brief without extra junk. The bar is a bit different in Ideate vs Solve.

Scores are for comparison only. You pick with `lock:N` — Spark won't declare a winner for you.

### Commands

Type these alone or together. If two commands conflict (for example jump *and* lock in one message), Spark stops and asks instead of guessing.

| Command | What it does |
|---------|--------------|
| `mode: ideate` / `mode: solve` | Switch between open brainstorming and constrained problem-solving |
| `M:i3 cooking-v1` | Pin round `i3` as a milestone named `cooking-v1` |
| `J:i2` / `J:m1` | Jump back to a past round or milestone (restores that shortlist) |
| `lock:2` / `lock:2 !M` | Lock idea #2 and end with a short brief (`!M` skips auto-milestone) |
| `cats:` / `cats:+name` / `cats:-3` / `cats:reset` | Show or edit the category buckets |
| `name:i3 better-title` | Rename a round's auto title |
| `parallel:2`…`5` | Run 2–5 idea-generating personas and merge (off by default; needs host subagents) |
| `n:6` | Ask for a shortlist of length 6 this turn |
| `compact:` | Shorter Ideas block; Controls stay full |
| `ground:repo` / `ground:none` | Skim this repo for context, or invent freely with no lookups |
| `help:cats` / `help:panel` / `help:commands` | Print the category bank, steer legend, or command list |

Conflict rules and the full procedure live in [`SKILL.md`](SKILL.md).

---

## Modes: Ideate vs Solve

| Mode | Use when |
|------|----------|
| **Ideate** | You're exploring — naming, positioning, "what could this be" |
| **Solve** | You're stuck on a real problem with real constraints |

Spark picks one when it's obvious and labels `Mode:` on every Ideas block. If it's unclear, it recommends and waits for you to confirm. Same workflow either way; only the Elegance rubric changes ([`references/scoring.md`](references/scoring.md)).

---

## Appendix: Method & concepts

Background for curious readers. At runtime the agent follows **R1–R7** in [`references/principles.md`](references/principles.md). The longer principle catalog is in [`references/research-notes.md`](references/research-notes.md).

### Runtime rules (R1–R7)

**R1 — Frame & constraints.** Lock topic, audience, constraints, and success before the first shortlist. In Solve, treat hard constraints as fuel, not something to ignore for flash.

**R2 — Category diversity.** Keep 6–10 task-specific categories and tag every item so the list doesn't collapse into one bucket.

**R3 — Diverge before evaluate.** Build a pool before scoring, killing, or elaborating. Only `lock:N` ends the loop.

**R4 — Kill the obvious.** Explicitly throw out 2–3 path-of-least-resistance answers for *this* Frame. Novelty is scored against that baseline.

**R5 — Score carefully; you lock.** Novelty / Uniqueness / Elegance are advisory; Uniqueness is estimated and usually unverified; the human decides.

**R6 — Steer & keep history.** Use the eight dials, reframe with Premise when needed, and keep rounds / milestones / jump-back so you don't throw away the session.

**R7 — Don't homogenize.** Change categories, premises, and steers across rounds so you don't get the same fluent centroid every time (evidence here is mostly between-user; within-session transfer is plausible, not proven).

### Parked principles (P10, P11, P15)

Optional depth, not required every turn. **P10** — combine distant concepts when stuck (maps to Combine). **P11** — move up/down concreteness without confusing "more abstract" with "more innovative" (maps to Abstraction). **P15** — ground lightly when it helps Solve; don't stall ideation waiting for research (maps to `ground:`).

### Named methods

**SCAMPER** — Substitute, Combine, Adapt, Modify, Put to other uses, Eliminate, Reverse: a checklist when you want structured variants.

**Morphological analysis** — Break the problem into dimensions and recombine cells to force odd mixes.

**Cross-domain analogy** — Steal structure from another field to break local fixation.

**Stokes-style constraints** — Tighten or pair constraints so the search stays inventive inside the feasible set — especially in Solve.

**Parallel subagents (`parallel:2`…`5`)** — Off by default. Spawns N different personas (up to ~6 candidates each), merges with dedupe, then scores. Host support:

| Host | `parallel:` |
|------|-------------|
| **Cursor** | Works when Task/subagent tools are available; otherwise falls back |
| **Claude Code** | Same |
| **Codex** | Depends on config; often falls back |

Fallback: single-agent generation plus a note in Controls. Cost/latency scale roughly with N. This is one parallel round, not a multi-round debate protocol ([`references/research-notes.md`](references/research-notes.md)).

---

## Local planning memory

`.forge/` is local authoring/planning scratch and is gitignored. Don't copy it when you install the skill.

---

## Further reading

- Eval fixtures: [`evals/golden.md`](evals/golden.md)
- Deep refs: [`references/`](references/) — principles, pipeline, scoring, steering, categories, research notes
