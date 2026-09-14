[Home](../README.md) · [中文](0001-知识DRY实现WET-Knowledge-DRY-Code-WET.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# RFC-0001: Knowledge DRY, implementation WET

Epistemic status: 【建议 / Proposal】<br>
Workflow status: Draft / 草案<br>
Related claim: H2; questions: Q5, Q6; experiment: EX-08 mechanism comparison

RFC means Request for Comments: a design proposal made open to challenge and experiment. Workflow status is separate from epistemic status; adoption does not confirm a hypothesis.

## Problem and hypothesis

[Hypothesis] Shared implementation offers reuse benefits but may propagate change across consumers. Local duplication may reduce that propagation while increasing synchronization, repair, storage, and validation costs. Net benefit is unknown.

## Proposal

[Proposal] Maintain rules, exceptions, and acceptance requirements as versioned authoritative knowledge. Permit units to generate local implementations from the same knowledge version. DRY means avoiding conflicting authorities for knowledge; WET here only permits implementation duplication.

Each knowledge record includes a rule ID, version, source, scope, effective and expiry conditions, positive and negative examples, and checks. Implementations record knowledge dependencies and contracts. A rule change identifies affected units, triggers validation, and informs retention, repair, or replacement.

Example: date-display rule R1 requires the user's selected time zone. Reports and reminders may implement it separately while depending on R1. Both must be checked when the rule changes. A shared rule does not guarantee either implementation is correct.

## Boundaries and alternatives

[Proposal] Retain shared libraries, explicit services, and local duplication as alternatives. Do not default to generated replacements for established capabilities such as cryptography merely to achieve duplication. Generation permissions and authoritative state writes retain common controls.

[Open] Localization cannot eliminate coupling through data, rules, time, and resources. Authoritative knowledge can itself become a failure source and needs versioning, checks, and recovery.

## Minimal validation design

[Proposal] Use the same small product, rules, and acceptance set:

- A: shared implementation, centrally changed with consumer validation;
- B: shared authoritative rules, local implementations synchronized and validated using dependency records;
- Introduce rule changes, exceptions, shared implementation defects, and local defects in the same event sequence under equal total budgets.

Record affected unit counts, human coordination minutes, rule drift, regressions, jointly failing inputs, and total generation and validation cost. Both arms maintain rules and dependency records, preventing knowledge-management benefits from being misattributed to duplication.

## Decision and stopping rules

[Proposal] Preregister scale, repetitions, cost caps, and a minimum meaningful effect. Support H2 only within the tested scope if B improves total or coordination cost under the predefined rule at equal quality. Narrow scope if drift or cost offsets the gain; mixed results remain [Open].

Stop for unauthorized authoritative writes, persistent rule conflicts, or budget exhaustion. Retain failures; do not remove difficult cases to favor an arm.

## Pending decisions

[Open] Who resolves knowledge conflicts? How are rule versions retired? Which capabilities should be shared? Could dependency inventories create a new maintenance burden?

Source: [S1 synthesis of five directions](../证据-Evidence/来源摘要-Source-Digest.en.md#s1). This proposal has no measured results; the [evidence ledger](../证据-Evidence/证据与参考-Evidence-and-References.en.md) does not treat agreement among versions as correctness evidence.
