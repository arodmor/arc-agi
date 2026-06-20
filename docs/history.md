# A short history of ARC-AGI (2019 → today)

*A sourced timeline of the Abstraction and Reasoning Corpus and the competitions
around it. Companion to the [hub README](../README.md); see also
[approaches](approaches.md) and the [2026 tracks](arc-agi-2-vs-3.md).*

> Re-verified **2026-06-20**. Figures and dates are linked in
> [Sources](#sources); competition details change, so re-check before reuse.

---

## 2019 — The idea

François Chollet publishes *"On the Measure of Intelligence"*
([arXiv:1911.01547](https://arxiv.org/abs/1911.01547)) and releases the
**Abstraction and Reasoning Corpus (ARC)**. The paper's central argument is that
intelligence should be measured as **skill-acquisition efficiency** on novel tasks —
not as skill at any fixed task, which can be bought with data and compute. ARC
operationalises this: each task is a few input→output grid examples plus a held-out
test input, and the evaluation tasks are novel, so memorisation buys you nothing.
From the start, ARC tasks are calibrated to be easy for humans and hard for machines.

## 2020 — First Kaggle competition

The inaugural **"Abstraction and Reasoning Challenge"** runs on Kaggle with a
**$20K** prize and **914 teams**. The winning entries top out around **20%** on the
private set, built on **brute-force program synthesis**: hand-write a domain-specific
language (DSL) of grid operations, then search for a short program that reproduces
each task's examples. This established the **program-synthesis** paradigm that would
dominate ARC for the next several years — powerful in principle, but limited by
combinatorial search blow-up and by whatever the hand-built DSL can express.

## 2022–2023 — ARCathon (Lab42)

With no large Kaggle edition running, **Lab42** keeps the benchmark alive by hosting
**ARCathon 1 (2022)** and **ARCathon 2 (2023)**, each with a **$100K** prize pool.
These editions broaden international participation and sustain incremental progress —
mostly refinements of program synthesis with augmentation and ensembling — while the
state of the art creeps upward but stays well short of human level.

## 2024 — Deep learning arrives

**ARC Prize 2024** relaunches the competition at scale: a **$1.1M** prize pool and
roughly **1,430 teams**. It is the breakthrough year. The private-eval state of the
art rises from **33% to 55.5%** over the course of the competition, propelled by two
techniques in particular:

- **Test-time training (TTT)** — fine-tuning a model on a task's *own* demonstration
  examples at inference time, pioneered for ARC by **MindsAI** starting in 2023 and
  widely adopted thereafter; and
- **Deep-learning-guided / LLM-guided program synthesis** — using neural models to
  propose candidate programs rather than searching blindly.

Results and eligibility:

- **"the ARChitects"** win first place with **53.5%**, using a test-time-training
  approach — and, crucially, **open-source** their solution, which is what made them
  prize-eligible.
- **MindsAI** post the top score of **55.5%** but **do not open-source**, and are
  therefore **ineligible** for a prize.
- The **85% Grand Prize is not claimed.**

This is also when the **ARC Prize Foundation** — co-founded in 2024 by **Mike Knoop**
and **François Chollet** — takes the steward role for the benchmark and the annual
competition. The year's findings are written up in the **ARC Prize 2024: Technical
Report** ([arXiv:2412.04604](https://arxiv.org/abs/2412.04604);
[blog](https://arcprize.org/blog/arc-prize-2024-winners-technical-report)).

## 2025 — A harder benchmark, and a tiny-model surprise

Two things define 2025:

- **ARC-AGI-2** is introduced — a redesigned benchmark explicitly built to resist
  the 2024-era recipes (TTT-heavy ensembles and large-model program search), so that
  a high score once again has to come from genuine generalisation rather than a
  well-tuned pipeline.
- The **ARC Prize 2025 Paper Award** goes to **TRM (Tiny Recursive Models)** — a
  ~7M-parameter network that *recurses* on a latent scratchpad — a striking result
  for the "small and efficient beats large and brute-forced" thesis. (Details and a
  critical reading live in
  [`recursive-reasoning-models`](https://github.com/arodmor/recursive-reasoning-models).)

The 2025 cycle is documented in the **ARC Prize 2025: Technical Report**
([arXiv:2601.10904](https://arxiv.org/abs/2601.10904)).

## 2026 — Three tracks, ~$2M

**ARC Prize 2026** runs on Kaggle with a pool of **over $2M** across three tracks —
**ARC-AGI-2** (static), **ARC-AGI-3** (interactive / agentic), and a **Paper Prize**.

Key mechanics (verified **2026-06-20**):

- **Opens** March 25, 2026 · **submission deadline** November 2, 2026 ·
  **winners announced** December 4, 2026 · **papers due** November 8, 2026.
- **Sandboxed evaluation:** no internet during Kaggle scoring (no hosted-API
  systems); solutions run self-contained under compute/time limits.
- **Open-source requirement** for prize eligibility (permissive licence; CC0 / MIT-0
  in practice), attached to a Solution Writeup within seven days of the deadline.
- **2026 is the final year ARC-AGI-2 runs as an official Kaggle competition.**
- **ARC-AGI-3** adds **milestone prizes** on June 30 and September 30, 2026 (each:
  1st $25K · 2nd $10K · 3rd $2.5K) and a public community leaderboard.

ARC-AGI-3 also resets expectations about who leads. At its March 2026 launch,
**humans solved 100%** of the environments while **frontier LLMs scored below 1%**,
and the **top preview agent (~12.6%) was a purpose-built agent, not a frontier
language model** — see [the 2026 tracks comparison](arc-agi-2-vs-3.md).

---

## Sources

- F. Chollet, *On the Measure of Intelligence* (2019) — <https://arxiv.org/abs/1911.01547>
- ARC Prize 2024: Technical Report — <https://arxiv.org/abs/2412.04604>
- ARC Prize 2024 winners & report (blog) — <https://arcprize.org/blog/arc-prize-2024-winners-technical-report>
- ARC Prize 2025: Technical Report — <https://arxiv.org/abs/2601.10904>
- ARC-AGI-3: A New Challenge for Frontier Agentic Intelligence — <https://arxiv.org/abs/2603.24621>
- ARC Prize 2026 — competition overview — <https://arcprize.org/competitions/2026>
- ARC Prize 2025 — competition details — <https://arcprize.org/competitions/2025>
- Lab42 / ARCathon — <https://lab42.global/arcathon/>

*Prose © 2026 Antonio Rodriguez-Moral, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).*
