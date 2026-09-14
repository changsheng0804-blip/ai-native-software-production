# AI 原生软件生产 · AI-Native Software Production

[中文](#中文) · [English](#english)<br>
五分钟入口 / Five-minute introduction · v0.2 · 2026-09-14

<a id="中文"></a>
## 中文

## AI 编程现在有点像炼金术吗？

不是说 AI 背后的科学不可靠，而是实际使用起来常有一种“工程方法还没跟上能力”的感觉。

AI 已经能在几分钟里完成过去需要很久的编码工作，但长期使用以后，一些问题会反复出现：

- **写得快，不等于真的对**：生成完成和验证通过是两回事；
- **解释很流畅，不等于解释和代码一致**：一句“已经检查过了”不能替代真实执行；
- **上下文越长，不一定越稳定**：更多信息也可能带来遗忘、混淆和注意力干扰；
- **局部修改可能产生很远的连锁影响**：共享实现和长依赖链让一个小改动变成全局协调；
- **AI 能廉价生成很多候选，但人的审查能力没有同比增长**；
- 当代码生成越来越快，真正稀缺的逐渐变成**验证、知识整理、依赖协调和人的注意力**。

这让我们开始怀疑一个更根本的问题：

> **会不会不是 AI 还不够像程序员，而是我们仍然在强迫一种新的生产者，按照为人类程序员设计的软件工程方式工作？**

这个仓库就是从这个问题开始的。完整故事见 [《我们为什么开始》](研究记录-Research-Notes/我们为什么开始-Why-We-Started.zh-CN.md)。

---

## 也许我们还只是把“蒸汽机”换成了“电动机”

今天很多 AI 编程仍然沿用原来的生产布局：

```text
需求
 ↓
写代码（现在由 AI 帮忙）
 ↓
代码库 / 共享模块 / API / 依赖
 ↓
人工阅读与审查
 ↓
部署
 ↓
出问题再 Debug
```

【推断】真正的变化可能不只是“让 AI 更快地完成原来的步骤”，而是重新设计：

- 什么算一个合适的生产单元；
- 信息和历史应该放在哪里；
- 怎样验收 AI 的结果；
- 单元怎样组合，才能尽量把错误限制在局部；
- 哪些判断交给机器，哪些判断值得占用人的注意力。

我们并不知道这种新组织方式最终是否成立。这正是这里要验证的事情。

---

## 最开始，我们只想验证两个很小的问题

### 1. 软件一定要靠固定的长调用链和长期代码资产才能完成任务吗？

有没有可能出现一种更临时的产物：用户提出意图，系统即时合成一小段程序、界面或工作流，在隔离环境里完成任务，然后丢弃？

哪怕它只能工作一次，也足以帮助我们检验一个基础假设：**代码必须长期保存和维护，究竟是软件的本质要求，还是过去生产成本下形成的默认方式？**

### 2. 一个功能单元能不能在失败后被重新生成，而不是必须由人逐行 Debug？

最小循环可以只是：

```text
功能目标
  ↓
AI 生成实现
  ↓
真实运行 / 测试
  ↓
失败
  ↓
把失败证据交给 AI
  ↓
修补或重新生成
  ↓
再次验证 / 必要时回滚
```

这不是“自主进化”。目标和边界仍然由外部确定。我们只是想知道：**一个功能单元能不能把“生成—验证—替换”当成正常生命周期。**

---

## 从这些小问题，逐渐长出了更大的研究问题

随着讨论和实验继续，研究对象从“自愈模块”逐渐变成：

> **如果主要生产者变成了擅长生成、但不稳定、上下文受限的 AI，软件生产本身应该如何重新组织？**

目前最关心四件事：

1. **切分成本**：能不能持续把复杂问题切成 AI 容易处理、容易验证的小单元？
2. **验证成本**：生成越来越便宜以后，验证会不会成为新的主要瓶颈？
3. **组合成本**：每个单元单独正确，组合起来是否仍会出现难以局部发现的问题？
4. **知识持续性**：实现可以替换，但业务含义、历史例外和运行经验怎样不一起消失？

---

## 当前形成的原则：它们是阶段性答案，不是起点

【建议】目前值得继续实验的几条原则包括：

- **知识 DRY，实现可以 WET**：业务真相需要权威来源，但具体实现未必必须共享；
- **状态持久，实现可以临时**：事实、身份、规则、权限和证据不应该只存在于某份代码或某次对话里；
- **试错前置，提交严格**：隔离环境中允许大量失败，改变真实状态前严格验证；
- **目标可检验，过程可以变化**：不要求每一步都按预设脚本执行，但结果必须落在可验收范围内；
- **生成与验收分离**：模型对自己工作的解释不能直接当成正确性证据。

这些原则都可能被未来实验修改、收窄或推翻。详见 [设计原则](理论-Theory/设计原则-Design-Principles.zh-CN.md) 和 [核心命题](理论-Theory/核心命题-Core-Thesis.zh-CN.md)。

---

## 我们按三层来验证，而不是直接证明一个“新范式”

### Level 1：这种软件形态能不能存在？

- 临时生成的软件能否完成真实功能？
- 功能单元能否经历“失败 → 修改/重生成 → 测试 → 回滚”？

### Level 2：它在某些局部问题上是否真的更好？

- 更自足的单元是否减少级联影响？
- 外部环境取知识是否比不断堆长上下文更稳定？
- 多候选 + 独立验证是否减少错误进入正式状态？

### Level 3：它能不能形成新的生产组织？

当产品越来越复杂、需求不断变化、历史不断积累时：

> **这种方式能否让人类必须承担的全局协调、审查和救场工作增长得更慢？**

如果最终人仍然需要理解全部代码和全部依赖，那只是把复杂度从编码搬到了集成和审查；如果大部分工作能够长期保持局部、可验证、可替换，生产方式才可能真的发生变化。

---

## 仓库怎么读

| 如果你想看 | 从这里开始 |
|---|---|
| 为什么会开始研究这件事 | [我们为什么开始](研究记录-Research-Notes/我们为什么开始-Why-We-Started.zh-CN.md) |
| 观点是怎样被反例和失败一步步修改的 | [研究演进](研究记录-Research-Notes/研究演进-Research-Evolution.zh-CN.md) |
| 当前比较正式的研究假设 | [核心命题](理论-Theory/核心命题-Core-Thesis.zh-CN.md) |
| 当前设计原则 | [设计原则](理论-Theory/设计原则-Design-Principles.zh-CN.md) |
| 现有实验与下一步计划 | [实验索引](实验-Experiments/实验索引-Experiment-Index.zh-CN.md) |
| 具体提案 | [RFC-0001：知识 DRY / 实现 WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.zh-CN.md) · [RFC-0002：状态持久 / 实现临时](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.zh-CN.md) · [RFC-0003：试错前置 / 提交严格](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.zh-CN.md) |
| 外部证据与反例 | [证据与参考](证据-Evidence/证据与参考-Evidence-and-References.zh-CN.md) |

---

## 研究方式

这里不以“维护一个新范式”为目标，而是尽量保留完整的变化过程：

```text
真实使用中的问题
        ↓
提出猜想
        ↓
最小实验
        ↓
失败 / 反例 / 新观察
        ↓
修改说法
        ↓
再次验证
```

我们使用四类状态区分不同强度的结论：

- **【已确认 / Confirmed】**：有可核验来源或本项目可重复证据；
- **【推断 / Hypothesis】**：由现象推出、但仍待实验；
- **【不确定 / Open】**：证据不足或存在冲突；
- **【建议 / Proposal】**：值得尝试的设计方向。

【不确定】目前还没有证据证明整套组织方式整体优于现有软件工程。失败、无收益和适用范围缩小，同样是有效研究结果。

不会写代码也可以参与：在 [Discussions](https://github.com/changsheng0804-blip/ai-native-software-production/discussions) 提真实体验、反例和问题；在 [Issues](https://github.com/changsheng0804-blip/ai-native-software-production/issues) 跟踪可验证实验。详见 [贡献指南](CONTRIBUTING.md)。

---

<a id="english"></a>
## English

## Why can AI programming feel a little like alchemy?

Not because the underlying science is unserious, but because the engineering methods often feel less mature than the capability itself.

AI can now produce in minutes what used to take much longer, yet repeated use exposes a familiar set of problems:

- **fast generation is not the same as correctness**;
- **a fluent explanation is not the same as evidence that the code actually behaves as claimed**;
- **more context does not always mean more reliability**; it can also create omission, confusion, and attention noise;
- **local edits can trigger distant effects** through shared implementation and long dependency chains;
- **AI can cheaply generate many candidates, while human review capacity does not scale at the same rate**;
- as generation becomes cheaper, the scarce resources increasingly look like **validation, knowledge organization, dependency coordination, and human attention**.

That led to a more fundamental question:

> **What if the problem is not only that AI is not yet enough like a programmer? What if we are still forcing a new kind of producer into a software-production system designed around human programmers?**

This repository starts from that question. Read the full story in [Why we started](研究记录-Research-Notes/我们为什么开始-Why-We-Started.en.md).

---

## Maybe we have only replaced the steam engine with an electric motor

A great deal of AI programming still preserves the old production layout:

```text
requirement
   ↓
write code (now with AI)
   ↓
codebase / shared modules / APIs / dependencies
   ↓
human review
   ↓
deploy
   ↓
debug when something breaks
```

[Hypothesis] The larger opportunity may be to reorganize more than the typing step:

- what counts as a useful unit of production;
- where information and history live;
- how AI output is accepted;
- how units compose while keeping failures local where possible;
- which decisions machines should handle and which deserve human attention.

We do not yet know whether such a reorganization will work. That is what this project is trying to test.

---

## We began with only two small questions

### 1. Does useful software always require a fixed long call chain and long-lived code assets?

Could a user express an intent, have the system synthesize a small program, interface, or workflow, run it in isolation, deliver the result, and then discard it?

Even a single-use artifact would help test a basic assumption: **is long-term code maintenance intrinsic to software, or partly a consequence of historical production costs?**

### 2. Can a functional unit be regenerated after failure instead of always being debugged line by line by a human?

A minimal loop is enough:

```text
functional goal
      ↓
AI generates implementation
      ↓
real execution / tests
      ↓
failure
      ↓
feed failure evidence back to AI
      ↓
repair or regenerate
      ↓
validate again / rollback when needed
```

This is not autonomous evolution. The goal and boundaries remain externally defined. The question is simply whether **generate → validate → replace** can become a normal lifecycle for a software unit.

---

## Those small questions grew into a larger one

As the discussion and experiments continued, the subject expanded beyond self-healing modules:

> **If the main producer becomes an AI that is excellent at generation but stochastic and context-limited, how should software production itself be reorganized?**

Four problems now matter most:

1. **Decomposition cost:** can complex work be kept in units that AI can handle and validate locally?
2. **Validation cost:** as candidates become cheap, does validation become the new bottleneck?
3. **Composition cost:** can individually acceptable units still fail in combination?
4. **Knowledge continuity:** if implementations are replaceable, how do business meaning, historical exceptions, and operational experience survive?

---

## Current principles: outcomes of the exploration, not starting assumptions

[Proposal] Several ideas are now worth testing further:

- **Knowledge DRY; implementations may be WET:** business truth needs an authoritative source, while concrete implementation does not always need to be shared;
- **Persistent state; potentially ephemeral implementation:** facts, identity, rules, permissions, and evidence should not live only inside one code artifact or one conversation;
- **Speculate before commitment; commit strictly:** allow many failures in isolation, verify carefully before changing authoritative state;
- **Testable outcomes; flexible processes:** the path may vary, but acceptable outcomes must remain checkable;
- **Separate generation from acceptance:** the generator’s explanation is not sufficient evidence of correctness.

These may be revised, narrowed, or rejected by future experiments. See the [Design principles](理论-Theory/设计原则-Design-Principles.en.md) and [Core thesis](理论-Theory/核心命题-Core-Thesis.en.md).

---

## Three levels of validation, not one grand proof

### Level 1: can this software shape exist?

- can temporary generated software complete a real task?
- can a unit go through “failure → repair/regeneration → test → rollback”?

### Level 2: is it better for some local problems?

- do more self-contained units reduce cascading change impact?
- is retrieving knowledge from an external environment more stable than continually expanding conversation context?
- do multiple candidates plus independent validation reduce the rate at which errors reach authoritative state?

### Level 3: can it become a different production organization?

As products grow, requirements change, and history accumulates:

> **Can this organization keep the amount of global coordination, review, and rescue work that humans must perform growing more slowly?**

If humans still need to understand all code and all dependencies, complexity has merely moved from coding to integration and review. If most work can remain local, testable, and replaceable, the production model may actually have changed.

---

## How to read this repository

| If you want to understand | Start here |
|---|---|
| Why this research started | [Why we started](研究记录-Research-Notes/我们为什么开始-Why-We-Started.en.md) |
| How observations and failures changed the ideas | [Research evolution](研究记录-Research-Notes/研究演进-Research-Evolution.en.md) |
| Current formal hypotheses | [Core thesis](理论-Theory/核心命题-Core-Thesis.en.md) |
| Current design principles | [Design principles](理论-Theory/设计原则-Design-Principles.en.md) |
| Existing experiments and next steps | [Experiment index](实验-Experiments/实验索引-Experiment-Index.en.md) |
| Concrete proposals | [RFC-0001: Knowledge DRY / implementation WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.en.md) · [RFC-0002: Persistent state / ephemeral implementation](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.en.md) · [RFC-0003: Speculate before commitment](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.en.md) |
| Evidence and counterexamples | [Evidence and references](证据-Evidence/证据与参考-Evidence-and-References.en.md) |

---

## Research method

The repository is meant to preserve the full loop rather than defend a “new paradigm”:

```text
real usage problem
      ↓
hypothesis
      ↓
minimal experiment
      ↓
failure / counterexample / new observation
      ↓
revised claim
      ↓
new test
```

We use four status labels:

- **Confirmed / 已确认**: supported by verifiable sources or repeatable project evidence;
- **Hypothesis / 推断**: inferred from observations but still awaiting tests;
- **Open / 不确定**: evidence is incomplete or conflicting;
- **Proposal / 建议**: a design direction worth trying.

[Open] We currently have no evidence that the overall production model is superior to established software engineering. Failure, no benefit, or a narrower scope are all valid research outcomes.

You do not need to write code to contribute: bring real experiences, counterexamples, and questions to [Discussions](https://github.com/changsheng0804-blip/ai-native-software-production/discussions), and track testable experiments in [Issues](https://github.com/changsheng0804-blip/ai-native-software-production/issues). See [Contributing](CONTRIBUTING.md).
