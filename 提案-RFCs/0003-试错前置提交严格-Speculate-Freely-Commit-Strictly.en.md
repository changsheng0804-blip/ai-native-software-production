[Home](../README.md) · [中文](0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# RFC-0003: Speculate before commitment, commit strictly

Epistemic status: 【建议 / Proposal】<br>
Workflow status: Draft / 草案<br>
Related claim: H4; questions: Q2, Q3, Q8; experiment: EX-08 side-effect and concurrency checks

## Problem and hypothesis

[Hypothesis] Trying several alternatives in a controlled environment may trade additional computation for fewer real errors. Benefits depend on simulation coverage, state freshness, validation capability, and commitment costs.

## Proposal

[Proposal] Define a candidate → acceptance → authoritative-state-change boundary:

- Candidates lack authoritative write and external send permissions by default, reading authorized snapshots or simulated data.
- Check hard constraints before ranking by latency, cost, or other soft objectives. Soft scores cannot compensate for hard failures.
- The selected candidate proposes an execution plan bound to rule versions, an expected state version, a unique operation ID, and evidence.
- Recheck current permissions and state before commitment; revalidate if state changed. Protect checking and writing with transactions, locks, or conditional writes appropriate to the business operation.
- For external services, specify irreversible effects, duplicate prevention, and reconciliation of requests with unknown outcomes.
- Reject automatic commitment on failure, conflict, inconclusive results, or exhausted budgets; preserve evidence and stop or escalate.

Commitment here changes business facts; it is not a Git version-control commit. Saving files to Git is not deployment or a change to users' business state.

## A concurrency counterexample

[Proposal] Use fictional inventory: two candidates each pass isolated checks against a snapshot containing one item. That does not authorize both to sell it. Authoritative commitment must protect the nonnegative-inventory condition, or accepted units can still cause a composition failure.

[Confirmed] Database serializable isolation requires applications to handle certain conflict failures by retrying. This is documented behavior of a specific mechanism. [E04](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e04)<br>
[Open] It does not establish the same guarantee for an operation spanning databases, messages, and external services.

## Minimal validation design

[Proposal] Compare A, one candidate with a strict commit boundary, against B, multiple isolated candidates with the same boundary, to identify the incremental value of candidate search. If needed, separately compare how early validation occurs without weakening either arm's actual permission controls.

Inject stale snapshots, concurrent contention, duplicate requests, external timeouts, candidate permission violations, missing tests, and jointly wrong candidates. Start with simulated external endpoints; experiments must not create real transactions or messages.

Record rejection reasons, validator misses, authoritative-state violations, duplicate effects, latency, total cost, and human escalation. Count unknown outcomes; do not automatically classify timeouts as success or failure.

## Decision and stopping rules

[Proposal] Preregister trial count, budgets, quality gates, and minimum meaningful effects. Support H4 only if B improves full cost or error control at equal quality. Narrow scope or abandon multiple candidates if overhead or simulation gaps erase benefits.

Stop immediately on sandbox escape or unauthorized authoritative effects. Observing no errors supports only the tested scope, not absolute safety.

Source: [S1 revised simulation and strict commitment proposal](../证据-Evidence/来源摘要-Source-Digest.en.md#s1). See the broader [production loop](../理论-Theory/生产闭环-Production-Loop.en.md).
