[Home](../README.md) · [中文](设计原则-Design-Principles.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# Design principles

All items below are [Proposal]: working research rules for v0.1, not proven universally optimal architecture.

| Principle | Operational meaning | Boundary to preserve |
|---|---|---|
| Knowledge DRY; implementations may be WET | DRY means an explicit authoritative knowledge source; WET here permits local implementation duplication, not a fixed copy count | Authority may be physically distributed, with versions, provenance, and conflict handling. Well-validated shared libraries remain an option |
| Persistent state; potentially ephemeral implementation | Facts, identities, permissions, rules, and evidence do not exist solely in one implementation or conversation | Ephemeral does not mean immediate deletion; retain adopted implementations and necessary failed samples for audit and replay |
| Speculate before commitment; commit strictly | Validate candidates in isolation before changing authoritative state | Commitment means business-state writes or external effects, not merely a Git commit; unknown results do not automatically pass |
| Testable outcomes; flexible processes | Define acceptable outcomes and resource budgets while allowing different paths | A score does not establish specification completeness; provide an inconclusive exit |
| Separate generation from acceptance | Explanations are not execution evidence; diversify test origins and checking mechanisms | Agreement among implementations is not proof of correctness |
| Preserve contracts; generate adapters when useful | Contracts define data and behavioral obligations; adapters translate representations | Check units, permissions, time semantics, and failure semantics |
| Feedback control serves explicit objectives | Observe deviations and choose repair, replacement, rollback, degradation, or shutdown | Optimize latency and cost only within hard constraints |
| Persist lessons in the environment | Record each exception's source, scope, effective date, expiry condition, and check | Review rule changes; a failing candidate must not automatically weaken acceptance criteria |
| Budget attention and computation | Cap candidates, retries, runtime, and human escalation frequency | On budget exhaustion, retain evidence and stop or escalate instead of generating indefinitely |

## Example

[Proposal] A reporting unit reads only authorized data and generates a chart under rule version R2. Generate several implementations and check boundary cases and independently reconciled data. Presentation may be scored; unauthorized reads require rejection. Adoption records the rule version, input digest, test evidence, and implementation ID.

[Open] Duplication versus sharing, and regeneration versus repair, depend on measured costs. Test them through the [initial RFCs](../提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.en.md) and [EX-08](../实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md). See the [glossary](术语表-Glossary.en.md).
