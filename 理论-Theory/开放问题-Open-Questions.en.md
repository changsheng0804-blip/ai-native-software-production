[Home](../README.md) · [中文](开放问题-Open-Questions.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# Open questions

Every question below is [Open]; next steps are [Proposal]. Priority expresses research order, not validated importance.

| ID | Question | Evidence that would advance the judgment | Next step |
|---|---|---|---|
| Q1 | Does decomposition still require humans to understand the entire system? | Decomposition time and cross-unit coordination at each complexity stage | EX-08, including decomposition and human rescue |
| Q2 | Will validation consume generation gains, and who validates validators? | Hidden independent checks, deliberately seeded errors, miss and false-rejection rates, all acceptance costs | EX-08, separate visible debugging and hidden acceptance sets |
| Q3 | Why can individually accepted units fail in composition? | Cross-boundary errors involving concurrency, history, permissions, and units | RFC-0003 commitment experiment |
| Q4 | How do exceptions and state survive replacement? | Rule retention after a fresh session and state reconciliation | RFC-0002 with deliberate context resets and replacement; answer the [E23](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e23) dilemma head-on (constrained regeneration vs. loss of boundary knowledge) |
| Q5 | How much duplication is economical? | Full change costs, rule drift, and common-cause failures under shared and local implementations | RFC-0001 without a predetermined winner |
| Q6 | How correlated are candidate failures? | Jointly failing input sets and generation configurations under the same specification | Compare resampling, different generation configurations, and specification formulations |
| Q7 | When can local feedback guarantee global convergence? | Proofs or counterexamples with explicit state space, legitimate set, scheduling assumptions, and stopping conditions | Define a tiny formal model first; stable patterns do not establish business correctness |
| Q8 | Does the objective function hide undeclared value judgments? | High-scoring outputs that violate real needs and recorded metric conflicts | Separate hard constraints and soft objectives; retain human judgment |
| Q9 | Is automatically formed identity and hierarchy worthwhile? | Cost and failure comparison against explicitly defined units | Recover EX-07; first compare a simple explicit hierarchy |
| Q10 | Is there a common mathematical structure across software and collective systems? | Explicit objects, mappings, assumptions, and properties that do not transfer | Treat analogies as leads and verify each mapping |
| Q11 | Can human coordination load grow more slowly over the long term? | Longitudinal data across stages and independent repetitions at equal quality and total budgets | EX-08; do not infer universal scaling from small samples |

## Undecided items

[Open] No universal runtime platform, optimal unit size, candidate count, or implementation lifetime is established. Examples are not product commitments.

[Proposal] First recover historical prototype code and runtime conditions, then preregister EX-08: metrics, budgets, stopping rules, and decision criteria written before execution. Do not prioritize more biological analogy prototypes yet.

Related: [Experiment index](../实验-Experiments/实验索引-Experiment-Index.en.md) · [Evidence gaps](../证据-Evidence/证据与参考-Evidence-and-References.en.md)
