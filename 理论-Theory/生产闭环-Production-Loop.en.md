[Home](../README.md) · [中文](生产闭环-Production-Loop.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# Production loop

[Proposal] Durable outputs include work units, checkable constraints, execution evidence, persistent knowledge, and traceable decisions. This is a reference process to be tested.

~~~mermaid
flowchart TD
  A["Human: goals, boundaries, tradeoffs"] --> B["Environment: facts, rules, permissions, evidence"]
  B --> C["Decompose tasks; define contracts and budgets"]
  C --> D["Generate candidates"]
  D --> E["Isolated execution; independent acceptance"]
  E --> F{"Hard constraints pass and evidence sufficient?"}
  F -->|"No / inconclusive"| G["Repair, regenerate, abandon, or escalate"]
  G --> C
  F -->|"Yes"| H["Composition checks; verify current state"]
  H --> I["Controlled commitment and adoption"]
  I --> J["Observe operation"]
  J --> K["Review and update knowledge"]
  K --> B
  J --> G
~~~

## Artifacts at each step

| Step | Required artifacts | Primary responsibility |
|---|---|---|
| Goals and boundaries | Accepted and prohibited behaviors, soft objectives, resource caps, escalation conditions | Humans define tradeoffs; tools help express them |
| Decomposition | Unit ID, inputs and outputs, dependencies, required rule versions | System proposes; humans resolve conflicts or undecomposable work |
| Generation | Implementation ID, generation configuration, input and knowledge versions | Generation stage |
| Isolated acceptance | Test versions, raw results, failure samples, unknowns | Acceptance stage using complementary evidence |
| Composition and commitment | Global checks, current state version, adoption rationale | Commit control mechanism |
| Observation | Behavior, incidents, cost, affected scope | Runtime environment |
| Learning | Source event, revised rule, scope, expiry condition | Review before knowledge adoption |

## Commitment boundary

[Proposal] Candidates propose change plans; an explicit commit mechanism performs authoritative writes. It checks identity, permissions, rule versions, current state, hard constraints, and unique operation IDs. Stop automatic commitment on failed constraints, conflicting verdicts, stale snapshots, or exhausted budgets.

For operations competing over shared state, checking and writing require concurrency control; checking now and writing later without protection is insufficient. Database isolation behavior is documented, while cross-system effects need separate design. [E04](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e04)

## Decisions after failure

[Proposal] Repair localized defects; regenerate when rules are clear and replacement is economical; consider rollback for regressions; degrade when dependencies are unavailable; escalate specification conflicts, boundary violations, and inconclusive acceptance. Rolling back code does not automatically undo messages or other external effects. Record unresolved reconciliation work.

## Carry history into the next cycle

[Proposal] Each knowledge record includes an ID, claim, source event, scope, version, expiry condition, verification method, and one of the four epistemic statuses. Preserve supersession links when retiring rules instead of erasing mistaken conclusions.

[Open] Validators and knowledge can themselves be wrong. The loop must test how such errors are detected, challenged, and corrected. [Open questions](开放问题-Open-Questions.en.md)
