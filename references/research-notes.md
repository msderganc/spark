# Spark research notes

**Rationale catalog** for the Spark skill. At runtime, agents execute **R1–R7** in [`principles.md`](principles.md) only. This file supplies the *why*: the full P-catalog, evidence hedges, contested claims, and method pointers. **Not required every turn** — load when authoring, debugging policy, or answering “why does Spark do X?”

---

## P-catalog (P1–P16)

| # | Principle | Status | One-sentence rule |
|---|-----------|--------|-------------------|
| **P1** | Novel ∧ Appropriate | **Must** | An idea counts only if it is surprising *for this Frame* and fit to constraints—not novelty theater. *(Amabile)* |
| **P2** | Separate diverge from converge | **Must** | Do not evaluate, rank, or crown while generating; kill and score only after a protected diverge pass. *(Osborn / Guilford)* |
| **P3** | Dual pathway: flexibility + persistence | **Must** | Originality needs both surveying many categories and digging deep in a few—steer which pathway is active. *(Nijstad et al., DPCM 2010)* |
| **P4** | Generate → inhibit → refine | **Must** | After a raw burst, explicitly suppress high-probability fixation responses, then refine what remains. *(latent inhibition / fixation)* |
| **P5** | Force category expansion | **Must** | Default away from one dominant bucket; require cross-category coverage before converging. *(DPCM category fluency)* |
| **P6** | Path-of-least-resistance is the enemy | **Must** | Score and inhibit against the *obvious* completion for *this* Frame, not a generic “creative” aesthetic. *(Ward, POLR)* |
| **P7** | Constraints catalyze (Solve) | **Must** | Treat hard constraints as creative fuel—search the feasible set inventively, don’t ignore them for flash. *(Stokes)* |
| **P8** | Human owns the final filter | **Must** | Model proposes scored options; human locks; scores never auto-declare the winner. *(HITL creativity support)* |
| **P9** | Steerable dimensions > rewrite brief | **Must** | Prefer small axis deltas (and premise reframe when needed) over discarding session state. *(mixed-initiative ideation)* |
| **P10** | Conceptual combination | **Parked** | Hybridize remote or adjacent concepts on purpose when stuck in local optima. *(Geneplore / bisociation)* |
| **P11** | Abstraction ladder | **Parked** | Move up/down concreteness deliberately; don’t conflate “more abstract” with “more innovative.” *(construal-level)* |
| **P12** | Premise as editable object | **Must** | The brief is mutable (**P+**), sticky (**P0**), or snap-back (**P-**)—state which premise is active. *(framing / problem-finding)* |
| **P13** | Uniqueness ≠ Novelty | **Must** | Rarity-in-the-wild is a separate claim from surprising-for-this-Frame; hedge U=5. *(originality vs rarity)* |
| **P14** | Elegance is mode-relative | **Must** | Ideate elegance = coherent low-waste concept-fit; Solve elegance = lean solution-fit—don’t mix rubrics. *(parsimony: Ideate vs Solve)* |
| **P15** | Ground lightly, invent freely | **Parked** | Use repo/world facts when they sharpen Solve; never block ideation on research theater. *(expertise vs ideation)* |
| **P16** | Resist homogenization | **Must** | Vary categories, premises, and steers so outputs don’t collapse to one high-probability centroid. *(Doshi & Hauser 2024)* |

**Parked (P10, P11, P15)** inform optional depth via axes (**C**, **A**) and grounding commands—they are **not** runtime Must rules.

**P16 hedge (required):** homogenization evidence is largely **population / between-user** (Doshi & Hauser 2024); **within-session transfer is plausible, not proven**.

**P1** is the definitional core; it is operationalized primarily through R3 (protected diverge) and R5 (N/U/E scoring + human lock).

---

## R1–R7 → P mapping

| Runtime rule | Primary P-numbers | Role |
|--------------|-------------------|------|
| **R1** Frame & constraints | P7, P12 | Frame/confirm; constraints as fuel in Solve |
| **R2** Category diversity | P3, P5 | Flexibility via cross-category coverage |
| **R3** Diverge before evaluate | P2, P8 | Protected diverge; no auto-winner |
| **R4** Inhibit fixation / fight POLR | P4, P6 | Kill step; Novelty vs obvious completion |
| **R5** Score cautiously; human locks | P1, P8, P13, P14 | Advisory N/U/E; human `lock:N` |
| **R6** Steer & premise | P9, P12 | Panel axes; editable premise; session continuity |
| **R7** Resist homogenization | P16 | Vary cats/premise/steers (hedged) |

---

## Contested claims

Brief flags where evidence is mixed or transfer to agent sessions is uncertain:

1. **LLM originality is fragile** — top-percentile reports (e.g. Guzik et al.) vs multi-model shortfalls (e.g. Zhao et al.) likely reflect different protocols; Spark assumes originality needs process support, not raw model swagger.
2. **LLM-as-judge for creativity** — weak self-discrimination (“Creating Trumps Critiquing”; Desdevises egg-task); Spark keeps scores **advisory** and human lock final.
3. **Generate-then-select** — helps quality but selection is the bottleneck; prefer rubric-bound scoring + human lock over opaque self-pick.
4. **Diverge/converge foraging (Malaie et al.)** — strong lab priming; durability in long design sessions unclear; still supports not merging diverge and converge.
5. **Homogenization mitigators** — persona/category diversity is plausible; magnitude for product/strategy ideation less mapped than story ideation.
6. **Inhibition timing** — early fluency may benefit from loose generation; originality under fixation needs selective inhibition; Spark sequences both (diverge → inhibit → expand).

---

## Named methods (pointers)

Spark does not mandate a single ideation technique; these inform optional depth. **README appendix “Method & concepts”** summarizes each for end users:

- **SCAMPER** — substitute/combine/adapt/modify/put to other uses/eliminate/reverse operators for systematic variant generation.
- **Morphological analysis** — decompose problem dimensions and recombine attribute cells to force non-obvious combinations.
- **Cross-domain analogy** — structure-mapping from a remote source domain to break local fixation.
- **Stokes-style constraints** — paired or tightened constraints that catalyze search within a feasible set (especially Solve).

---

## Parallel subagents vs multi-round discussion

Spark’s optional **`parallel:N`** runs **single-round** subagents with **distinct personas**, then merges and dedupes before scoring.

This is **not** the Lu et al. **multi-round discussion protocol** (initiation → discussion → convergence across several turns). Parallel personas may still help **diversity** at merge time, but they are **not a substitute** for multi-round debate or true multi-agent convergence phases.

---

## Bibliography (selected)

| Authors | Year | Topic |
|---------|------|-------|
| Amabile | 1996 | Componential / novel + appropriate |
| Osborn | 1953 | Brainstorming; defer judgment |
| Guilford | 1950s | Divergent vs convergent thinking |
| Nijstad, De Dreu, Rietzschel, Baas | 2010 | Dual Pathway to Creativity Model |
| Ward | 1994 | Path of least resistance |
| Stokes | 2005 | Constraints and creativity |
| Finke, Ward, Smith | 1992 | Geneplore |
| Koestler | 1964 | Bisociation |
| Getzels & Csikszentmihalyi | 1976 | Problem-finding / framing |
| Cassotti et al. | — | Inhibitory control in ideation |
| Malaie, Spivey, Marghetis | 2024 | Diverge/converge as foraging |
| Desdevises | 2025 | LLM creativity paradox / fixation |
| Doshi & Hauser | 2024 | Generative AI homogenization |
| Lu et al. | 2024 | LLM multi-agent discussion |
| Zhao et al. | 2024/25 | LLM creativity assessment |
| Guzik, Byrge, Gilde | 2023 | Machine originality (TTCT) |
| Moreno et al. | 2014 | SCAMPER expert study |
| Daly et al. | — | Morphological analysis comparison |
| Gentner | 1983 | Structure-mapping / analogy |
