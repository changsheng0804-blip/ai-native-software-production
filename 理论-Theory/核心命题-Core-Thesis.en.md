[Home](../README.md) · [中文](核心命题-Core-Thesis.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# Core thesis

## Object of study

[Proposal] Study production units, quality control, knowledge carriers, composition boundaries, and responsibility allocation. Self-repair, candidate generation, and dynamic adaptation are optional mechanisms. Historical analogies generate questions; they do not establish organizational effectiveness.

[Confirmed] The source document and subsequent discussion pose this research question. This confirms provenance only; outcomes still require experiments. [Source digest S0–S1](../证据-Evidence/来源摘要-Source-Digest.en.md)

## H1: Production organization hypothesis

[Hypothesis] For software tasks amenable to decomposition, verification, and isolation, redesigning task boundaries, external knowledge, acceptance mechanisms, composition, and human–AI responsibilities may keep most work within AI's effective capabilities and reduce human coordination load during system evolution.

A stronger version predicts that human coordination load grows more slowly than product complexity over a predefined range. This is not a universal law; a single success or short curve cannot establish long-term behavior.

## H2–H5: Testable subsidiary claims

| ID | Status and claim | Potential disconfirming observation |
|---|---|---|
| H2 | [Hypothesis] Authoritative rule versions with locally duplicated implementations reduce the propagation of implementation changes | Rule drift, repeated fixes, and validation cost exceed isolation benefits |
| H3 | [Hypothesis] Separately persisted facts, identities, and constraints preserve history through implementation replacement | Exceptions disappear, migration is difficult, or full conversations must be reread |
| H4 | [Hypothesis] Isolated candidate trials before commitment reduce erroneous changes to real state | Simulation gaps, stale snapshots, or external effects erase the benefit |
| H5 | [Hypothesis] Turning runtime evidence into versioned knowledge reduces repeated human escalations | Rules grow and conflict while later generations repeat the same mistakes |

See [RFC-0001](../提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.en.md), [RFC-0002](../提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.en.md), and [RFC-0003](../提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.en.md).

## Measuring value

[Proposal] Compare two production organizations using the same requirement sequence, quality gates, and resource caps. Record:

- Human coordination minutes per independently accepted feature;
- Accepted feature count, regressions, state violations, and permission violations;
- All decomposition, generation, validation, integration, recovery, and knowledge maintenance costs;
- Human escalation rate, cross-unit coordination events, and retention of historical rules.

An accepted feature must pass preregistered behavioral checks; lines of code and candidate counts are not output measures. Human time includes specification, validator, and rule maintenance. Moving costs into those activities must not remove them from accounting. See [EX-08](../实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md).

## Scope and limits

[Proposal] Start with real features having limited effects, rollback options, and independent acceptance criteria. Add state, concurrency, rule changes, and historical exceptions progressively. Use stricter specialized engineering for high-risk cores; generated replacement is not assumed appropriate.

[Open] How much benefit is explained by decomposability, verifiability, reversibility, and failure correlation? Shared facts and resources still create coupling; implementation isolation does not remove essential business complexity.

[Open] Neither historical prototype reports nor external mechanism references establish H1. Failure, no benefit, and narrower applicability are valid findings. [Evidence and references](../证据-Evidence/证据与参考-Evidence-and-References.en.md)
