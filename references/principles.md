# Spark executable principles (R1–R7)

These are the **runtime rules** agents must follow when running Spark. Rationale, full P-catalog (P1–P16), bibliography, and contested claims live in [`research-notes.md`](research-notes.md).

---

## R1 — Frame & constraints

**Must do**

- Establish a clear **Frame** before the first shortlist: topic/problem, audience, constraints, and success criteria.
- In **Solve** mode, treat hard constraints as creative fuel — search the feasible set inventively.
- Thin prompts: ask **1–3** framing questions, then propose Frame and **require confirm**.
- Rich prompts: skip questions, still **propose Frame and require confirm** before generating.
- Re-confirm Frame only when the ask changes materially (including **P+** premise reframes).

**Must not**

- Generate a shortlist before Frame is stated and confirmed (unless H6 skip-confirm applies after two ambiguous non-confirms).
- Ignore stated constraints to chase flash or novelty theater.

**Citation hook:** Stokes — constraints catalyze creativity; Getzels — problem-finding / framing. *(Maps: P7, P12)*

---

## R2 — Category diversity

**Must do**

- Show **6–10 task-specific active categories** in Ideas each shortlist turn.
- Tag each shortlist item with its category.
- Require cross-category coverage before converging; use **B+** / **E+** / `cats:` when one bucket dominates.
- Draw from the expansion-friendly bank in [`categories.md`](categories.md); full bank on demand via `help:cats`.

**Must not**

- Produce a shortlist that silently clusters in one dominant bucket while labeling many categories.
- Dump the full category bank into Ideas every turn.

**Citation hook:** Nijstad et al. — Dual Pathway to Creativity (flexibility via category fluency). *(Maps: P3, P5)*

---

## R3 — Diverge before evaluate / no auto-winner

**Must do**

- Run internal stages in order: diverge → inhibit → expand → score → converge (see [`pipeline.md`](pipeline.md)).
- Generate a raw candidate pool **before** scoring, killing, or elaborating.
- Present scores as **advisory**; elaborate 2–3 top picks without crowning a single winner.
- Exit only on explicit human **`lock:N`**.

**Must not**

- Evaluate, rank, or declare a winner during the diverge pass.
- Auto-select the highest-scored item as "the answer."

**Citation hook:** Osborn — defer judgment; Guilford — divergent vs convergent thinking. *(Maps: P2, P8)*

---

## R4 — Inhibit fixation / fight POLR

**Must do**

- After diverge, explicitly **inhibit** path-of-least-resistance (POLR) completions for *this* Frame.
- Surface **2–3 killed/fixation** items every shortlist turn (labeled `K1`, `K2`, …).
- Score **Novelty** against the obvious completion for *this* Frame, not generic "creativity."
- Use **I+** and **E+** when outputs feel clichéd or category-stale.

**Must not**

- Hide near-duplicates as variety.
- Treat fluency or polish as a substitute for genuine alternative categories.

**Citation hook:** Ward — path of least resistance; latent inhibition / fixation literature. *(Maps: P4, P6)*

---

## R5 — Score cautiously; human locks

**Must do**

- Score every shortlist item on **Novelty / Uniqueness / Elegance** (1–5) using rubrics in [`scoring.md`](scoring.md).
- Treat **Uniqueness** as *estimated familiarity under available context*; mark **unverified** when `ground:` was not used.
- Apply the correct **Elegance** rubric for the active mode (Ideate vs Solve).
- Reserve **U=5** for rare cases and hedge as a claim, not proof.
- On **`lock:N`**, emit the lock brief schema and stop the steer loop.

**Must not**

- Inflate scores (not everything is 4–5).
- Let N/U/E alone determine the winner.
- Present U as verified fact without grounding.

**Citation hook:** Human-in-the-loop creativity support; originality ≠ rarity. *(Maps: P8, P13, P14)*

---

## R6 — Steer & premise; don't discard session

**Must do**

- Honor the steer panel (**I S A E B P C T**; see [`steering.md`](steering.md)); **omit = 0**.
- Track **current premise** in State; distinguish **P+** reframe from **P-** snap-back to original ask.
- Preserve session via iterations (`i#`), milestones (`M:`), and **`J:`** restore — jump-back ≠ discarding history.
- Accept free-text overlay alongside axis deltas.

**Must not**

- Discard iteration state on steer unless the user explicitly starts fresh.
- Treat **P-** (snap to original ask) as equivalent to **`J:`** (restore a prior iteration).

**Citation hook:** Mixed-initiative / interactive ideation UIs; editable problem representation. *(Maps: P9, P12)*

---

## R7 — Resist homogenization

**Must do**

- Vary categories, premises, and steer vectors across iterations so outputs don't collapse to one high-probability centroid.
- When outputs feel samey, push **E+**, **P+**, `cats:`, or killed-fixation review before converging further.
- Remember: one fluent list ≠ the full creative space.

**Must not**

- Repeat the same category mix and premise unchanged across steers while expecting genuinely new territory.
- Claim homogenization resistance is proven at the within-session level.

**Citation hook:** Doshi & Hauser (2024) — LLM output homogeneity. **Required hedge:** this evidence is largely **population / between-user**; **within-session transfer is plausible, not proven**. *(Maps: P16)*

---

## P-catalog pointer

For the full principle catalog (P1–P16), parked principles (P10, P11, P15), bibliography, and Lu-vs-parallel discussion, see [`research-notes.md`](research-notes.md). **P10, P11, and P15 are not runtime Must rules** — they inform optional depth via axes and grounding, not mandatory execution.
