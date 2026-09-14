[Home](../README.md) · [中文](08-持续演进对照实验-Longitudinal-Comparison.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# EX-08: Longitudinal comparison of software production

Epistemic status: 【建议 / Proposal】 · Execution progress: planned, not run<br>
Primary claim: H1; subsidiary claims: H2–H5

## Research question

At equal quality and total resource constraints, can the proposed organization reduce human coordination cost per accepted feature as requirements and history accumulate, without shifting the burden to acceptance, integration, and knowledge maintenance?

## Product and arms

[Proposal] Select a small, greenfield information-management product with a real use case, including entry, querying, reporting, and role permissions. Use fictional data and simulated external interfaces. The specific product remains undecided.

- A: conventional AI-assisted development. Allow reasonable modularization, automated tests, documentation, and shared libraries, with humans coordinating requirements, implementation changes, and integration.
- B: candidate production loop. Explicit task boundaries, versioned rules and evidence, budgeted generation, independent acceptance, composition checks, and runtime feedback into knowledge; escalate under predefined conditions.

Both arms receive the same starting requirements, generator capabilities, quality gates, computational budgets, and human-time accounting. Do not handicap A by withholding established practices. Count B's specification, validator, and platform setup time. Apply tool-capability changes to both arms in the same round or report a deviation.

## Trial sequence

[Proposal] Begin with a pilot of 30 changes and 3 independent repetitions. This is a starting proposal, not an adequate statistical design by itself. Freeze final counts and the protocol before execution.

| Stage | Changes introduced | Observation focus |
|---|---|---|
| Initial | Basic entry, querying, reporting | Decomposition and acceptance preparation costs |
| Expansion | Features, shared rules, roles | Isolation of local changes |
| History | Legacy exceptions, compatibility, schema changes | Knowledge and state continuity |
| Stress | Concurrency, duplicate requests, simulated timeouts, local faults | Composition, recovery, escalation |
| Inheritance | Clear working conversations and start fresh sessions | Human restoration of hidden knowledge |

Use the same sequence in both arms. Balance execution order and record operator familiarity and learning effects between arms. Keep implementations and knowledge separate to avoid directly copying solutions between arms.

## Acceptance beyond visible tests

[Proposal] Establish checks before execution through a process separate from candidate generation. Split visible debugging from hidden acceptance sets. Record hard constraints, functional correctness, and usability separately. Use hidden checks only at planned checkpoints; do not repeatedly feed hidden failures back without recording it.

Check validators too: seed known errors to measure detection and document human adjudication of disputed outputs. When the same genuine requirement gap affects both arms, revise specifications consistently, retaining original results and revision reasons.

## Metrics and definitions

| Metric | Definition |
|---|---|
| Human coordination cost, primary | Human minutes on requirements, decomposition, rules, review, validators, integration, recovery, and knowledge maintenance divided by independently accepted features |
| Effective output | Preregistered features passing acceptance; if none pass, the cost ratio is undefined, not zero |
| Human escalation rate | Work events requiring human intervention divided by all work events; report the denominator |
| Cross-unit coordination | Cross-boundary decisions per change using a preregistered counting rule |
| Historical knowledge retention | Historical-rule checks passed after replacement or session reset divided by applicable checks |
| Validator miss rate | Known seeded errors escaping acceptance divided by evaluated known seeded errors; natural defects reported separately |
| Full cost | Setup, generation, acceptance, integration, operation, recovery, retention, and knowledge maintenance measured separately; report human time and compute spend separately and disclose conversion assumptions for aggregates |
| Quality and risk | Regressions, false rejections, permission or state violations, duplicate effects, and unknown outcomes separately counted |

Describe complexity with fixed proxies such as behavioral acceptance items, dependency edges, state categories, and historical exception counts. Lines of code cannot represent all complexity. Raw records include experiment, arm, repetition and change IDs, timestamps, inputs and versions, costs, verdicts, and human intervention reasons.

## Analysis and decision

[Proposal] First compare output, quality, and full cost at each stage. Then plot cumulative human time against complexity proxies. Report every repetition, variation, and failure, not just means. Three pilot repetitions cannot establish long-term scaling.

Before a formal run, fill in the product, final change sequence, quality gates, budgets, minimum meaningful effect, decision rules, and stopping rules. Unfilled items remain undecided; do not choose favorable thresholds after seeing results.

At equal quality, improvement by B under preregistered rules supports H1 within the tested scope. Benefits consumed by validation and integration contradict the corresponding claim. Mixed or insufficient data are inconclusive. A winning B arm does not establish every RFC; use each RFC's mechanism controls separately.

## Stopping and deliverables

[Proposal] Pause at budget exhaustion, persistent hard-constraint failure, isolation failure, or validator failure. Count recovery and human rescue. Deliver a bilingual report, protocol revision, runnable implementations, sanitized raw data, reproduction steps, and counterexamples. Current data and results: none yet.
