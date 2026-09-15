# 贡献指南 · Contributing

[返回首页 / Home](README.md) · [中文](#中文) · [English](#english)<br>
版本 / Version: v0.1 · 2026-09-14

<a id="中文"></a>
## 中文

【建议】欢迎提出反例、复现实验、补充来源、修订命题、改进解释或校对翻译。不需要先认同研究假设，也不要求会写代码。

### 选择入口

- [讨论区](https://github.com/changsheng0804-blip/ai-native-software-production/discussions)：开放问题、批评、真实需求、尚无明确完成条件的想法。
- [议题](https://github.com/changsheng0804-blip/ai-native-software-production/issues)：一个有完成条件的验证问题；写清命题、方法、指标和预期产物。
- 合并请求（PR）：对正式文件的修订；说明改了什么、原因、来源、影响范围和检查结果。

【建议】不会操作合并请求时，直接发讨论说明“哪篇文章、哪句话、为什么、有什么依据”。讨论可以先用一种语言，正式纳入仓库时补齐双语。

### 讨论如何进入正式文档

【建议】讨论区按模板提交（反例与反驳／竞争框架／真实需求／开放问题／自由想法，模板见 [.github/DISCUSSION_TEMPLATE](.github/DISCUSSION_TEMPLATE/)）。新观点由维护者或研究 agent 定期整理进 [意见清单](研究记录-Research-Notes/意见清单-Viewpoint-Ledger.zh-CN.md)：每条记录来源、主张、针对命题、状态与所需证据。被吸收的观点双语同步并带四类认识状态；被拒绝或被反例推翻的同样记录理由、不删除历史。意见清单的存在理由是防止研究只沿一条线索自我确认——异质意见是理论的异质验证来源。

### 四类状态和证据

【建议】正式断言使用【已确认 / Confirmed】【推断 / Hypothesis】【不确定 / Open】【建议 / Proposal】。定义和范围见 [证据与参考](证据-Evidence/证据与参考-Evidence-and-References.zh-CN.md)。

【建议】“已确认”必须有直接支持具体断言的来源或运行证据。区分来源自述、独立复现和跨场景推广。测试失败、负面结果、无法判断均值得提交；不得删掉失败样本制造成功率。

### 双语与命名

【建议】同一篇正式长文使用相同中文名＋英文名，分别以 .zh-CN.md 和 .en.md 结尾。两版同步更新版本、命题编号、状态、限定条件、数字、引用和实验结论；翻译不得把“可能”改成“必然”。

README.md 和 CONTRIBUTING.md 保留 GitHub 可识别的标准文件名，文件内提供完整中英文。其余正式目录和文件采用中文＋英文。对话与探索草稿不作为第二套正式知识源。

### 修订命题或提案

【建议】保留命题编号，记录旧说法、新说法、证据与反例，以及为何扩大或缩小范围。RFC 是征求意见稿；采用“草案 → 讨论中 → 采纳／拒绝／被替代”的流程。流程状态独立于四类认识状态，采纳不等于有效性已被证明。

### 提交实验

【建议】使用 [实验索引的记录格式](实验-Experiments/实验索引-Experiment-Index.zh-CN.md)。补齐源码、环境、输入、配置、复现步骤、原始结果、失败样本和全部成本。必要的工具或生成配置用于复现，不用模型身份划分观点归属。

【建议】提前写明对照、预算、质量门槛、停止条件与结果判断办法。公开数据应去除密钥、私人对话、个人数据和无关账号信息。来源材料只公开与研究相关且有权公开的内容。

### 合并前检查

【建议】核对中英文含义一致、引用直接支持断言、相对链接有效、状态与证据相符；明确哪些实验实际运行过。讨论聚焦观点与证据，批评方案不攻击参与者。许可方案尚待决定，当前没有许可证文件。

---

<a id="english"></a>
## English

[Proposal] Contributions include counterexamples, reproduction, references, claim revisions, clearer explanations, and translation review. Agreement with the hypotheses and coding ability are not prerequisites.

### Choose an entry point

- [Discussions](https://github.com/changsheng0804-blip/ai-native-software-production/discussions): open questions, criticism, real needs, and ideas without defined completion criteria.
- [Issues](https://github.com/changsheng0804-blip/ai-native-software-production/issues): a bounded verification question with a claim, method, metrics, and deliverables.
- Pull requests: formal document revisions explaining the change, rationale, evidence, scope, and checks.

[Proposal] If pull requests are unfamiliar, post the document, sentence, concern, and evidence in a discussion. Informal discussion can start in one language; formal adoption requires both.

### How discussions enter the formal documents

[Proposal] Submit discussions using the templates (Counterexample / Competing Frameworks / Real Needs / Open Questions / Free Ideas; templates in [.github/DISCUSSION_TEMPLATE](.github/DISCUSSION_TEMPLATE/)). The maintainer or a research agent periodically consolidates new views into the [Viewpoint Ledger](研究记录-Research-Notes/意见清单-Viewpoint-Ledger.en.md): each entry records source, claim, targeted proposition, status, and evidence required. Absorbed views are synchronized bilingually with one of the four epistemic statuses; rejected or overturned views are also recorded with reasons, and history is not deleted. The ledger exists to keep the research from confirming itself along a single thread — heterogeneous opinions are a heterogeneous verification source for the theory.

### Status and evidence

[Proposal] Use 【已确认 / Confirmed】, 【推断 / Hypothesis】, 【不确定 / Open】, or 【建议 / Proposal】 for formal claims. See definitions and scope in [Evidence and references](证据-Evidence/证据与参考-Evidence-and-References.en.md).

[Proposal] Confirmation requires a source or execution evidence directly supporting the specific claim. Distinguish self-report, independent reproduction, and generalization. Failed tests, negative results, and inconclusive findings are welcome; do not discard failures to manufacture success rates.

### Languages and names

[Proposal] Formal long documents share the same Chinese-plus-English basename, ending in .zh-CN.md and .en.md. Synchronize revision, claim IDs, statuses, qualifications, numbers, references, and conclusions. Translation must not turn “may” into “must.”

README.md and CONTRIBUTING.md retain GitHub-recognized filenames and contain full Chinese and English versions. Other formal directories and files use Chinese-plus-English names. Conversations and exploratory drafts are not a second authoritative knowledge base.

### Revising claims and proposals

[Proposal] Preserve claim IDs and record old and new statements, evidence, counterexamples, and reasons for changing scope. RFC workflow is Draft → In discussion → Accepted / Rejected / Superseded. Workflow status is separate from epistemic status; adoption does not prove effectiveness.

### Submitting experiments

[Proposal] Follow the [experiment record format](实验-Experiments/实验索引-Experiment-Index.en.md). Supply code, environment, inputs, configuration, reproduction steps, raw results, failures, and full costs. Tool and generator configurations support reproduction; model identity does not organize intellectual contributions.

[Proposal] Specify controls, budgets, quality gates, stopping rules, and decision criteria in advance. Remove secrets, private conversations, personal data, and unrelated account information from public data. Publish only research-relevant source material that contributors are authorized to disclose.

### Before merging

[Proposal] Check language equivalence, directly supporting references, working relative links, and status–evidence consistency. State which experiments actually ran. Focus discussion on claims and evidence; criticize proposals without attacking participants. License selection remains pending; no license file is currently included.
