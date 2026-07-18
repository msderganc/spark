# Categories

Categories operationalize **flexibility** (R2): they force the shortlist to span multiple conceptual buckets instead of one POLR cluster.

---

## Active categories (Ideas)

Each shortlist turn shows **6–10 task-specific active categories** in the **Ideas** zone. These are minted for the current Frame — not copied verbatim from the bank below.

Rules:

- Every shortlist item is **tagged** with one active category.
- Active categories should be **mutually distinguishable** for this ask (avoid synonyms that hide one-bucket clustering).
- Regenerate or steer (**E+**, **B+**, `cats:`) when coverage is weak or one bucket dominates.

The **full reference bank** is **not** dumped into Ideas every turn. Users expand it on demand via **`help:cats`** in Controls.

---

## Reference bank (domain-agnostic)

Use as expansion prompts when minting active categories. Numbered for easy `cats:` references.

| # | Category lens | Prompt |
|---|---------------|--------|
| 1 | **Inversion** | Flip the default assumption or do the opposite |
| 2 | **Constraint flip** | Turn a limitation into the core mechanism |
| 3 | **Analogy transplant** | Import a pattern from an unrelated domain |
| 4 | **Extreme user** | Design for an edge persona (novice, power, excluded) |
| 5 | **Ritual / habit** | Embed in a repeated human ritual or habit loop |
| 6 | **Marketplace** | Two-sided dynamics, platforms, matching |
| 7 | **Tool / instrument** | A tangible tool, widget, or instrument-first angle |
| 8 | **Narrative / story** | Story-first, character arc, or mythic frame |
| 9 | **Systems / feedback** | Loops, second-order effects, unintended consequences |
| 10 | **Scarcity / abundance** | What if the resource were scarce — or infinitely abundant? |
| 11 | **Bundling / unbundling** | Combine separable pieces — or split an incumbent bundle |
| 12 | **Time-shift** | Past-era, near-future, or asynchronous timing |
| 13 | **Role swap** | Swap producer/consumer, human/machine, buyer/seller |
| 14 | **Anti-pattern** | Deliberately break an industry taboo (legal adjacent) |
| 15 | **Removal** | Solve by subtracting, not adding |
| 16 | **Scale jump** | 10× bigger or 10× smaller |
| 17 | **Sensory / embodied** | Lead with touch, sound, space, or physical sensation |
| 18 | **Gift / social signal** | Status, gifting, identity performance |

Mint 6–10 active categories by adapting these lenses to the Frame. Add task-specific names (e.g. "regulatory arbitrage" for a fintech Solve) when they improve tag clarity.

---

## `cats:` grammar

Edit active categories between turns.

| Form | Meaning |
|------|---------|
| `cats:` | Show current active category list |
| `cats:+analogy` | Add a category (free-text name OK) |
| `cats:-3` | Remove active category by list position or bank # |
| `cats:1,4,7,12` | Replace active set with bank entries **1, 4, 7, 12** (adapt names to Frame) |
| `cats:reset` | Re-mint 6–10 task-specific categories from scratch |

**Invalid `cats:` syntax or unknown bank ref → ask before re-run.**

After `cats:` changes, regenerate or steer so shortlist tags reflect the new active set.

---

## Steering interactions

| Steer | Category effect |
|-------|-----------------|
| **E+** | Ban categories that dominated the last shortlist; force replacements |
| **E-** | Lean into categories that scored well / resonated |
| **B+** | Increase category count; thinner coverage per bucket |
| **B-** | Deepen fewer categories; richer per-bucket ideas |

See [`steering.md`](steering.md) for the full panel.
