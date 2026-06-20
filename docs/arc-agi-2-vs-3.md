# ARC-AGI-2 vs ARC-AGI-3 — the two 2026 tracks

*The static track and the interactive track ask for fundamentally different things.
Companion to the [hub README](../README.md); see also the [history](history.md) and
[solver approaches](approaches.md).*

> Re-verified **2026-06-20**. Dates, prizes and leaderboard numbers change —
> re-check `arcprize.org` and Kaggle before relying on any figure. Sources at the
> [bottom](#sources).

---

## At a glance

| | **ARC-AGI-2** (static) | **ARC-AGI-3** (interactive) |
|---|---|---|
| **Task shape** | Infer a rule from input→output grid examples, produce the output grid | Act in a novel, turn-based environment; no input/output pairs |
| **What's tested** | Abstraction & generalisation on a *single shot* | Exploration, world-modelling, goal-setting *over time* |
| **Instructions** | Implicit in the examples | **None** — the agent must infer the goal itself |
| **Scoring** | Two attempts per task; **85%** private-eval target | Performance across interactive environments |
| **State of play (Mar 2026)** | 2024 SoTA ~55.5%; target 85% | Humans 100%; frontier LLMs <1%; top preview agent ~12.6% |
| **2026 status** | **Final year** as an official Kaggle competition | New track; milestone prizes Jun 30 & Sep 30, 2026 |
| **Sandbox** | No internet / no hosted-API during scoring | No internet / no hosted-API during scoring |

---

## ARC-AGI-2 — the static track

This is ARC in its classic form, made harder. A task presents a few **input→output
grid pairs**; you infer the transformation and apply it to a held-out test input.
Scoring uses a **two-attempts-per-task** rule, and the bar for the Grand Prize is
**85%** on the private evaluation set, achieved **within Kaggle's efficiency
limits** (compute and time).

What makes it *ARC-AGI-2* rather than *-1*: the benchmark was redesigned in 2025 to
**resist the 2024-era recipes** — the test-time-training-heavy ensembles and
large-model program search that pushed the previous benchmark to 55.5%. The goal is
that a high score has to reflect genuine generalisation again, not a well-tuned
pipeline.

A practical wrinkle worth knowing: **2026 is the final year ARC-AGI-2 runs as an
official Kaggle competition.** The lineage of grid-solver techniques —
[program synthesis, TTT, recursive models](approaches.md) — all applies here, with
the sandbox rules (no internet, no hosted APIs) favouring **small, self-contained,
adaptive** systems over giant hosted LLMs.

## ARC-AGI-3 — the interactive track

ARC-AGI-3 changes the question. Instead of mapping a grid to a grid, an agent is
placed inside a **novel, turn-based environment with no instructions** and must
figure out, by itself, three things that static ARC never required:

- **Explore** — take actions to *gather information* about how the environment works.
- **Model** — build an internal theory of the environment's dynamics from what it
  observes.
- **Set goals** — infer what counts as success (there's no labelled objective) and
  then plan a sequence of actions toward it.

This is much closer to a person sitting down with a video game they've never seen —
poke at it, form a hypothesis, test it, figure out the win condition. It is also
where current AI is weakest.

### The launch numbers (and why they matter)

At the March 2026 launch:

- **Humans solved 100%** of the environments.
- **Frontier LLMs scored below 1%** used directly — e.g. **Gemini 3.1 Pro ~0.37%**,
  **Claude Opus 4.6 ~0.2%**.
- The **top preview agent reached ~12.6%** — and it was a **purpose-built agent, not
  a frontier language model**.

The takeaway isn't that LLMs are useless here; it's that **raw model scale does not
buy interactive competence**. The capability ARC-AGI-3 measures — efficient
exploration of an unknown world — is not what next-token pretraining optimises for,
and the early lead went to a system *designed* for the task rather than the biggest
model pointed at it.

### Prizes and structure

ARC-AGI-3 runs **milestone prizes** at checkpoints on **June 30, 2026** and
**September 30, 2026** (each: 1st $25K · 2nd $10K · 3rd $2.5K), alongside a public
**community leaderboard** intended to support harness/agent research, not just final
standings. As with every track, prize-eligible work must be **open-sourced** and runs
in the **sandbox** (no internet, no hosted-API calls).

---

## Why the distinction is the whole point

Static ARC asks: *can you abstract a rule from a few examples?* Interactive ARC asks:
*can you walk into an unknown world and figure out how it works, what you're trying
to do, and how to do it — with no one telling you?* The second is a strictly harder,
more agentic form of generalisation, and the 2026 results suggest the field is much
further from it than from the static benchmark. That gap is exactly what makes the
interactive track the more interesting frontier.

---

## Sources

- ARC Prize 2026 — competition overview — <https://arcprize.org/competitions/2026>
- ARC Prize 2026 — ARC-AGI-2 track — <https://arcprize.org/competitions/2026/arc-agi-2>
- ARC Prize 2026 — ARC-AGI-3 track — <https://arcprize.org/competitions/2026/arc-agi-3>
- ARC-AGI-3: A New Challenge for Frontier Agentic Intelligence — <https://arxiv.org/abs/2603.24621>
- ARC-AGI-3 docs / quickstart — <https://docs.arcprize.org/>
- ARC Prize 2025: Technical Report — <https://arxiv.org/abs/2601.10904>

*Prose © 2026 Antonio Rodriguez-Moral, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).*
