[Home](../README.md) · [中文](术语表-Glossary.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# Glossary

[Proposal] The table defines usage within this research so readers and contributors can communicate consistently. It does not claim universal definitions across fields.

| Term | Meaning in this repository |
|---|---|
| AI-native software production | Designing work units, acceptance, knowledge retention, and responsibility around AI participation in primary generation |
| Production unit | Work with explicit inputs, outputs, scope, dependencies, and acceptance; not necessarily a function or service |
| Candidate implementation | Code or an executable artifact generated for a requirement but not yet adopted |
| DRY | Don't Repeat Yourself; the emphasis here is explicit knowledge authority |
| WET | Permission for local implementation duplication; no required copy count |
| Contract / 契约 | Checkable agreements on data, units, permissions, behavior, and failure handling |
| Adapter / 适配器 | An implementation translating one party's representation into another's contract |
| Oracle / 判定器 | A mechanism judging requirements, possibly returning pass, fail, or inconclusive |
| Validator / 验证器 | A checking tool or process; passing checks does not establish complete specifications |
| Invariant / 不变量 | A condition required to hold throughout the specified operations |
| Sandbox / 沙箱 | An isolated execution environment limiting reads, writes, networking, and resources |
| Commitment / 状态提交 | An authoritative business-state change or external effect, distinct from a Git commit |
| Idempotency / 幂等 | Repeating the same operation request must not duplicate its business effect |
| Rollback / 回滚 | Restoring an earlier version or state; restoration scope depends on the mechanism |
| Common-cause failure / 共因失效 | Candidates fail together through shared misunderstandings, sources, or dependencies; correlation magnitude must be measured |
| Convergence / 收敛 | Reaching a target set under explicit conditions; specify states, process, assumptions, and time horizon |
| Self-stabilization / 自稳定 | Recovery to and preservation of legitimate states in a specified model; see E01 |
| CRDT | Conflict-free Replicated Data Type for merging specified replicated data; see E02 |
| Human coordination load / 人类协调负担 | Human time and decisions for decomposition, rules, acceptance, integration, recovery, and knowledge synchronization |
| RFC | Request for Comments, recording a proposed design and validation plan |
| Issue / 议题 | A bounded question or experimental work item with completion criteria |
| PR | Pull Request, a reviewable change proposed for inclusion in the main version |
| Preregistration / 预注册 | Writing questions, methods, metrics, thresholds, and stopping rules before observing results |

[Evidence and references](../证据-Evidence/证据与参考-Evidence-and-References.en.md) · [Contributing](../CONTRIBUTING.md)
