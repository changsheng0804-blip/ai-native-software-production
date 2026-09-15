[Home](../README.md) · [中文](意见清单-Viewpoint-Ledger.zh-CN.md)

Version: v0.1 · Updated: 2026-09-15 · Paired language revision: v0.1

# Viewpoint Ledger: collecting and disposing of divergent views

## Purpose

[Proposal] This ledger collects views, counterexamples, and competing frameworks from different people, at different times, which may contradict each other, and tracks how each one was disposed of. Its reason for existing is the repository's own epistemological discipline: **research must not confirm itself along a single thread (the equivalent of a "common-cause failure" of the theory) — heterogeneous opinions are a heterogeneous verification source for the theory.** This is the same thing, applied at the research level, as the design principles "separate generation from acceptance" and "make verification sources as heterogeneous as possible".

## Rules

[Proposal]

- New views preferably come from GitHub Discussions (submitted with the [discussion templates](../.github/DISCUSSION_TEMPLATE/)), or from explicit disagreements during the research;
- Each entry records: ID, date, source, claim, targeted proposition, status, evidence required, outcome;
- Status values: **pending review / under discussion / absorbed (→ location) / rejected (→ reason) / overturned by a counterexample (→ location)**;
- Views absorbed into formal documents must be synchronized bilingually and carry one of the four epistemic statuses; rejections and overturns are also recorded with reasons, and history is not deleted (repository discipline: failures and counterexamples are part of the result);
- Periodic consolidation: paced by the research; suggested after every 10 entries or at each experiment summary, executed by the maintainer or a research agent.

## Register

| ID | Date | Source | Claim summary | Targets | Status | Evidence required | Outcome |
|---|---|---|---|---|---|---|---|
| V001 | 2026-09-15 | Repository owner, discussion | "Economics of confirmation": cheap tokens make the entire try–err–confirm loop cheap; strategy shifts from "right the first time" to "converge through the loop"; intent can converge conversationally | D1, D8, Section 4 premise | Absorbed | — (quantity side holds; quality side needs external anchors) | Deepened into [D1 of Fundamental Differences](../理论-Theory/生产差异-Fundamental-Differences.en.md); EX-08 records "intent statement" time and rejection reasons to distinguish the two paths |
| V002 | 2026-09-15 | Kirsch ([E23](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e23)) | The ephemeral-software hypothesis is flawed: constrained regeneration → no longer ephemeral; unconstrained → boundary knowledge lost; the future is malleable rather than ephemeral | RFC-0002, Q4 | Absorbed | Needs EX-08 comparison | Dilemma folded into [Open question Q4](../理论-Theory/开放问题-Open-Questions.en.md) |
| V003 | 2026-09-15 | Kent Beck ([E24](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e24)) | No need to reorganize production: keep TDD, small steps, humans adjudicate; AI produces "plausible-looking but broken" code | H1 | Absorbed | Needs EX-08 comparison | Made one of the [EX-08](../实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md) control groups |
| V004 | 2026-09-15 | Anthropic context engineering ([E20](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e20)) | The bottleneck is context, not verification; engineering focus shifts to context engineering | D1, D4 | Absorbed | — | Recorded in [§5.2 of Fundamental Differences](../理论-Theory/生产差异-Fundamental-Differences.en.md): not mutually exclusive; context engineering is a subproblem of the verification system |
| V005 | 2026-09-15 | Spec-driven development ([E21](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e21), [E22](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e22)) | Specs are "living, executable assets" with staged verification; isomorphic to "acceptance-check-style interfaces" | D8, Q2 | Absorbed | Needs to verify who bears spec-writing cost | Absorbed in [§5.2 of Fundamental Differences](../理论-Theory/生产差异-Fundamental-Differences.en.md) as the same class of solution, with differences marked |
| V006 | 2026-09-15 | Repository owner, discussion | Production organization should be rebuilt as a "verification-driven selection system" (five zones: intent / generation / verification / commit / environment), rather than forcing AI into an interlocking assembly line | D1–D8, Production Loop | Absorbed | Needs EX-08 comparison | Formalized as [Production Organization](../理论-Theory/生产组织形态-Production-Organization.en.md) |

## Relationship to existing documents

- Discussion entry and submission process: [Contributing](../CONTRIBUTING.md)
- Evidence register for views: [Evidence and references](../证据-Evidence/证据与参考-Evidence-and-References.en.md)
- Destination of absorbed views: theory documents (Fundamental Differences, Interface Rigidity, Core Thesis, Design Principles, RFCs)
