[Home](../README.md) · [中文](实验索引-Experiment-Index.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# Experiment index

[Confirmed] Source sections VII and IX describe seven prototypes. The source's “six” heading and closing count conflict with its enumeration; this index uses 01–07. [S0](../证据-Evidence/来源摘要-Source-Digest.en.md#s0)

[Open] This initial release contains research documents only. Source code, complete environments, seeds, logs, and independent reproductions for the seven prototypes were not available. “Reported” below means reported in the source, not experiments completed in this repository. Missing results are not represented as zero.

| ID and name | Original file lead | Source-reported observation | Limits and required verification | Status |
|---|---|---|---|---|
| EX-01 Self-healing unit | self_healing_unit.jsx | Generation, executed tests, failure feedback, regeneration, and version rollback were connected | Fixed tests and minimal execution isolation; recover failures and independent acceptance checks | 【不确定 / Open】Reported; awaiting reproduction |
| EX-02 Environment-driven state machines | environment_swarm.jsx | 28 units reassign according to positions and quotas | One-dimensional ordering without neighbor negotiation; check whether behavior follows direct allocation alone | 【不确定 / Open】Reported; awaiting reproduction |
| EX-03 Two-dimensional spatial field | spatial_field.jsx | Sites derive states from distance fields; damage remains local | No inter-unit dependencies; connectivity and software composition benefits untested | 【不确定 / Open】Reported; awaiting reproduction |
| EX-04 Local growth rules | growth_frontiers.jsx | Connected growth has timing competition; enclosed regions become unrecoverable | Record topology, scheduling, and reversibility; do not equate this with disease mechanisms | 【不确定 / Open】Reported; awaiting reproduction |
| EX-05 Potts model | potts_model.jsx | Boundary penalties and revisable states improve patterns; a strong target field suppresses exploration | Recover parameters and seeds; compare direct computation; no claim of arbitrary-system convergence | 【不确定 / Open】Reported; awaiting reproduction |
| EX-06 Differential adhesion | differential_adhesion.jsx | Initialization omission, single-color collapse, count-preserving identity exchange, ratio and cooling adjustments; multiple domains remained | Pixels lack persistent region identity; distinguish original models, simplified implementation, and physical analogy | 【不确定 / Open】Reported; awaiting reproduction |
| EX-07 Hierarchical promotion | hierarchical_promotion.jsx | Stable regions acquire IDs; snapshot freezing leaves gaps, followed by neighbor absorption | Can freezing and identity rules introduce new traps? Compare explicit hierarchy first | 【不确定 / Open】Reported; awaiting reproduction |
| EX-08 Longitudinal comparison | [Protocol](08-持续演进对照实验-Longitudinal-Comparison.en.md) | Not run; tests organizational benefits and the three RFCs | Select a product and freeze requirement sequences, acceptance, and budgets | 【建议 / Proposal】Planned |

## Reproducing historical prototypes

[Proposal] Supply code and permission information, dependency versions, run instructions, generator configuration, inputs, random seeds, hardware or execution environment, actual outputs, and original failure records. Screenshots can illustrate observations but cannot replace execution data.

Distinguish three levels: runnable code; an observation under specified conditions; value for real software production. An earlier level does not establish a later one.

## Record format for each experiment

[Proposal] Create corresponding Chinese and English records containing:

- Experiment ID, associated claims, epistemic status, execution progress, protocol version;
- Question, controls, input sequence, validator provenance, budget, stopping conditions;
- Implementation and knowledge versions, reproduction steps, raw-data locations;
- All costs, failures and deviations, excluded samples and reasons;
- Observations, interpretations, alternatives, scope, and next steps.

Execution progress uses planned / awaiting reproduction / running / finished and does not replace epistemic status. Conclusions use supported / contradicted / inconclusive; workflow adoption or a single success is not confirmation.
