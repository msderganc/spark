# Steering panel

The steer panel is a compact multi-axis control surface. Users steer with axis letters and **+** / **0** / **-** levels. **Omit an axis = 0** (no change on that dimension).

Full panel order (fixed in Controls): **I S A E B P C T**

```
Steer (omit=0): I+/0/- S+/0/- A+/0/- E+/0/- B+/0/- P+/0/- C+/0/- T+/0/-
```

Free-text overlay is OK alongside axis deltas (e.g. `I+ focus on teachers`).

---

## Axis legend

| Axis | Name | **+** | **0** | **-** |
|------|------|-------|-------|-------|
| **I** | Innovation | More innovative | Same | More conventional |
| **S** | Scope | Broader | Same | Narrower |
| **A** | Abstraction | More abstract | Same | More concrete |
| **E** | Expansion | Ban dominant categories | Same | Lean into what's working |
| **B** | Breadth | More categories | Same | Deepen fewer |
| **P** | Premise | Reframe brief | Hold current | Snap to original ask |
| **C** | Combine | Hybridize (ids) | Same | Split (id) |
| **T** | Target | Deepen one (id) | Same | Reshuffle full shortlist |

### Notes

- **I ≠ Novelty score.** **I** steers generation policy toward more or less innovative *direction*; **Novelty** is a post-hoc 1–5 score vs POLR for the Frame. Steer **I** ↔ score **Novelty** — related but not identical.
- **P+** reframes the working brief (update State premise; may require Frame re-confirm if material).
- **P0** holds the current premise.
- **P-** snaps back to the **original ask** — this is **not** the same as **`J:i#`** (restore a prior iteration snapshot).
- **C+** and **T+** require item id refs (see below).
- v1 has **no** Uniqueness or Elegance steer axes; push U/E via free-text or indirect axes (**S**, **A**, **E**, **B**).

---

## Item references

| Ref | Meaning |
|-----|---------|
| `1` … `n` | Shortlist item by id |
| `K1`, `K2`, … | Killed / fixation item |
| `T+3` | Deepen shortlist item **3** |
| `C+2+5` | Hybridize items **2** and **5** |
| `C-4` | Split item **4** into distinct concepts |

**Missing or invalid ref → ask before re-run.** Do not silently guess which item the user meant.

---

## Examples

| Input | Effect |
|-------|--------|
| `I+` | Push toward more innovative directions (vs current shortlist tone) |
| `E+ B+` | Ban dominant categories; spread across more categories |
| `P+` | Reframe the brief; update premise in State |
| `T+3` | Elaborate / deepen item 3; may reshuffle others |
| `C+2+5` | Merge concepts from items 2 and 5 into hybrid(s) |
| `S- A+` | Narrower scope, more abstract framing |
| *(empty / all omitted)* | Regenerate with same steer vector as last turn (all axes at 0) |

---

## Conflict handling

Do **not** silently resolve conflicting command sets. **Stop**, describe the conflict, and ask the user to fix.

**OK:** steer-only; jump-only; milestone-only; lock-only; clearly sequenced (`J:i2 then I+`); `J:i2 M:i2 title`; free-text alone.

**Conflict (stop):** `J` + `lock`; `lock` + steers; two jumps; same axis set twice with different values; jump + lock + steers pile-up; lock + milestone of a different iteration without clarifying which wins.

See SKILL.md conflict decision table for the full OK vs stop list.

---

## On-demand help

- **`help:panel`** — expand this legend in Controls
- **`help:commands`** — full command card in `SKILL.md` (`mode:`, `M:`, `J:`, `lock:`, `cats:`, `name:`, `parallel:`, `ground:`, `help:`)
