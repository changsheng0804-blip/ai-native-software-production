[Home](../README.md) · [中文](生产组织形态-Production-Organization.zh-CN.md)

Version: v0.1 · Updated: 2026-09-15 · Paired language revision: v0.1

# Production organization: from "assembly line" to a "verification-driven selection system"

## The question

[Proposal] The characteristics and pain points of generative AI (D1–D8 in [Fundamental Differences](生产差异-Fundamental-Differences.en.md)) clash with the "interlocking chain" way that industrial continuous production is organized. This document answers: if software production were reorganized so that its structure matches the production characteristics of generative AI, what would it look like? The whole document is a sketch of an organizational form ([Proposal]), not a proven universal optimum; analogies are used to raise questions, and effectiveness is to be tested by [EX-08](../实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md).

## 1. The essence of the clash: correctness presupposed vs. correctness verified

[Hypothesis] The organizational logic of the assembly line (continuous production, the long call chains of conventional software engineering) is: **correctness is built into the structure** — each stage's output is by default a valid input to the next, so production can be organized by "processing order": A must be correct, then B can be correct, then C can be correct.

The characteristics of generative AI mean correctness **cannot be presupposed; it can only be verified afterwards**:

- output is sampled (D5): one stage's error propagates and amplifies along the chain;
- artifacts are samples (D2): the implementation text is not trustworthy; running beats reading;
- "get it right the first time" is not viable (D1, D3): convergence must come through the loop.

Hence the first principle of reorganization:

> **Make verification a first-class citizen of the organizational structure instead of an appendage of the production flow — structure is organized by "verification boundaries", not by "processing order".**

[Hypothesis] This also explains why AI feels natural in images and short-form media but awkward in software: image production has short chains where every step can be seen and discarded on failure; software has been organized into long chains that amplify AI's weakness (every step may be wrong) into a fatal flaw.

## 2. The organizational form: five zones

[Proposal] A production unit (or the whole production system) consists of five responsibility zones. They are not departments; they are five positions within the same loop:

| Zone | Content | Who/what | Characteristics |
|---|---|---|---|
| **Intent zone** | Acceptance sheet: acceptable behaviors, prohibited behaviors, "cannot judge" exit, budget caps | Human | The only zone only humans can do; all human work lives here: setting goals, writing pass criteria, adjudicating conflicts |
| **Generation zone** | Many candidates, free experimentation; failure is normal traffic, not an incident | AI (isolated environment, cheap) | Multi-candidate, deliberate waste, lineage branching all happen here; failure cost is low enough to ignore |
| **Verification zone** | Candidates must pass the acceptance sheet plus execution evidence; the validators themselves must also be audited (E19/E28 method) | Mechanism (heterogeneous sources) | Does not trust quantity (common-cause failure, D5), does not trust self-report (D2, E34–E36), trusts only external anchors |
| **Commit zone** | Only candidates that passed verification plus state checks (permissions, concurrency, latest state) are written into authoritative state; rollback-able | Gate mechanism | Commit = changing authoritative state or producing external effects, not just saving files; irreversible external actions get their own gate |
| **Environment zone** | Rule base, evidence, exceptions, state — versioned | Persistent storage | Knowledge does not disappear with implementations; implementations can be replaced, the environment persists (RFC-0002) |

Loop direction: intent zone → generation zone → verification zone → (fail → back to generation or escalate to humans) → commit zone → runtime observation → lessons written back to the environment zone → intent-zone revision. Details in the flowchart of [Production Loop](生产闭环-Production-Loop.en.md).

## 3. Sketch: from "assembly line" to "breeding farm"

[Proposal] An analogy for communication (not a proof): continuous production is like an **assembly line** — raw material is by default acceptable, every process step is standardized, defective items are detected at the end, and inventory is stored long-term. Generative production is more like a **breeding farm**:

- every plant differs (sampling);
- good or bad is only known after it grows (verification);
- pulling out one bad plant does not harm the others (discreteness + tolerance);
- breeding is cheap, so sow many and select (deliberate waste);
- the gene bank preserves lineage and history (environment zone);
- the farmer decides what variety is wanted, selects, and adjudicates what stays (humans).

Mapping: the order = the acceptance sheet; the nursery = the generation zone; selection = the verification zone; transplanting = the commit zone; the gene bank = the environment zone.

[Open] The analogy only helps communication; it cannot prove gains. Its most valuable use is guiding the choice of experiment subjects (see Section 5).

## 4. Why it matches AI's characteristics (mapping table)

| AI characteristic / pain point | Organizational counterpart |
|---|---|
| Generation is cheap (D1) | Generation zone runs deliberate waste and multi-candidate; replace beats patch |
| Output is probabilistic, errors correlate (D5) | Verification zone uses heterogeneous evidence and does not trust candidate count |
| Artifacts are samples; self-report unreliable (D2) | Verification zone accepts only execution evidence; reading implementation and listening to explanations are not acceptance criteria |
| No memory (D4) | Environment zone carries all knowledge; implementations can be replaced, knowledge is not lost |
| Fixed does not mean fixed forever (D5) | Every commit is independently verified; "it was fixed last time" is not inherited |
| Good at adding, bad at deleting (D6) | Cheap units tend toward rebirth rather than patching; acceptance sheets stop patch accumulation |
| Only humans know the intent (D8) | The intent zone is human-only; the acceptance sheet is the human's persistent output |
| Output always exists; errors are silent (D3) | Commit gates and the "cannot judge" exit make errors visible and rollback-able |

## 5. Application scenarios and the transition path

[Proposal] Scenarios where this can win (following the "range map" of [Interface Rigidity](接口刚性-Interface-Rigidity.en.md)): tasks that simultaneously satisfy — can be split into small pieces; each piece's quality is easy to judge (cheap acceptance); mistakes can be undone (reversibility); one piece failing does not implicate others (discreteness). Examples: reports, forms, internal small tools, format conversion, content pipelines.

[Proposal] Transition is not overturning the existing system; it is "**cultivating islands, then connecting the islands**":

1. find independently acceptable units inside the existing system;
2. give each unit a minimal loop: acceptance sheet + isolated generation + verification gate;
3. use EX-08 to compare the same requirement sequence under both organizations (useful features, human coordination minutes, regression defects, escalation ratio);
4. expand the plots that win; record the scope where it loses, without claiming universal victory.

[Hypothesis] This path corresponds to the repository's three verification levels: Level 1 existence (can an island work), Level 2 local gains (is an island better than the traditional organization), Level 3 organizational gains (after islands are connected, does global human coordination really decrease).

## 6. Relationship to existing documents

- Difference basis: [Fundamental Differences](生产差异-Fundamental-Differences.en.md) (D1–D8)
- Interface shape: [Interface Rigidity](接口刚性-Interface-Rigidity.en.md) (acceptance-check interfaces, kernel + periphery, range map)
- Process details: [Production Loop](生产闭环-Production-Loop.en.md)
- Propositions and unknowns: [Core Thesis](核心命题-Core-Thesis.en.md) (H1–H5), [Open Questions](开放问题-Open-Questions.en.md) (Q1–Q11)
- To be tested: [EX-08](../实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md), [EX-09](../实验-Experiments/09-文档生产试验田-Document-Production-Trial-Field.en.md)
