# Spark — golden prompts & expected responses

Subjective v1 fixtures. Judge on **structure and behavior**, not identical idea text.
Each case: prompt(s) → must-pass checklist → golden response shape.

---

## G1 — Ideate (rich prompt)

**Prompt**
> Brainstorm product ideas for a weekend cooking club for remote coworkers. Audience: US tech workers. Hard constraint: no live video required. Success: people actually cook the same week.

**Expect before shortlist**
- [ ] Rich prompt: **no** heavy Qs (or at most none); states proposed Frame
- [ ] Gets **confirm** before first shortlist
- [ ] `Mode: Ideate` (auto)

**After confirm (“yes” / “go”)**
- [ ] Shortlist 8–12; category tags
- [ ] Scores: Novelty / Uniqueness / Elegance (1–5) using rubrics
- [ ] 2–3 killed/fixation items
- [ ] 2–3 elaborations
- [ ] Task-specific categories + fuller reference list offered
- [ ] Steer panel (`I+/0/-` … `T+/0/-`); omit=0
- [ ] Instructions include: steer, `M:`, `J:`, `lock:N`
- [ ] State block: mode, original ask, current premise, `i#`, milestones, last vector
- [ ] Milestones section (empty ok)
- [ ] Pipeline **not** shown (internal)
- [ ] Iteration id e.g. `i1` + auto-title

**Golden shape (abbrev)**
```text
Mode: Ideate
Frame: … (confirmed)
Iteration: i1 · …

Shortlist
1. … [category]  N:_ U:_ E:_
…

Killed (fixation)
K1. …

Elaborations
…

Categories used: … | Full list: …

Milestones: (none)
State: …

Steer (omit=0): I+/0/- S+/0/- A+/0/- E+/0/- B+/0/- P+/0/- C+/0/- T+/0/-
Also: M:i# title | J:i#|m# | lock:N | cats:…
```

---

## G2 — Solve (problem)

**Prompt**
> Our onboarding completion drops 40% between invite and first project. Constraints: no new headcount, must ship in one quarter. Success: +15pp completion.

**Expect**
- [ ] `Mode: Solve` (auto — failure + constraints)
- [ ] Frame confirm before shortlist
- [ ] Same output chrome as G1
- [ ] Opportunistic grounding only if repo context exists; does not block on web search

---

## G3 — Thin prompt → framing → confirm

**Prompt**
> spark some ideas for dogs

**Expect (turn 1)**
- [ ] **1–3** framing questions aimed at what it’s making
- [ ] Does **not** emit full shortlist yet

**User**
> Pet subscription box. Buyers: new dog owners. Constraint: under $40/mo. Success: second-month retention.

**Expect (turn 2)**
- [ ] States Frame summarizing the ask
- [ ] Asks for **confirmation** before generating

**User**
> confirmed

**Expect (turn 3)**
- [ ] First shortlist + full chrome (`i1`, panel, state, lock reminder)

---

## G4 — Mode unsure → recommend + confirm

**Prompt**
> Ideas for fixing our empty states — also brainstorm wild empty-state concepts for a design exploration

**Expect**
- [ ] Does not silently pick without flagging ambiguity **OR** recommends one mode and asks confirm
- [ ] After user picks, labels `Mode:` and continues (Frame confirm still applies if not done)

---

## G5 — Steer loop

**Setup:** After G1 shortlist exists as `i1`.

**Prompt**
> I+ E+ T+3

**Expect**
- [ ] New iteration `i2` (not overwrite without history)
- [ ] Behavior reflects more innovative + ban-dominant-categories + deepen item 3
- [ ] Unspecified axes treated as `0`
- [ ] State shows last vector including I+ E+ T+3
- [ ] Full chrome again (panel, lock, milestones list)

---

## G6 — Milestone + jump

**Setup:** After G5 (`i1`, `i2`).

**Prompt**
> M:i1 cooking-club-v1

**Expect**
- [ ] Milestone listed every later turn: e.g. `m1 cooking-club-v1`
- [ ] No forced regenerate unless also steered

**Prompt**
> J:m1

**Expect**
- [ ] Restores `i1` full state (premise + shortlist)
- [ ] Jump-only → restore + panel; **no** new shortlist unless user steers/`go`
- [ ] Current `i#` reflects restored iteration

---

## G7 — Lock

**Setup:** Shortlist visible.

**Prompt**
> lock:2

**Expect**
- [ ] Stops steer loop
- [ ] Tight brief: title, one-liner, why fits, scores, next step
- [ ] Does **not** implement unless asked
- [ ] Auto-milestone from item title (unless `lock:N !M`)
- [ ] Lock was advertised in prior turn’s instruction strip

---

## G8 — Command conflict

**Prompt**
> J:i1 lock:3 I+

**Expect**
- [ ] **Stops** — does not apply silent precedence
- [ ] Describes the conflict
- [ ] Asks user to fix / choose one intent

---

## G9 — Negative: do not full-Spark

**Prompt**
> Implement the OAuth callback handler we already decided on — fix the redirect URI bug

**Expect**
- [ ] Does **not** run Ideate/Solve shortlist loop
- [ ] Helps with implementation/debug instead (or stays out of Spark mode)

---

## Scoring spot-check (any shortlist case)

Pick 2–3 items and verify scores are **plausible under rubrics** (not all 5s; killed items look like fixation). Uniqueness 5 should be rare and hedged as a claim.

---

## Fixture map (v1 minimum)

| ID | Covers |
|----|--------|
| G1 | Ideate happy path |
| G2 | Solve happy path |
| G3 | Framing + confirm |
| G5 | Steer |
| G6 | Milestone + jump |
| G7 | Lock |
| G8 | Conflict handling |

G4 and G9 recommended extras.
