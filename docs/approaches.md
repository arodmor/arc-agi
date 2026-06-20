# How ARC-AGI solvers have evolved

*An annotated tour of the solver families that have defined ARC-AGI, and why each
ran into the benchmark's resistance to memorisation. Companion to the
[hub README](../README.md); see also the [history](history.md) and the
[2026 tracks](arc-agi-2-vs-3.md).*

> Re-verified **2026-06-20**. This is a conceptual map of public approaches, not a
> ranking. Sources at the [bottom](#sources).

---

## The throughline

ARC is built so that *seeing more data* doesn't help: the evaluation tasks are
novel, and each has its own rule. So every successful approach has, in one way or
another, found a way to **adapt to the specific task in front of it** — search for a
program that fits *these* examples, fine-tune on *these* demonstrations, or iterate a
small model on *this* grid. The families below are roughly chronological, but they
overlap and combine in practice.

## 1. Brute-force program synthesis over a DSL (2020–)

The founding paradigm. You hand-design a **domain-specific language (DSL)** of grid
operations — recolour, translate, tile, flood-fill, find symmetry, count objects —
and then **search** for a short program in that DSL that reproduces every training
example of a task. Apply the winning program to the test input.

- **Why it works:** ARC tasks really are compositional rules, and a good DSL makes
  many of them expressible in a few operations. The 2020 Kaggle winner (~20%) was
  built this way.
- **The catch:** the search space explodes combinatorially with program length, and
  the DSL is a hard ceiling — anything it can't express, you can't find. Most of the
  field's effort went into smarter search (pruning, type constraints, priors) and
  richer DSLs.

## 2. Augmentation and ensembling (2022–2023)

Squeeze more out of synthesis solvers by **augmenting** each task (rotations,
reflections, colour permutations — transformations that preserve the rule) to expose
more structure, and by **ensembling** several solvers and voting on outputs.

- **Why it works:** augmentation multiplies the effective evidence per task;
  ensembles cover each other's blind spots.
- **The catch:** incremental. It hardens existing solvers rather than expanding what
  they can express, so progress through the ARCathon years was steady but bounded.

## 3. Test-time training (TTT) (2023–)

The pivotal idea behind the 2024 jump. Instead of a frozen model, **fine-tune at
inference time on the task's own demonstration examples** (plus augmentations), then
predict the test output. Each task gets a model briefly specialised to it.

- **Why it works:** it turns ARC's "few examples per task" from a liability into a
  training signal — exactly the skill-acquisition-efficiency the benchmark rewards.
  Pioneered for ARC by **MindsAI** (from 2023) and central to **"the ARChitects'"**
  open-source winning entry in 2024.
- **The catch:** compute-heavy (a fine-tuning run *per task*) and operationally
  fiddly — learning rates, how many augmentations, when to stop. Powerful, but not
  cheap, and not obviously "understanding."

## 4. LLM-guided program search (2024)

Use a **large language model to propose candidate programs** (or candidate outputs)
rather than searching the DSL blindly, optionally combined with TTT. The model acts
as a strong prior over "what kind of rule is this likely to be."

- **Why it works:** LLMs carry a lot of useful structure about transformations and
  can prune the search dramatically.
- **The catch:** needs large models and careful scaffolding, and — decisively for
  the competition — **the prize track is sandboxed with no internet**, so hosted-API
  LLMs are out. This pushes eligible solutions toward small, self-contained models.

## 5. Deep-learning solvers + TTT ensembles (2024–2025)

The combination that produced the **55.5%** private-eval state of the art in 2024:
neural solvers, test-time training, augmentation and ensembling stacked together.

- **Why it works:** it blends learned priors with per-task adaptation and the
  robustness of ensembles.
- **The catch:** still far from the **85%** target, and heavy — which is precisely
  why **ARC-AGI-2** was redesigned for 2025 to resist this style of pipeline.

## 6. Tiny recursive models — HRM and TRM (2025–)

A different bet: not bigger, but **iterative**. A small network **recurses** —
repeatedly refining a latent "scratchpad" and a candidate answer over many steps —
so that *test-time compute behaves like effective depth*. **HRM** (Hierarchical
Reasoning Model) introduced the idea for these puzzles; **TRM** (Tiny Recursive
Models, ~7M parameters) simplified it and won the **ARC Prize 2025 Paper Award**.

- **Why it's interesting:** it's **small, self-contained, and needs no internet or
  API** — a natural fit for the sandboxed prize rules — and it reframes "reasoning"
  as iteration rather than scale.
- **The catch:** follow-up analyses argue a good share of the headline performance
  comes from **efficiency, task-specific (puzzle-ID) conditioning, and aggressive
  test-time compute** rather than general "deep reasoning." A balanced reading
  matters here.

A fuller treatment of recursive models — mechanism, the reported numbers (always
attributed to their source), and the critical follow-up work — lives in
[`recursive-reasoning-models`](https://github.com/arodmor/recursive-reasoning-models).

---

## So where does that leave 2026?

- The static **ARC-AGI-2** track rewards approaches that generalise *and* fit the
  sandbox (no internet, compute limits) — which favours small, adaptive models and
  efficient search over giant hosted LLMs.
- The interactive **ARC-AGI-3** track is a different game entirely: not "map a grid
  to a grid" but "act in a novel world." Grid-solver lineage doesn't transfer
  directly — see [the 2026 tracks comparison](arc-agi-2-vs-3.md).

---

## Sources

- F. Chollet, *On the Measure of Intelligence* (2019) — <https://arxiv.org/abs/1911.01547>
- ARC Prize 2024: Technical Report — <https://arxiv.org/abs/2412.04604>
- ARC Prize 2025: Technical Report — <https://arxiv.org/abs/2601.10904>
- *Less is More: Recursive Reasoning with Tiny Networks* (TRM) — <https://arxiv.org/abs/2510.04871>
- *Hierarchical Reasoning Model* (HRM) — <https://arxiv.org/abs/2506.21734>
- ARC Prize — competitions index — <https://arcprize.org/competitions>

*Prose © 2026 Antonio Rodriguez-Moral, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).*
