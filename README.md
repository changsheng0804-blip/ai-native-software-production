# AI 原生软件生产 · AI-Native Software Production

[中文](#中文) · [English](#english)<br>
五分钟入口 / Five-minute introduction · v0.1 · 2026-09-14

<a id="中文"></a>
## 中文

**如果 AI 成为主要的代码生成者，软件的工作单位、质量控制、知识保存和人机分工应该如何重新组织？**

【建议】这里是持续修订的研究根据地。围绕命题、证据、实验与状态组织，不以模型身份划分观点。

### 核心假设与当前原则

【推断】通过明确任务边界、持久知识、独立验收和受控组合，可能让大部分工作持续落在 AI 的有效能力范围，并减少系统演进时的人类协调负担。详见 [核心命题](理论-Theory/核心命题-Core-Thesis.zh-CN.md)。

【建议】首批原则：

- **知识 DRY，实现可 WET**：规则有明确权威版本，局部代码允许重复。
- **状态持久，实现可临时**：事实、身份、规则与证据能在实现替换后延续。
- **试错前置，提交严格**：隔离环境中尝试，改变正式状态前核验。
- **目标可检验，过程可变化**：在硬约束内探索，并保留人工判断出口。

### 研究方法与当前进度

【建议】按“分析 → 推演 → 外部来源核验 → 整合方案 → 对照实验 → 修订”推进。比较完整成本、有效功能和人类协调时间，保留反例和失败。

【已确认】首版根据原始讨论文档与后续讨论整理了双语理论、3 份提案、实验索引和证据登记；整理依据见 [来源摘要](证据-Evidence/来源摘要-Source-Digest.zh-CN.md)。

【不确定】原文报告的 **7 个原型尚待本仓库复现**；源码和运行记录未随附件取得。**EX-08 只是计划，未运行**。目前没有证明这套组织方式整体优于现有方法。

### 还不知道什么

【不确定】任务切分是否仍依赖人理解全局？验证与集成会不会吃掉收益？历史例外如何继承？多个候选会不会一起犯错？见 [开放问题](理论-Theory/开放问题-Open-Questions.zh-CN.md)。

### 从这里继续

| 想了解什么 | 入口 |
|---|---|
| 当前理论 | [核心命题](理论-Theory/核心命题-Core-Thesis.zh-CN.md) · [设计原则](理论-Theory/设计原则-Design-Principles.zh-CN.md) · [生产闭环](理论-Theory/生产闭环-Production-Loop.zh-CN.md) · [术语表](理论-Theory/术语表-Glossary.zh-CN.md) |
| 首批提案 | [知识 DRY / 实现 WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.zh-CN.md) · [状态持久 / 实现临时](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.zh-CN.md) · [试错前置 / 提交严格](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.zh-CN.md) |
| 实验与思想变化 | [实验索引](实验-Experiments/实验索引-Experiment-Index.zh-CN.md) · [持续演进对照计划](实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.zh-CN.md) · [研究演进](研究记录-Research-Notes/研究演进-Research-Evolution.zh-CN.md) |
| 依据与状态 | [证据与参考](证据-Evidence/证据与参考-Evidence-and-References.zh-CN.md) · [来源摘要](证据-Evidence/来源摘要-Source-Digest.zh-CN.md) |

### 如何贡献

【建议】不会写代码也可以：在 [讨论区](https://github.com/changsheng0804-blip/ai-native-software-production/discussions) 提问题、反例或真实需求；在 [议题](https://github.com/changsheng0804-blip/ai-native-software-production/issues) 跟踪具体实验；通过合并请求提出双语修订。详见 [贡献指南](CONTRIBUTING.md)。

四类认识状态一一对应：**已确认 / Confirmed · 推断 / Hypothesis · 不确定 / Open · 建议 / Proposal**。正式长文中英文保持同一版本。许可证选择待定。

---

<a id="english"></a>
## English

**If AI becomes a primary code generator, how should work units, quality control, knowledge retention, and human–AI responsibilities be reorganized?**

[Proposal] This is an evolving research home organized by claims, evidence, experiments, and status rather than model identity.

### Core hypothesis and current principles

[Hypothesis] Explicit task boundaries, durable knowledge, independent acceptance, and controlled composition may keep most work within AI's effective capabilities and reduce human coordination load as systems evolve. See the [core thesis](理论-Theory/核心命题-Core-Thesis.en.md).

[Proposal] Initial principles:

- **Knowledge DRY; implementations may be WET:** authoritative rule versions, optional local duplication.
- **Persistent state; potentially ephemeral implementation:** facts, identity, rules, and evidence survive replacement.
- **Speculate before commitment; commit strictly:** try in isolation and verify before authoritative state changes.
- **Testable outcomes; flexible processes:** explore within hard constraints with an explicit human-judgment exit.

### Method and current stage

[Proposal] Analyze → derive hypotheses → verify external sources → integrate proposals → run controlled experiments → revise. Measure full costs, accepted features, and human coordination time; retain counterexamples and failures.

[Confirmed] This edition synthesizes the source document and subsequent discussions into bilingual theory, 3 RFCs, an experiment index, and an evidence register. See the [source digest](证据-Evidence/来源摘要-Source-Digest.en.md).

[Open] The **7 source-reported prototypes await reproduction here**; their code and execution records were unavailable with the attachment. **EX-08 is a protocol, not a completed experiment.** No overall superiority over existing approaches has been established.

### What remains unknown

[Open] Does decomposition still require global human understanding? Will validation and integration consume the gains? How will historical exceptions survive? Will candidates fail together? See [open questions](理论-Theory/开放问题-Open-Questions.en.md).

### Continue reading

| Interest | Entry points |
|---|---|
| Current theory | [Core thesis](理论-Theory/核心命题-Core-Thesis.en.md) · [Design principles](理论-Theory/设计原则-Design-Principles.en.md) · [Production loop](理论-Theory/生产闭环-Production-Loop.en.md) · [Glossary](理论-Theory/术语表-Glossary.en.md) |
| Initial proposals | [Knowledge DRY / code WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.en.md) · [Persistent state / ephemeral implementation](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.en.md) · [Speculate freely / commit strictly](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.en.md) |
| Experiments and revisions | [Experiment index](实验-Experiments/实验索引-Experiment-Index.en.md) · [Longitudinal protocol](实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md) · [Research evolution](研究记录-Research-Notes/研究演进-Research-Evolution.en.md) |
| Sources and status | [Evidence and references](证据-Evidence/证据与参考-Evidence-and-References.en.md) · [Source digest](证据-Evidence/来源摘要-Source-Digest.en.md) |

### Contribute

[Proposal] No coding is required: bring questions, counterexamples, or real needs to [Discussions](https://github.com/changsheng0804-blip/ai-native-software-production/discussions); track experiments in [Issues](https://github.com/changsheng0804-blip/ai-native-software-production/issues); propose bilingual revisions through pull requests. See [Contributing](CONTRIBUTING.md).

Statuses correspond exactly: **已确认 / Confirmed · 推断 / Hypothesis · 不确定 / Open · 建议 / Proposal**. Formal Chinese and English texts share one revision. License selection is pending.
