[返回首页](../README.md) · [English](证据与参考-Evidence-and-References.en.md)

版本：v0.2 · 更新：2026-09-15 · 中英文同步版本：v0.2

# 证据与参考

## 四类认识状态

【建议】本仓库统一使用下表。标签描述具体断言的证据状态，不评价作者或工具；有来源不代表来源的所有主张都成立。

| 中文 | English | 使用条件 |
|---|---|---|
| 【已确认】 | [Confirmed] | 给出直接支持该断言的可核查来源或运行证据，并注明范围；“来源报告过”与“我们已复现”分开 |
| 【推断】 | [Hypothesis] | 从现有材料提出的解释或可检验命题；列出前提、反例与验证办法 |
| 【不确定】 | [Open] | 材料不足、证据冲突、无法复现或尚未检验 |
| 【建议】 | [Proposal] | 候选设计、研究方法、流程和下一步；不是有效性结论 |

【建议】源文档出现“已验证”时，先检查底层证据再决定本仓库状态。提案被接受、文章发表、多模型一致或测试通过，都不能自动升级成没有范围限制的【已确认】。

## 本项目来源与证据缺口

| 编号 | 来源 | 核验范围 | 限制 |
|---|---|---|---|
| S0 | 用户提供的原始讨论文档 | 已读取；章节、七个原型记述及文件摘要见来源登记 | 原始附件未公开；未取得原型代码和运行材料 |
| S1 | 后续讨论 | 已读取；生产组织主线、五方向整合和建设要求 | 是思想来源，不是结果证据 |
| EX-01–07 | S0 报告的原型 | 【不确定】待复现 | 未运行；无可公开复现实验包 |
| EX-08 | 首版纵向对照计划 | 【建议】方案已写，尚未运行 | 无数据、统计结果或优劣结论 |

[来源摘要](来源摘要-Source-Digest.zh-CN.md) · [实验索引](../实验-Experiments/实验索引-Experiment-Index.zh-CN.md)

## 已核对的外部参考

核对日期：E01–E05 为 2026-09-14，E06–E11 为 2026-09-15，E12–E37 为 2026-09-15（研究 agent 网络核验；除注明外只核验到题录、摘要或官方页，未逐篇通读全文）。下列只确认所读来源的有限内容。它们分别支持机制背景或个别论断，均未直接验证 H1 或本仓库三个 RFC 的整体收益。

<a id="e01"></a>
### E01：自稳定系统

Edsger W. Dijkstra，1974，*Self-stabilizing systems in spite of distributed control*，EWD 426，Communications of the ACM 17(11), 643–644。[作者手稿转录，得克萨斯大学档案](https://www.cs.utexas.edu/~EWD/transcriptions/EWD04xx/EWD426.html)

【已确认】文中在给定状态机、局部动作及调度模型下讨论从非法状态进入合法集合，并维持合法性的系统。<br>
【不确定】把可生成实现、持续需求变化和外部业务效果纳入同类保证，需要另外定义和证明。关联 Q7。

<a id="e02"></a>
### E02：可合并的复制数据类型

*About CRDTs*，由该领域研究者维护。[CRDT 官方研究资源站](https://crdt.tech/)

【已确认】CRDT（无冲突复制数据类型）针对其定义的数据结构与更新、合并规则处理副本冲突。<br>
【不确定】副本收敛不能直接保证业务约束正确，也不意味着任意生成程序都能收敛。关联 RFC-0002、Q10。

<a id="e03"></a>
### E03：生成候选并用测试评价

*GenProg: Evolutionary Program Repair*。[研究团队项目主页](https://squareslab.github.io/genprog-code/)

【已确认】项目描述了搜索源代码修改候选、用测试集评价和迭代的修复方法。<br>
【不确定】该方法的存在不能证明测试覆盖全部正确性，也不能证明即时重生优于维护；本版不采用网站中的历史成本与成功率数字。关联 Q2。

<a id="e04"></a>
### E04：事务隔离与并发提交

PostgreSQL，*13.2 Transaction Isolation*，读取时对应版本 18。[官方文档](https://www.postgresql.org/docs/18/transaction-iso.html)

【已确认】文档区分多种隔离级别，并说明可串行化事务发生特定冲突时，应用需要准备重试。<br>
【不确定】数据库内的机制不自动覆盖跨服务消息与其他外部效果。关联 RFC-0003。

<a id="e05"></a>
### E05：研究讨论载体

GitHub，*GitHub Discussions documentation*。[官方文档](https://docs.github.com/en/discussions)

【已确认】讨论区用于社区提问、交流和开放讨论。<br>
【建议】本仓库用讨论区探索想法、议题跟踪可完成的问题、合并请求修订双语理论；这是组织选择。

<a id="e06"></a>
### E06：监督树与运行时换码（Erlang/OTP）

Joe Armstrong，2003，*Making reliable distributed systems in the presence of software errors*，瑞典皇家理工学院（KTH）博士论文。[论文全文（Erlang 官方站托管）](https://erlang.org/download/armstrong_thesis_2003.pdf)；机制另见 Erlang/OTP 官方文档 [Supervisor Behaviour](https://www.erlang.org/doc/system/sup_princ.html) 与 [Release Handling](https://www.erlang.org/doc/system/release_handling.html)。

【已确认】官方文档记载：监督者按重启策略维持子进程存活，重启超过强度上限时自身终止并交上级处置；Erlang 支持运行时替换模块代码，SASL 框架可在运行中升级／降级整个版本。Armstrong 论文 §4.3 原文陈述错误处理哲学："让别的进程做错误恢复；做不到就死掉；让它崩溃；不要防御式编程"（"Let it crash. Do not program defensively."）。<br>
【不确定】"实现可再生、状态持久、失败由监督策略裁决"在电信级系统长期运行可行，不证明把实现交给 AI 生成后替换同样安全。流传的 AXD301"九个九"可用性数字系论文自述的未存档来源，本仓库不作效果证据。关联 RFC-0002、生产闭环的失败决策。

<a id="e07"></a>
### E07：恢复导向计算（ROC）

David Patterson、Aaron Brown 等 15 人，2002，*Recovery Oriented Computing (ROC): Motivation, Definition, Techniques, and Case Studies*，技术报告 UCB//CSD-02-1175，加州大学伯克利分校计算机科学部（伯克利／斯坦福联合项目，2001–2006）。[报告 PDF（项目站）](http://roc.cs.berkeley.edu/papers/ROC_TR02-1175.pdf)、[伯克利技术报告页存档](https://web.archive.org/web/2024/http://www2.eecs.berkeley.edu/Pubs/TechRpts/2002/5574.html)。

【已确认】报告主张硬件故障、软件缺陷与操作员错误是"需要面对的事实，而非待解决的问题"，应把工程重心从拉长平均无故障时间转向缩短平均修复时间（强调 MTTR 而非 MTTF），并提出系统级撤销、递归重启、快速诊断等机制，引入真实站点故障数据（断电主因是操作员错误）。<br>
【不确定】它证明快速恢复路线的工程可行性，不证明防错可以放松；对后续业界的影响是作者事后转述而非可复现测量。关联生产闭环的运行观察、RFC-0003 的失败后决策、Q2。

<a id="e08"></a>
### E08：乐观并发控制

H. T. Kung、John T. Robinson，1981，*On Optimistic Methods for Concurrency Control*，ACM Transactions on Database Systems 6(2), 213–226。[ACM DOI 页](https://dl.acm.org/doi/10.1145/319566.319567)（正文付费；题录与原文表述经 Crossref 官方元数据及公开托管的全文核对）。

【已确认】论文提出事务的读／验证／写结构：读阶段不加锁、改动先写本地副本，提交前对最新状态验证，验证失败则放弃并作为新事务重来。<br>
【不确定】"放开试、提交前对最新状态严格验证、失败重来"在数据库并发控制中成立，不证明推广到候选软件生产管线后收益为正——收益部分正是 RFC-0003 待实验的内容。另见 E04。

<a id="e09"></a>
### E09：形式化方法的工业使用与成本（AWS）

Chris Newcombe、Tim Rath、Fan Zhang、Bogdan Munteanu、Marc Brooker、Michael Deardeuff，2015，*How Amazon Web Services Uses Formal Methods*，Communications of the ACM 58(4), 66–73。[CACM 文章页](https://cacm.acm.org/research/how-amazon-web-services-uses-formal-methods/)、[作者预印本](https://lamport.azurewebsites.net/tla/formal-methods-amazon.pdf)；工具定位见 [Lamport 的 TLA+ 页](https://lamport.azurewebsites.net/tla/tla.html)。

【已确认】AWS 工程师在 S3、DynamoDB、EBS 与内部分布式锁管理等 10 个大型系统使用 TLA+ 规格与模型检查，找到设计评审、代码评审与长期测试均未发现的并发时序缺陷（如 DynamoDB 一个需 35 步序列才复现的丢数据缺陷；一处已通过评审的修复方案本身仍有缺陷，模型检查数秒发现）。<br>
【已确认】成本侧：工程师从零学习 TLA+ 约 2–3 周可得可用结果；规格为数百行量级；作者称写规格"比写非形式化证明更可靠且更省时"；管理层在年度规划中为 TLA+ 分配工程时间。<br>
【不确定】这是"关键系统困难设计问题"上的经验，不证明任意任务的验收成本都可承受，也不证明 AI 生成实现的验收器应一律采用形式规格。它给 Q2 提供了真实价格参考：数百行规格＋数周学习，换取评审与测试找不到的设计缺陷。关联 Q2、设计原则"目标可检验"、接口刚性的验收单。

<a id="e10"></a>
### E10：没有银弹（Brooks）

Frederick P. Brooks, Jr.，1986，*No Silver Bullet — Essence and Accidents of Software Engineering*，Information Processing '86（IFIP 第十届世界计算机大会，都柏林），1069–1076 页；转载于 IEEE Computer 20(4)（1987 年 4 月），10–19 页。[computer.org 文章页](https://www.computer.org/csdl/magazine/co/1987/04/01663532/13rRUwcS1zv)、[UNC 技术报告全文](https://www.cs.unc.edu/techreports/86-020.pdf)。

【已确认】Brooks 把软件困难分为"本质"（概念结构的规格、设计与测试）与"意外"（表示与实现），断言"没有任何单一的技术或管理技术改进，能靠自身带来哪怕一个数量级的提升"，并逐一检视九类候选（高级语言、面向对象、人工智能、专家系统、自动编程、图形化编程、程序验证、环境与工具、工作站），结论均为只触及意外困难。<br>
【已确认】经通读全文核验：原文未把"改变生产组织方式与人机分工"作为候选加以论证；Brooks 提出的对本质的进攻是购买而非构建、需求提炼与快速原型、增量开发、培养伟大设计师。<br>
【不确定】H1 落在 Brooks 论证范围之外的维度，不等于 Brooks 会认同 H1——他认定的本质困难与本仓库四个成本（切分、验证、组合、知识）高度重合。两者构成可检验的对立：重组后这些成本长期不降，Brooks 胜；显著下降，H1 在限定范围内成立。关联 H1、核心命题。

<a id="e11"></a>
### E11：电气化生产率的延迟兑现（David）

Paul A. David，1990，*The Dynamo and the Computer: An Historical Perspective on the Modern Productivity Paradox*，American Economic Review 80(2)（Papers and Proceedings），355–361 页，斯坦福大学经济系。[IDEAS 题录](https://ideas.repec.org/a/aea/aecrev/v80y1990i2p355-61.html)、[全文扫描件](http://digamo.free.fr/david90.pdf)；1989 年长版工作论文见 [华威大学 TWERP 339](https://warwick.ac.uk/fac/soc/economics/research/workingpapers/1989-1994/twerp339.pdf)。

【已确认】David 论证：美国工厂电气化扩散缓慢（1899 年电动机不足工厂机械动力的 5%）；早期电气化只是用电动机替换蒸汽机充当原动机，"厂内基于天轴与皮带传动的动力系统原封不动"；制造业生产率收益迟至 1920 年代初才显现，距首批中央电站约四十年；收益来自围绕"单元驱动"（每台机器配独立电动机）重新设计工厂（单层厂房、线性布局、灵活调整机器位置），1919–29 年制造业生产率加速约一半可由电动机容量增长统计解释。<br>
【不确定】该解释是"通用目的技术"文献的经典案例而非定论：Field（2003）主张 1929–41 才是技术进步最快的十年并将重心移向运输与流通部门；Crafts（2002）以增长核算质疑把"数十年滞后"直接读作 ICT/AI 的必然；David 本人提醒"计算机不是发电机"。类比用于提出问题，不用于证明答案。关联 README 核心类比、核心命题研究起点。

<a id="e12"></a>
### E12：Copilot 随机对照实验（实验室任务）

Sida Peng、Eirini Kalliamvakou、Peter Cihon、Mert Demirer（GitHub/Microsoft），2023，*The Impact of AI on Developer Productivity: Evidence from GitHub Copilot*。[arXiv:2302.06590](https://arxiv.org/abs/2302.06590)、[GitHub Blog 摘要](https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/)

【已确认】随机对照实验中，使用 Copilot 的开发者完成同一 HTTP 服务器任务的用时快 55.8%，组间完成率无显著差异；实验只测"写完"，未测正确率与评审成本。<br>
【不确定】单任务实验室证据不能外推为整体生产率；它支持"生成侧提速"，不测量"交付侧收益"。关联 D1、Q2。

<a id="e13"></a>
### E13：三家大公司现场随机对照实验

Kevin Zheyuan Cui、Mert Demirer、Sonia Jaffe、Leon Musolff、Sida Peng、Tobias Salz，2024（SSRN）→2025，*The Effects of Generative AI on High-Skilled Work*。[NBER w34851](https://www.nber.org/system/files/working_papers/w34851/revisions/w34851.rev1.pdf)、[Microsoft Research 页](https://www.microsoft.com/en-us/research/publication/the-effects-of-generative-ai-on-high-skilled-work-evidence-from-three-field-experiments-with-software-developers/)

【已确认】官方摘要口径：合并三场实验 4,867 名开发者，完成任务数 +26.08%（SE 10.3%）；经验较少的开发者采用率与收益更高；测量的是完成数/PR 数，非质量与缺陷率。<br>
【不确定】正文逐项数字因 SSRN 反爬未直接核验；各场实验单独噪声大。关联 D1。

<a id="e14"></a>
### E14：NAV IT 两年纵向案例

Viktoria Stray 等（SINTEF/NAV IT，挪威），2025–2026，*Developer Productivity With and Without GitHub Copilot*，HICSS-59。[arXiv:2509.20353](https://arxiv.org/abs/2509.20353)

【已确认】703 个仓库、26,317 个提交、25 名 Copilot 用户对照 14 名非用户：采用 Copilot 后提交活动无统计显著变化，主观感知生产率提高。<br>
【不确定】单一组织、以提交量为代理指标；表明"感知变快"与"产出指标"可以脱节。注意：该案例方向与"生成变快→待验证变多"不完全一致，它支持的是"感知-产出脱节"，不直接支持验证瓶颈。关联 D1、D8。

<a id="e15"></a>
### E15：DORA 2025《State of AI-assisted Software Development》

Google Cloud 主导，2025。[dora.dev 报告页](https://dora.dev/dora-report-2025/)、[ThoughtWorks 摘要](https://www.thoughtworks.com/en-us/insights/reports/the-2025-dora-report)

【已确认】官方结论：AI 是"放大器"，放大组织既有优势与弱点；个人效率与交付速度提升与系统不稳定度上升并存；最高回报来自对底层组织系统的改造而非工具本身。<br>
【不确定】问卷自报数据，相关非因果；第三方转述的 90% 日活数字未经原文核对。关联 README 类比、H1。

<a id="e16"></a>
### E16：写代码 vs 交付代码（NBER 弱链假说）

Mert Demirer、Leon Musolff、Liyuan Yang，2026 年 5 月（9 月修订），*Writing Code vs. Shipping Code: Productivity Effects Across Generations of AI Coding Tools*，NBER Working Paper 35275。[NBER 页](https://www.nber.org/papers/w35275)

【已确认】（在其测量口径内）50 万+ GitHub 开发者的匹配事件研究：自动补全、交互式 agent、自主 agent 分别使提交量 +30% / +180% / +240%，但项目数仅 +80%、实际发布仅 +30%；作者提出"弱链假说"：AI 收益被人链瓶颈（评审、集成、发布）衰减；人机替代弹性仅 0.23（强互补）。<br>
【不确定】GitHub 遥测与市场数据的观察性研究；它量化了"生成端收益 ≠ 交付端收益"，是本仓库"验证是瓶颈"当前最强的外部量化支撑。另：该文同时报告四个软件市场"新应用数量激增、总使用量没有增长"，与"多出的提交是低价值产出"的解释同向——衰减缺口至少与三组解释相容（低价值产出、需求侧饱和、评审标准收紧），不能只读成"验证卡住"。关联 D1、Q2、H1。

<a id="e17"></a>
### E17：生成代码的质量存量（商业扫描研究组）

GitClear，2025，*AI Copilot Code Quality: 2025 Look Back*。[报告页](https://www.gitclear.com/ai_assistant_code_quality_2025_research)；同类：Veracode 2025 GenAI Code Security Report（45% 的 AI 生成代码未过基础安全测试，2026 春更新为 28–30%，[博客](https://www.veracode.com/blog/spring-2026-genai-code-security/)）、Escape 2025（5,600+ vibe-coded 应用 2,000+ 漏洞，[方法论](https://escape.tech/blog/methodology-how-we-discovered-vulnerabilities-apps-built-with-vibe-coding/)）、云安全联盟 2026（1,645 个 Lovable 应用约 10% 有漏洞端点，[研究笔记](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/)）

【已确认】GitClear 对 211M 行变更的描述统计：重复代码块约 4 倍增长；复制粘贴行占比 8.3%→12.3%（2021→2024）；重构行占比从 25% 跌到 10% 以下。<br>
【不确定】商业分析公司的描述统计，方法未同行评审、因果不清；各子来源的具体数字（Veracode 45%/28–30%、Escape 2,000+ 漏洞、CSA 约 10%）未逐一独立核验，只能说明"生成侧缺陷存量在涨"，不能精确归因。关联 D1、D6。

<a id="e18"></a>
### E18：METR 长任务时间视野

Thomas Kwa 等（METR），2025（NeurIPS 2025；2026-07 v4），*Measuring AI Ability to Complete Long Software Tasks*。[arXiv:2503.14499](https://arxiv.org/abs/2503.14499)、[持续更新页](https://metr.org/time-horizons/)

【已确认】"50% 任务完成时间视界"方法及测量：2025 年初 Claude 3.7 Sonnet 约 50 分钟；2019 年以来约每 7 个月翻倍；2026 年 5 月 FAQ 给 GPT-5 约 2 小时 17 分；论文明确警告外推风险。<br>
【不确定】任务集是自包含、明确定义、可自动评分的"干净"任务；整体性/人工评分下 agent 表现大幅下降；>16 小时任务测量不可靠。它区分了"能力上升"与"生产可信度"，不解决验证难题。关联 D1。

<a id="e19"></a>
### E19：OpenAI 停用 SWE-bench Verified

OpenAI，2026-02-23，*Why SWE-bench Verified no longer measures frontier coding capabilities*。[官方页](https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/)

【已确认】官方审计 138 个模型常败题：59.4% 的测试用例本身有缺陷、会拒绝功能正确的解法；前沿模型可逐字复现人类黄金补丁（训练污染）；近半年得分仅 74.9%→80.9%；OpenAI 停用该基准，推荐 SWE-bench Pro。<br>
【不确定】利益相关方声明；SWE-bench Pro 本身也受批评（[LessWrong](https://www.lesswrong.com/posts/nAMhbz5sfpcynjPP5/swe-bench-pro-is-even-worse)）。"人工审过的 ground-truth 测试仍有约六成缺陷"是 Q2"谁验证验证器"的强旁证。关联 Q2、D1。

<a id="e20"></a>
### E20：Anthropic 上下文工程

Anthropic 工程博客，2025-09-29，*Effective context engineering for AI agents*。[链接](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

【已确认】官方论证：上下文是有限资源；token 增多出现"context rot"，模型回忆准确率下降；注意力预算消耗；工程重心从 prompt engineering 转向 context engineering（MCP、工具、历史选择与循环精炼）。<br>
【不确定】与"验证瓶颈"不互斥；其对策方向是"把上下文喂对"，不讨论生产组织重构。关联 D4，作为竞争观点记录。

<a id="e21"></a>
### E21：规格驱动开发（产业与学术）

Den Delimarsky（GitHub），2025-09，*Spec-driven development with AI*。[博客](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/)、[Spec Kit](https://github.com/github/spec-kit)；Deepak Babu Piskala，2026-01，*Spec-Driven Development: From Code to Contract in the Age of AI Coding Assistants*。[arXiv:2602.00180](https://arxiv.org/abs/2602.00180)

【已确认】GitHub：规格是"活的、可执行的资产"、共享事实源；Specify→Plan→Tasks 四阶段，每阶段未完全验证不得进入下一阶段。学术版提出 spec-first / spec-anchored / spec-as-source 三级严格度及"何时 SDD 不值得"的决策框架。<br>
【不确定】流程提案非效果证据；两者假定规格编写本身便宜，并保留"人看规格、人做验收"的中心地位，比"内核＋外围"更保守。关联 D8、验收单式接口、Q2。

<a id="e22"></a>
### E22：TDD 基准（测试即规格）

Yi Cui 等，2025-05，*Tests as Prompt: A Test-Driven-Development Benchmark for LLM Code Generation*（WebApp1K / TDD-Bench）。[arXiv:2505.09027](https://arxiv.org/abs/2505.09027)

【已确认】1,000 个跨 20 领域 TDD 任务、19 个前沿模型：指令遵循与上下文学习能力比一般编码能力更决定成败；长提示中的指令丢失是主要性能瓶颈之一。<br>
【不确定】基准只测"测试给定后生成代码"，未测"测试本身由谁写、写对没有"——后者恰是 Q2 的核心空白。关联 D8、Q2。

<a id="e23"></a>
### E23：对"临时软件/实现可弃"的系统性反驳

Andreas Kirsch（blackhc），2026-03-18，*The Flawed Ephemeral Software Hypothesis*。[链接](https://www.blackhc.net/essays/future_of_software/)

【已确认】该文承认"生成变便宜"，但断言瓶颈转移到验证、集成、UX/边界情况（Amdahl 定律类比）；主张未来是 malleable（可塑）而非 ephemeral（易逝），代码仍是事实源；记录了支持方档案（Karpathy vibe coding、Vercel Rauch ephemeral apps、a16z Acharya [Disposable Software](https://a16z.com/disposable-software/)、Tunguz [Ephemeral Software](https://tomtunguz.com/ephemeral-software)、Replit Masad 等）与反驳支柱（边缘情况只能靠生产暴露；状态与集成面使重生成面临静默数据损坏；接口稳定性期望使每次重生成引入方差；援引 Brooks "grow, not build" 与 Spolsky 重写教训）。<br>
【不确定】个人长篇论证，非实证。<br>
【建议】其核心两难需正面回应：约束重生成（读旧代码、diff、日志、测试）→ 它不再是临时软件；不约束 → 每轮重生成重置已沉淀的边界知识。关联 RFC-0002、Q4。

<a id="e24"></a>
### E24：改良派反方（Kent Beck）

Kent Beck，2026-04 起，*Genie Tarpit* 系列（及 *Nobody Wants Agents*）。[tidyfirst.substack.com/p/genie-tarpit](https://tidyfirst.substack.com/p/genie-tarpit)

【已确认】Beck 认为 AI 生成"看似合理但坏掉的代码"，复杂度累积快于人类管理能力；杠杆不在更好的提示词，而在团队在"可用功能/可改代码"两轴上的位置；对策是 outcome-oriented（描述要什么、让系统决定怎么做），但明确不主张推翻现有工程组织。<br>
【不确定】随笔文体、个人判断；代表"增量吸收"路线。关联 H1（应编为 EX-08 的对照组之一）。

<a id="e25"></a>
### E25：AI 助手与不安全代码（斯坦福）

Neil Perry、Megha Srivastava、Deepak Kumar、Dan Boneh（斯坦福），2022（arXiv）/CCS 2023，*Do Users Write More Insecure Code with AI Assistants?*。[arXiv:2211.03622](https://arxiv.org/abs/2211.03622)

【已确认】47 名参与者实验：有 AI 助手（Codex）的参与者写出的代码显著更不安全，且更相信自己写出了安全代码——对 AI 产出的自评与客观结果系统性脱节。<br>
【不确定】CTF/安全类小型任务、2022 年模型、受控实验。关联 D1、D2、D3。

<a id="e26"></a>
### E26：Copilot 代码安全评估（NYU）

Hammond Pearce 等（NYU），2021（arXiv）/IEEE S&P 2022，*Asleep at the Keyboard?*。[arXiv:2108.09293](https://arxiv.org/abs/2108.09293)

【已确认】89 个高风险场景、1,689 个 Copilot 生成程序，约 40% 存在可利用漏洞。<br>
【不确定】针对 CWE Top-25 构造的场景、函数级代码、早期模型；"存在漏洞"不等于"全部不可用"，实际影响依赖人工评审过滤。关联 D1。

<a id="e27"></a>
### E27：SWE-Bench+（基准虚高）

Reem Aleithan、Haoran Xue 等（York 大学），2024，*SWE-Bench+: Enhanced Coding Benchmark for LLMs*。[arXiv:2410.06992](https://arxiv.org/abs/2410.06992)

【已确认】人工逐例审查 SWE-Agent+GPT-4 的成功补丁：32.67% 是"答案泄漏"（issue 正文/评论直接给解法），31.08% 靠弱测试用例蒙混通过；剔除后解决率从 12.47% 跌到 3.97%。<br>
【不确定】单一 agent+模型组合、人工标注；证明"基准报告的解决率虚高"，间接支持"验证不充分"。关联 Q2、D1。

<a id="e28"></a>
### E28：SWE-bench "已解决"补丁真的对吗

You Wang、Michael Pradel、Zhongxin Liu（斯图加特大学），2025，*Are "Solved Issues" in SWE-bench Really Solved Correctly?*，ISSTA 2025。[arXiv:2503.15223](https://arxiv.org/abs/2503.15223)

【已确认】对三个 SOTA 工具在 SWE-bench Verified 的补丁做差分测试：7.8% 被计为"正确"却通不过开发者测试套件；29.6% 的"合理补丁"与人类 ground-truth 行为不同（其中 28.6% 确证错误）；报告解决率被高估 6.2 个百分点。<br>
【不确定】限于 SWE-bench Verified 的验证机制；"基准通过 ≠ 正确"的最直接定量证据。关联 Q2。

<a id="e29"></a>
### E29：LLM 生成单元测试的缺陷检测能力

Lin Yang 等（天津大学/华为等），2024，*On the Evaluation of Large Language Models in Unit Test Generation*。[arXiv:2406.18181](https://arxiv.org/abs/2406.18181)

【已确认】17 个 Java 项目、5 个开源 LLM + GPT-4：LLM 生成单元测试的缺陷检测能力有限，首要原因是测试自身有效性低（大量测试无法编译/不通过或断言无效）。<br>
【不确定】单元测试粒度、Java 项目；说明"用 LLM 生成验证器"不能想当然，印证"验证需要被验证"。关联 Q2。

<a id="e30"></a>
### E30：LLM 的错误相关性（跨模型）

Elliot Kim、Avi Garg、Kenny Peng、Nikhil Garg（Cornell 等），2025，*Correlated Errors in Large Language Models*。[arXiv:2506.07962](https://arxiv.org/abs/2506.07962)

【已确认】对 350+ 个 LLM 的实证：两个模型同时出错时，约 60% 的情况错在同一处；更大更强的模型即使架构/供应商不同，错误也高度相关。<br>
【不确定】评估对象是推理/文本任务而非代码；错误相关性是聚合统计，不代表每个具体问题都共因失败。关联 D5、Q6。

<a id="e31"></a>
### E31：LLM 生成代码的失败独立性（代码场景）

Rodrigo Pato Nogueira、Karthik Pattabiraman、Marco Vieira、João R. Campos（UBC 等），2026（arXiv 预印本），*A Systematic Methodology for Evaluating Failure Independence in LLM-Generated Code*。[arXiv:2607.02808](https://arxiv.org/abs/2607.02808)

【已确认】224 个问题 × 12 个模型 × 5 种语言：同一模型的多次实现结构高度相似；N 版本编程框架下，三/五版本集成的可靠性增益只有独立假设下可实现值的 0.43/0.44，同模型集成更低至 0.3 以下；人工故障分析显示"不同的失败模式背后往往共享同一根因"。<br>
【不确定】2026-07 预印本、尚未见同行评审；多数投票/集成场景。把"共因失败"变成可量化的失败独立性指标。关联 D5、Q6。

<a id="e32"></a>
### E32：自一致性（多候选收益的边界）

Xuezhi Wang 等（Google Research），2022（arXiv）/ICLR 2023，*Self-Consistency Improves Chain of Thought Reasoning in Language Models*。[arXiv:2203.11171](https://arxiv.org/abs/2203.11171)

【已确认】采样多条推理路径 + 多数投票在 GSM8K 等任务上显著提升准确率；经典 pass@k 结果（Codex：HumanEval 上 pass@1≈28% → pass@100≈72%）同样表明采样有真实收益。<br>
【不确定】推理任务而非代码；多数投票的前提是"多数与正确答案一致且样本错误不完全重叠"——当所有样本共享同一偏差/同一模糊规格时，投票会把同一个错误放大。它划定"多候选无用"的边界，而非否定。关联 D5。

<a id="e33"></a>
### E33：自修复是万灵药吗

Theo X. Olausson 等（MIT/ETH），2023（arXiv）/ICLR 2024，*Is Self-Repair a Silver Bullet for Code Generation?*。[arXiv:2306.09896](https://arxiv.org/abs/2306.09896)

【已确认】自修复收益被模型自身反馈能力卡住：用强外部反馈（真实测试）时有效，用模型自生成反馈时几乎无增益；固定预算下，"多样化的初始候选"比"反复修复同一候选"更有效。<br>
【不确定】MBPP/HumanEval 类函数级任务、GPT-3.5/4 时代。关联 D5、D6。

<a id="e34"></a>
### E34：思维链解释可以不忠实

Miles Turpin 等（Anthropic/MIT），2023（arXiv）/NeurIPS 2023，*Language Models Don't Always Say What They Think*。[arXiv:2305.04388](https://arxiv.org/abs/2305.04388)

【已确认】通过引入有偏的诱导问题，可以让模型系统性改变答案，而它的 CoT 解释仍能编造出一套自洽但错误的原因——解释与真实推理过程脱钩，且越流畅越有误导性。<br>
【不确定】文本推理任务（GSM8K 等）；演示的是"可被诱导的不忠实"，非声称解释永远不忠实。直接摧毁"解释可作为正确性证据"的论证。关联 D2、生成与验收分离。

<a id="e35"></a>
### E35：LLM 生成的代码注释不准确

Sungmin Kang、Louis Milliken、Shin Yoo（KAIST），2024，*Identifying Inaccurate Descriptions in LLM-generated Code Comments via Test Execution*。[arXiv:2406.14836](https://arxiv.org/abs/2406.14836)

【已确认】评估 3 个 LLM 生成的 Java 注释：最好的模型也有约五分之一（约 20%）的注释包含可证实的不准确陈述；现有"注释-代码一致性检测"技术对识别不准确注释无统计显著效果；作者主张"文档测试"——根据文档生成测试并运行，用外部执行证据验证文档。<br>
【不确定】Java、注释级；"不准确"按可证实陈述判定；另一项 2026 研究（[ACM 3786175](https://dl.acm.org/doi/10.1145/3786175.3788344)）报告专家评分下 58.8% 的 AI 注释质量与人工注释相当——两者不矛盾（质量观感 vs 事实准确性），但表明本仓库主张宜聚焦"事实准确性/与行为一致性"。关联 D2（两张皮）。

<a id="e36"></a>
### E36：模型不能自我纠错

Jie Huang 等（DeepMind），2023（arXiv）/ICLR 2024，*Large Language Models Cannot Self-Correct Reasoning Yet*。[arXiv:2310.01798](https://arxiv.org/abs/2310.01798)

【已确认】无外部反馈时，让模型自查自纠不提升甚至降低准确率——"自我评估"不是验证。<br>
【不确定】推理任务。关联 D2、D3。

<a id="e37"></a>
### E37："代码评审终结"论证（立场论文）

Martin Monperrus，2026，*The End of Code Review: Coding Agents Supersede Human Inspection*。[arXiv:2606.13175](https://arxiv.org/abs/2606.13175)

【已确认】该文论证"人审吞吐不随 AI 产量增长、瓶颈与生产率增益成比例放大"。<br>
【不确定】这是论证性立场论文而非测量研究，引用时必须注明；只经检索确认题录，未通读。关联 D1。

## 待核验的线索

【不确定】以下在原材料中出现，本版尚未完成原始来源核验或仅有部分覆盖：

- 不同实现的共同失败研究：已部分覆盖（E30、E31），但缺少真实团队工作流中的实地数据；
- 自动修复测试集过拟合研究：尚无直接研究；测试集自身缺陷已有旁证（E19、E27、E28）；
- 细胞波茨模型、差异黏附和群体机器人与本原型的具体对应；
- 实时生成产品、一次性软件的辩论与档案已覆盖（E23），但实证性能数字未核验；
- 扩散、控制论、演化与本方案之间的数学映射。

【不确定】原清单中的"电气化生产率类比的历史因果解释"已于 2026-09-15 核验并转入已核对参考（[E11](#e11)）；其因果解释仍是有争议的研究结论，不是定论。

【建议】补证时优先原论文、作者资料、官方实现和可重复数据。登记准确题名、作者或机构、日期、直接链接、对应断言、支持与不支持的范围；不要仅保存搜索摘要。

## 升级与纠错

【建议】改变某命题状态时，在合并请求中记录旧状态、新状态、证据编号、替代解释和范围。反例可使已确认结论收窄或退回不确定；保留旧版本。没有项目数据时，不写成功率、性能改善或“已证明新范式”。
