[Home](../README.md) · [中文](生产差异-Fundamental-Differences.zh-CN.md)

Version: v0.1 · Updated: 2026-09-15 · Paired language revision: v0.1

# Fundamental Differences: how an AI producer differs from a traditional producer

## One-sentence thesis

[Hypothesis] The fundamental difference between the two producers is not "speed" but the **simultaneous inversion of cost structure and of the epistemological status of artifacts**:

- In traditional production, the most expensive step is "translating intent into a correct implementation"; in AI production this step is nearly free, and the bottleneck shifts to "stating intent clearly + verifying whether the result is correct".
- In traditional production, the artifact (code) is the definition of behavior; in AI production, the artifact is only one candidate sample of behavior, and its text can neither determine nor fully describe its behavior.

This document gathers the repository's scattered observations — the alchemy-like feeling, the code–explanation mismatch, the verification bottleneck, discreteness and tolerance, interface rigidity — into one difference table, and uses three reasons — "cheap / mistake-proofing / nature" — to judge which differences will disappear as models grow stronger and which will not. This document integrates concepts and draws inferences only; it adds no experimental evidence.

## 1. The baseline for comparison

The following are analysis premises. The category column distinguishes "architectural fact" (checkable against public models and API documentation; this repository has not independently reproduced them), "current model state" (may change as models progress), and "inference":

| Dimension | Traditional producer (human programmer) | AI producer (LLM) | Category |
|---|---|---|---|
| Cost of generation | Expensive, scarce, slow | Cheap, abundant, fast | Current model state (the cheap side is expected to persist) |
| Nature of output | Deterministic: written once, behavior fixed | Probabilistic: every call is a resample | Architectural fact |
| Persistent state | Internal memory + external artifacts | No cross-call internal state; only a context window | Architectural fact (current) |
| Intent → implementation | The most expensive step | A nearly free step | Current model state (expected to persist) |
| Error pattern | Few, locatable, do not recur after repair | Frequent, confident, possibly common-cause; fixed does not mean fixed forever | Current model state (mistake-proofing class) |
| Status of the artifact | Definition of behavior | One candidate sample of behavior | Inference (holds under the current model state) |

## 2. Eight fundamental differences

Each entry is structured: mechanism → production consequence → durability (cheap / mistake-proofing / nature) → corresponding existing items → falsification condition. Except for the architectural facts in the "mechanism" column, every entry is [Hypothesis].

### D1 Cost structure inverted: implementation becomes free, verification becomes the bottleneck

- **Mechanism**: LLMs push the translation cost of "intent → implementation" to near zero; but output is probabilistic, and correctness cannot be attested by the generator itself — it must be verified externally. [Hypothesis] Human verification throughput has not grown with generation speed; the cheaper generation gets and the more it produces, the larger the total volume awaiting verification.
- **Production consequence**: the bottleneck moves from "production" to "proof". Production organization is designed around "making verification cheap": acceptance front-loaded, checkable interfaces, generate–verify loops, verification budgets.
- **Durability**: cheap (abundance continues with the economics of compute; does not disappear) + mistake-proofing (the per-round verification burden falls as models grow stronger) + nature (verification cost has no zero lower bound in principle: tests can only falsify (Dijkstra), behavioral equivalence is undecidable, and E09 shows that even TLA+-level formal verification carries a fixed cost of "hundreds of lines of spec plus weeks of learning" — model progress lowers error rates, but it cannot remove the minimal verification volume of "confirming whether the real intent is satisfied").
- **Corresponds to**: Q2 (will verification swallow generation gains), EX-09, the README's "generation speed grows faster than verification speed", the design principle "budget attention and compute".
- **Falsification**: verification means appear that scale automatically with generation volume with proportionally falling cost; or evidence shows the verification burden does not grow with generation volume and acceptance time is not a bottleneck.

### Deepening D1: the economics of confirmation (discussion addendum, 2026-09-15)

[Hypothesis] A more precise phrasing of "implementation becomes free" is that **the entire try–err–confirm loop becomes cheap**: not only is generating a candidate nearly free — repeated attempts, follow-up questions, redo, and confirmation within the conversation are nearly free too (token consumption). This shifts the user's strategy space from "think it through upfront and get it right the first time" (because every attempt used to be expensive) to "make a rough first attempt, then converge through the cheap loop" (because every attempt now burns only a few tokens). Three consequences follow:

- **Intent does not need to be fully specified upfront**: intent can be forced out inside the loop through "wrong → correct → retry", making the conversation itself the production floor rather than a communication phase before production — partially relieving D8's "specify first" pressure. This is complementary to the premise warning in Section 4: upfront intent is one sufficient path; conversational convergence is another, cheaper path; the two can be tested in parallel (EX-08 records "intent statement" time and rejection reasons to distinguish them).
- **What is cheap is the quantity of "trying", not the quality of "being right"**: the reliability of confirmation does not grow with token consumption; it is determined by external anchors (real execution, real data, checkable results) and human judgment. Conversational confirmation without anchors is just paying to hear self-testimony (E34–E36).
- **Human attention does not expand with cheap tokens**: the more loops and the more items awaiting confirmation, the more attention becomes the bottleneck (design principle "budget attention and compute"; Level 3).

### D2 The epistemological status of the artifact: from "definition" to "sample"

- **Mechanism**: autoregressive generation makes code text just one sample from a conditional distribution; the text cannot fully determine its behavior; explanations and documentation are written after the fact against the generated text, not two expressions of the same internal understanding (the "two skins" phenomenon).
- **Production consequence**: the review intensity of reading code falls; execution evidence becomes the main source of knowledge about behavior; the generator cannot testify for itself, so generation and acceptance must be separated.
- **Durability**: nature (self-report is never verification evidence, only a matter of degree) + mistake-proofing (as model self-consistency improves, the reliability with which text predicts behavior rises, but not to "verification-free").
- **Corresponds to**: research evolution §2, the design principle "separate generation from acceptance", RFC-0001's authoritative knowledge version, S0 §II.
- **Falsification**: artifact text plus generation configuration reliably predicts behavior (reading code ≈ knowing behavior); this difference degrades into a purely quantitative one.

### D3 Output always exists, correctness is never promised (confident errors)

- **Mechanism**: LLMs tend to produce fluent output for almost any input; when specifications are vague or the task is unsolvable, errors are usually silent rather than "I don't know".
- **Production consequence**: systems must make errors visible: checkable outputs, an explicit "cannot judge" exit, a commit gate, budget caps. Vague intent is no longer absorbed by the implementer's judgment; it turns directly into plausible-looking wrong artifacts.
- **Durability**: mistake-proofing (alignment and refusal training will improve it) + nature ("default production" is a structural property of autoregression; it can be suppressed, not eliminated).
- **Corresponds to**: the production loop's "cannot judge" branch, the design principle "speculate before commitment; commit strictly", research evolution §2.
- **Falsification**: under vague specifications the model consistently refuses or asks questions, and its silent error rate falls below that of human programmers.

### D4 No persistent memory: knowledge must live in the environment

- **Mechanism**: no persistent state across calls; the context window is finite, and the more information it holds the more it dilutes; there is no unified internal understanding that feeds both code and documentation.
- **Production consequence**: the environment (repository, rule base, evidence, state) becomes the system's memory; "the environment holds knowledge; AI fetches it on demand". Long context is not knowledge; authority and timeliness must be maintained by the environment.
- **Durability**: the weight of "nature" rests on "which facts are current and authoritative is governed by the environment", not on "no internal state" — vendors are building persistent memory; even if internal memory arrives, it does not overturn D4, it only changes the parameters of environment design. The falsification condition correspondingly becomes: internal memory clearly outperforms environmental governance.
- **Corresponds to**: RFC-0002, the design principle "persist lessons in the environment", H3, research evolution §3.
- **Falsification**: models gain persistent, versionable, retrievable internal memory that clearly outperforms environmental solutions.

### D5 Sampling fluctuation and common-cause failure: fixing once does not mean fixed forever

- **Mechanism**: every generation is a new sample; a fix does not transfer across samples; multiple candidates share the same model bias, the same vague specification, the same omitted boundaries, so failures are highly correlated.
- **Production consequence**: N candidates ≠ N independent attempts; reliability comes from heterogeneous verification sources, loops, and isolation, not from candidate count; every "rebirth" carries regression risk, and a replacement must pass acceptance again.
- **Durability**: mistake-proofing (thins as models become more reliable, but a structural residue remains).
- **Corresponds to**: the error-correlation dimension, the design principle "separate generation from acceptance" (do not treat agreement among multiple implementations as proof), Q6.
- **Falsification**: evidence shows that same-source candidates barely overlap in their failing-input sets.

### D6 Repair naturally tends to accumulate rather than delete

- **Mechanism**: autoregression is incremental continuation; "delete, simplify, refactor" requires explicit planning and is not default behavior. Round after round of "fixes" tends to add conditions, compatibility layers, and patches.
- **Production consequence**: units with low rebuild cost tend toward "replace rather than patch"; units must be small enough to discard and swap; acceptance sheets must block "patch accumulation quietly changing behavior".
- **Durability**: mainly mistake-proofing (extended thinking and training will improve deletion ability) + partly structural.
- **Corresponds to**: the README's "good at continuing to generate, not at stopping to delete things", interface rigidity's "retreat line", the design principle "persistent state; potentially ephemeral implementation".
- **Falsification**: evidence shows patching cost stays below regeneration cost, or models' deletion/simplification ability is stably stronger than their continuation ability.

### D7 Parallelism and speed change the strategy space: exploration replaces careful design

- **Mechanism**: generation takes seconds and can be cheaply parallelized; keeping many candidates at once is affordable within a compute budget.
- **Production consequence**: "deliberate waste", multi-candidate filtering, lineage-style organization, and evolutionary selection become rational strategies; human work shifts from "polishing one artifact" to "choosing a lineage and allocating resources".
- **Durability**: cheap (permanent).
- **Corresponds to**: the README's five directions (lineage, deliberate waste), interface rigidity's "generate many, filter fast", direction four.
- **Falsification**: evidence shows the gains of multiple candidates do not outweigh the verification and filtering costs (exactly what Q2 is meant to quantify).

### D8 The precision of intent shifts onto humans: specification becomes the bottleneck

- **Mechanism**: once translation is free, the model does not know "what you want"; vague intent is no longer absorbed by the implementer's domain judgment; it directly produces plausible-looking artifacts.
- **Production consequence**: the scarce human skill shifts from "writing implementations" to "turning vague feelings into checkable constraints" (acceptance sheets). The acceptance sheet becomes the primary persistent artifact; acceptance cost may swallow generation gains — EX-09's first-round observation: "cheap acceptance is also shallow acceptance".
- **Durability**: nature (permanent. Intent never transfers automatically; models growing stronger does not make "knowing what you want" cheaper — it only makes expressing constraints more valuable).
- **Corresponds to**: direction five (making taste and intent explicit), Q2, interface rigidity's "acceptance-check" anchor, H4.
- **Falsification**: evidence shows that pass rates under vague specifications do not vary with specification clarity, or acceptance time is not a production bottleneck.

## 3. Which one is the "real difference"

[Hypothesis] The unified statement is **the cost-structure inversion of D1 + D8**: the most expensive step in traditional production is "turning intent into a correct implementation"; in AI production the most expensive step becomes "stating intent clearly + verifying results". Every other difference is either a cause or a consequence of it:

```text
Cause side: D3 (confident errors), D5 (probabilism and common-cause failure) → make verification necessary and expensive
Main claim: D1 (implementation free, verification becomes the bottleneck) + D8 (specification becomes the human bottleneck)
Consequence side: D2 (artifacts are samples; run beats read), D4 (knowledge moves into the environment), D6 (replace beats patch), D7 (exploration strategies become feasible)
```

Use the three reasons — "cheap / mistake-proofing / nature" — to judge durability:

- **Thins with model progress** (mistake-proofing class): D3 silent errors, D5 error rates, D6 accumulation tendency. These describe weaknesses of current models, not the foundation of the new production mode.
- **Does not disappear with model progress** (cheap class + nature class): D7 parallelism, D1's abundance side (cheap); D2 self-attestation invalid, D4 environmental governance (knowledge moves into the environment), D8 intent bottleneck, D1's minimal verification volume (nature).

[Hypothesis] This yields a testable judgment: **even if models become strong enough that "first generation is basically correct", production organization must still be rebuilt around D8 (intent) and D4 (memory); and as long as generation remains cheap (D1), generate-many, filter-fast, redo-on-failure stays a rational strategy.** Therefore "production differences" are not a temporary phenomenon of "models not being strong enough".

[Open] The boundaries of D1–D8 may interpenetrate — for example, D8 and D2 both involve "artifacts do not carry intent"; they are split into eight for falsifiability, not to build a complete classification.

## 4. The production mode that follows

The following restates existing principles (the nine design principles, the three RFCs, the production loop, interface rigidity) as one whole; all items are [Proposal], with validity to be tested by [EX-08](../实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md)/[EX-09](../实验-Experiments/09-文档生产试验田-Document-Production-Trial-Field.en.md):

**Premise warning**: items 1–3 imply "intent can be fully stated and frozen into an acceptance sheet before execution". This premise faces three independent rebuttal sources: Taylorism's known failure mode of "separating planning from execution" in manufacturing (tacit knowledge loss, waste of quality-by-final-inspection — Deming opposed exactly "quality through inspection"); Suchman's *Plans and Situated Actions*: "plans are weak representations of action; execution is full of situated improvisation"; and this repository's own EX-09 round-1 observation "cheap acceptance is also shallow acceptance" (shallow acceptance often because intent was not stated clearly). "Intent can be fully specified upfront" should therefore be downgraded to a testable hypothesis: if "unclear explanation" dominates the rejection-reason distribution in EX-08, the premise fails, and the center of gravity of persistent assets should move from "acceptance sheets" toward "knowledge environment + evidence", with acceptance sheets as only one resource. E24's outcome-orientation and "acceptance-first" are two faces of the same hypothesis.

1. **The production unit is the loop, not the artifact**: the production unit changes from "an implementation written correctly once" to a "generate–verify loop". The artifact (implementation) is disposable; the loop (goal + acceptance criteria + evidence records + knowledge environment) persists. This also gives the earlier discussion's "self-improving unit" a derived position: it is not a novel mechanism, but the natural production unit under D1 + D2 + D8 — because artifacts are samples (D2) and generation is cheap (D1), the only thing that can persist is the loop that keeps producing acceptable samples.
2. **The persistent assets are acceptance criteria and the knowledge environment, not code**: code can be regenerated; acceptance sheets (acceptable behaviors, prohibited behaviors, inconclusive exit) and the knowledge environment (rules, exceptions, evidence) cannot.
3. **The human role is acceptance-sheet author and conflict adjudicator**: humans no longer read implementations line by line; they work on goals, acceptance sheets, and upgrade conflicts (a corollary of interface rigidity's "kernel + periphery"); this is also the point of accountability (defect liability, compliance), not only a cognitive necessity.
4. **Interface tightness is a design variable**: loosen where possible to the "acceptance-check style" (do not dictate how, only check results), at the cost that checkable pass criteria must exist; where it cannot be loosened, keep the "gear style" (precise contracts). Tightness itself must be measured per task (the interface rigidity document's "retreat line").
5. **Error-visibility design**: inconclusive exit, commit gate, budget caps, isolation sandbox — make probabilistic errors observable, isolatable, rollback-able events rather than silent bad results.
6. **Make verification sources as heterogeneous as possible**: tests, types, permission checks, data reconciliation, human spot checks come from different sources, so that common-cause failures are not missed by same-source validators.

## 5. External-evidence checks and the strongest rebuttals

### 5.1 Empirical status of the three core claims (checked 2026-09-15; sources in [Evidence and references](../证据-Evidence/证据与参考-Evidence-and-References.en.md))

| Claim | Empirical status | Key sources |
|---|---|---|
| D1 Verification becomes the bottleneck (generation gains decay at the delivery end) | Partially supported: generation-side speedups confirmed repeatedly (lab +55.8%, field +26%, commit volume +180–240%), but delivery-end gains decay sharply (actual releases only +30%), supporting the "weak-link hypothesis"; "human verification throughput does not grow" still lacks direct longitudinal measurement, so [Hypothesis] is retained | E12–E16, E18 |
| D2 Artifacts are samples; self-report is unreliable | Supported (the current-model-state part): CoT explanations can be induced into unfaithfulness; about one-fifth of LLM comments contain verifiable errors and consistency detection is ineffective; self-check/self-correct without external feedback is ineffective. The nature part — "self-report can never attest" — remains [Hypothesis] | E34–E36, E25 |
| D5 Common-cause failure | Supported with boundaries: integration reliability gains from same-source candidates are only 0.43/0.44 of what the independence assumption promises; when different models err simultaneously, about 60% err in the same place; yet sampling still yields real gains (pass@k, self-consistency) that depend on an external selector — the absolute claim "multiple candidates are useless" does not hold | E30–E33 |

### 5.2 The strongest rebuttals and responses

1. **"Not inversion, just exposure"** (E23, E24, E10 Brooks): verifying/discovering correct behavior was always the essential cost; AI merely cut the coding cost that was never the dominant part. **[Response]** Whether "the bottleneck ratio really flips" needs longitudinal measurement: E16's +240% commits → +30% releases is the strongest existing evidence for the "flip". But that decay gap is compatible with at least three competing explanations: ① low-value output (the extra commits are copy-paste blocks or code that was not needed — E17 points the same way; E16 also reports "application counts surge while total usage does not grow" across four software markets, consistent with this); ② demand-side saturation (teams do not need more releases); ③ stricter review standards (humans became more demanding, rather than throughput not growing). The "flip" can therefore currently be stated only as "consistent with the verification bottleneck, not excluded". To distinguish: EX-08 counts output by value (useful features preregistered and passing independent acceptance), classifies rejection reasons as "unclear explanation / generation deviated / acceptance criteria missing / feature itself valueless" (using EX-09's established "generation deviated" phrasing), and puts "generation minutes vs. acceptance minutes ratio" on its metrics list.
2. **The "disposable implementation" dilemma** (E23): constrained regeneration (must read old code, diffs, logs, tests) → it is no longer ephemeral software; unconstrained → every regeneration round resets accumulated boundary knowledge. **[Response]** This is the attack line RFC-0002 must answer head-on: which side the boundary knowledge sedimented in implementations (exceptions, compatibility, implicit contracts) belongs to needs a designed comparison in EX-08; it has been folded into Q4.
3. **The context-bottleneck school** (E20): the bottleneck is context, not verification. **[Response]** The two are not mutually exclusive: context engineering is a subproblem of the verification system (only with the right facts can acceptance and generation be correct), not a substitute for reorganizing production.
4. **The specification-driven school** (E21, E22): SDD is highly isomorphic to "acceptance-check-style interfaces". **[Response]** Absorb it as the same class of solution and mark the differences: who bears the spec-writing cost, how specs are versioned (Q2), and the gap the SDD literature does not cover — "who writes the tests themselves, and whether they are written correctly".
5. **The improvement school** (E24): keep TDD, small steps, tests as contracts, humans continue adjudicating — no reorganization needed. **[Response]** Do not argue only in theory: make it one of EX-08's control groups, compared against H1's "reorganize production" group.

## 6. The question truly worth attacking: the verification bottleneck (Q2)

[Proposal] If only one question may be attacked first, choose the verification bottleneck. Reasons:

1. **Hub position**: D1's corollary is "all generation-side advantages are capped by verification cost". If verification is not cheap, multi-candidate, replacement, and loops all stall; if verification is cheap and trustworthy, the whole production mode follows naturally.
2. **Greatest organizational leverage**: acceptance front-loading, interface tightness, heterogeneous evidence, error visibility — all are production-mode-level dials that do not depend on new model capabilities (the effectiveness of validator generation itself depends on model capability, so it belongs under "to be tested", not premises).
3. **Testable now**: [EX-08](../实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md)'s design (public debugging set + hidden acceptance set) and [EX-09](../实验-Experiments/09-文档生产试验田-Document-Production-Trial-Field.en.md) (already measuring "intent statement + acceptance" minutes; the first round already observed "cheap acceptance is also shallow acceptance") already point at it.

**Why not wait for the model to solve verification itself**: if self-verification reaches auditable reliability, the mistake-proofing part fails, but the nature part (confirming real intent) and the D8 side (acceptance-sheet authors remain human) do not change — attacking verification is "hedging both ways", not "betting that models do not improve". Section 3's conclusion — rebuild around D8 (intent) and D4 (memory) — is therefore robust to model progress; this section's "most worth attacking now" is sensitive to model progress and must carry this condition. EX-08 may add a "self-verification vs. external acceptance" comparison arm as a discriminator.

[Proposal] The specific preregistered increments for EX-08:

- separate the public debugging set from the hidden acceptance set (already suggested by the repository);
- implant known defects into the acceptors and measure miss rates and false-rejection rates (a minimal version of "who verifies the validators");
- follow EX-09's measurement rules and record "intent statement + acceptance" human minutes per useful feature;
- run the same requirement sequence under two interface tightness levels (gear vs. acceptance-check) and compare acceptance cost and combined failure rates.

[Open] Acceptors themselves can also err (the second half of Q2; the production loop's "acceptors and knowledge itself can also err"). This is the hardest and most easily overlooked part of the verification-bottleneck problem.

## 7. Key unknowns and falsification conditions

| Unknown | Current status | What would advance the judgment |
|---|---|---|
| Whether the acceptance-cost curve varies systematically with task type | [Open] | EX-08/EX-09 data: human acceptance minutes grouped by task type |
| Actual strength of common-cause failure | [Open] | Q6 experiment: overlap of failing-input sets across different samplings and phrasings under the same specification and model |
| Whether heterogeneous verification can compensate for common-cause failure | [Open] | Compare miss rates of same-source vs. heterogeneous validators |
| How to measure interface tightness | [Open] | Interface rigidity document's undecided item: format-check counts, acceptance-sheet item counts, rework rates |
| Whether verification cost truly swallows generation gains | [Open] | EX-08 control-group comparison of total human time |
| Whether human verification throughput grows with generation volume | [Open] | No direct longitudinal measurement yet (E12–E16 provide only indirect evidence; human-side reference: manual inspection rate is roughly 100–200 LOC/hour, Boehm & Basili put early-fix cost at 10–100× cheaper than late-fix, but AI scenarios still lack longitudinal data); EX-08 adds a "generation minutes vs. acceptance minutes" ratio metric |
| When model self-verification can be trusted | [Open] | Repeatedly measure with the validator-audit method of E19/E28 (implant known defects, measure miss and false-rejection rates); EX-08 adds a "self-verification vs. external acceptance" comparison arm |

## 8. Relationship to existing documents

| Difference | Main correspondence |
|---|---|
| D1 cost inversion | Q2, EX-09, README, design-principle budgets |
| D2 artifacts are samples | separate generation from acceptance, research evolution §2, RFC-0001 |
| D3 confident errors | speculate before commitment / commit strictly, production loop |
| D4 no persistent memory | RFC-0002, H3, write lessons back into the environment |
| D5 common-cause failure | error correlation, Q6 |
| D6 accumulation tendency | ephemeral implementation, replace beats patch |
| D7 exploration strategy | five directions (lineage, deliberate waste) |
| D8 intent bottleneck | direction five, acceptance-check-style interface, H4 |

This document's "the loop is the production unit" restates the flowchart in [Production loop](生产闭环-Production-Loop.en.md); the "kernel + periphery" shape follows [Interface rigidity](接口刚性-Interface-Rigidity.en.md).

## Evidence registry

[Confirmed] External evidence has been registered in the repository format in [Evidence and references](../证据-Evidence/证据与参考-Evidence-and-References.en.md) (E12–E37, checked 2026-09-15, verified online by the research agent, not read in full, article by article). Core conclusions: ① generation-side speedups are well supported and delivery-end decay is directly quantified by E16 — "verification is the bottleneck" is partially supported, but "human verification throughput does not grow" still lacks direct measurement ([Hypothesis] retained); ② common-cause failure has code-scenario quantitative evidence (E31) with clear boundaries (sampling still yields gains that depend on an external selector); ③ self-report unreliability has the strongest evidence (E34–E36). The strongest rebuttals (E23's dilemma, E24's improvement school, E20's context school, E21's specification-driven school) are recorded with responses in §5.2, and E23's dilemma is folded into [Open question Q4](开放问题-Open-Questions.en.md).
