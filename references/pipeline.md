# Internal pipeline

Spark runs a fixed internal sequence on every shortlist generation or regeneration. The pipeline is **not shown** in Ideas — users see shortlist, killed, elaborations, and active categories only.

**Stages:** frame → diverge → inhibit → expand → score → converge → steer-loop

---

## Stage recipes

### Frame

- Route **Ideate** vs **Solve**; label `Mode:`.
- Establish Frame (topic/problem, audience, constraints, success).
- Confirm before first shortlist (rich prompt → propose Frame + confirm; thin → 1–3 framing Qs then Frame + confirm; skip-confirm rules apply).
- Output: agreed Frame stored in State.

### Diverge

- Generate a **raw candidate pool** (default 8–12; honor explicit counts; soft cap ~20).
- **No scoring, killing, or ranking yet.**
- Pull from 6–10 active categories; aim for cross-category spread.
- Optional **parallel** insert (see below) happens here on regenerate turns.

### Inhibit

- Identify path-of-least-resistance / fixation completions for *this* Frame.
- Select **2–3 killed items** (`K1`, `K2`, …) — ideas suppressed because they are too obvious, too dominant, or near-duplicates.
- Near-duplicate dedupe (required on parallel merge).

### Expand

- Ensure category coverage: fill thin buckets, apply **E+** / `cats:` bans, or **B+** breadth pressure.
- Hybridize or split when **C+** / **C-** steers apply.
- Each surviving candidate gets a category tag.

### Score

- Apply **N / U / E** rubrics (1–5 each) per [`scoring.md`](scoring.md).
- Use Ideate vs Solve **Elegance** rubric correctly.
- Mark **U unverified** when `ground:` was not used.
- Scores are **advisory** — no auto-winner.

### Converge

- Format shortlist (title + one line + scores + category tag).
- Elaborate **2–3** top picks (not a single crowned winner).
- Emit iteration snapshot (`i#`, premise, cats, ids/titles/scores, killed, last vector, parallel labels).

### Steer-loop

- Return **Ideas** then **Controls** (SCREEN contract).
- Wait for steer / `M:` / `J:` / `lock:` / `cats:` / free-text.
- On steer or `cats:` change → re-enter pipeline (usually from **diverge**, carrying Frame + premise + steer vector).
- On **`lock:N`** → emit lock brief and exit.
- On conflict → stop and ask (no silent precedence).

---

## Parallel insert (optional)

On **regenerate** turns when `parallel:N` (N = 2…5) is set:

1. Spawn N subagents with **4–5 line sufficiently different personas** (self-check + rewrite if too similar).
2. Each subagent produces up to **6 candidates** (cap enforced).
3. Vary temperature/sampling per subagent when the host allows.
4. **Merge-time dedupe** across personas before inhibit/score.
5. Degrade gracefully if parallel is unsupported (note in State).

Single-round parallel ≠ Lu multi-round discussion protocol (see `research-notes.md`).

Parallel runs **before merge** into the shared inhibit → expand → score → converge path — not as a separate user-visible stage.

---

## What not to surface

- Do not print stage names or internal reasoning in Ideas.
- Do not expose raw candidate pools beyond the formatted shortlist + killed.
- Pipeline pointers in SKILL.md and this file are for the agent, not the user-facing screen.
