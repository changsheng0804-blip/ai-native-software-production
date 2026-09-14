[Home](../README.md) · [中文](09-文档生产试验田-Document-Production-Trial-Field.zh-CN.md)

Version: v0.1 · Updated: 2026-09-15 · Paired language revision: v0.1

# EX-09: Document production trial field

Epistemic status: 【建议 / Proposal】 · Execution progress: running<br>
Related: Q2 (verification cost), H5 (knowledge retention); scope limits below

## Question

[Proposal] Use this repository's own document production as a minimal observation field: the repository owner sets goals and accepts results; AI produces. This division of labor is itself a miniature of the research vision — the human retreats to the position of goals and acceptance. A single question is measured:

> **For each accepted delivery, how many minutes does the human spend on stating what is wanted and on acceptance?**

## What it can and cannot answer

[Proposal] It can observe the shape of acceptance cost across task types (one facet of Q2) and the distribution of rejection causes: unclear instruction, generation drift, missing acceptance criteria.

[Open] It cannot be extrapolated to software production: documents have no runtime, state, or composition problem; the sample is small; the measurer is a party to the work. This experiment provides early data points for Q2 only and is not used to support or oppose H1.

## Record

| Round | Date | Task | Intent (minutes) | Acceptance (minutes) | Rejection rounds | Result | Notes |
|---|---|---|---|---|---|---|---|
| 1 | 2026-09-15 | Theory consolidation batch 1: interface-rigidity document plus this experiment design | not measured | 2 | 1 | Passed (sections 5–6 not understood; rewritten for re-verification) | Baseline round; intent accumulated from prior discussion; rejection cause: unclear exposition. First observation: acceptance took only 2 minutes yet included unread sections — cheap acceptance is also shallow acceptance; related to Q2 |
| 2 | 2026-09-15 | Re-verification of rewritten sections 5–6 | 0 (original intent) | 1 | — | Passed | Read two sections only; understood after rewrite. Lesson: the same information in plain language is accepted faster and more deeply |

## Measurement rules

[Proposal] Intent: time from finishing the previous deliverable to stating the next requirement. Acceptance: time from receiving a deliverable to giving pass / reject and what to change. Times use 5-minute granularity; round up rather than omit. One rejection round per request; multiple issues listed in one rejection still count as one round. Acceptance pass line: understood and approved; parts passed without understanding are recorded as not passed and await rewriting — this rule was added from the round-1 observation.

## Summary and stopping

[Proposal] Summarize every 10 rounds: average acceptance minutes, rejection rate, rejection-cause distribution. If acceptance time stays well above the value of the delivery, that is itself an important Q2 observation. No termination deadline; the field continues with repository maintenance.
