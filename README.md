# AI 原生软件生产 · AI-Native Software Production

[中文](#中文) · [English](#english)  
五分钟入口 / Five-minute introduction · v0.3 · 2026-09-14

<a id="中文"></a>
## 中文

## AI 编程现在有点像炼金术吗？

这里说的“炼金术”，不是说 AI 背后的科学不可靠。恰恰相反，模型本身建立在现代机器学习、统计与优化之上。

这种“炼金术感”来自实际使用：**能力已经很强，但稳定的工程方法似乎还没有跟上。**

AI 可以在几分钟里完成过去需要很久的编码工作，但长期使用以后，一些体验会反复出现：

- 写得很快，不等于真的对；
- 解释得很流畅，不等于解释和实际代码一致；
- 上下文塞得越来越多，不一定越来越可靠，反而可能更混乱；
- 一个看起来很局部的修改，可能沿着共享模块和依赖链影响很远；
- AI 可以廉价地产生很多候选，但人的审查能力没有同比增长；
- 代码越来越容易生成以后，真正稀缺的反而变成了验证、知识整理、依赖协调和人的注意力。

于是问题逐渐从：

> **“怎么让 AI 更像一个靠谱的程序员？”**

变成了另一个更不舒服的问题：

> **“会不会不是 AI 还不够像程序员，而是我们仍然在强迫一种新的生产者，按照为人类程序员设计的软件工程方式工作？”**

这个仓库就是从这里开始的。完整的思考过程见 [《我们为什么开始》](研究记录-Research-Notes/我们为什么开始-Why-We-Started.zh-CN.md)。

---

## 电动机出现以后，为什么工厂没有立刻变得更高效？

这可能是整个研究里最重要的一个类比。

电力刚普及的时候，很多工厂主只是把蒸汽机换成了电动机，却保留了蒸汽时代的整个空间布局：一个巨大的中央动力源，通过传动轴和皮带轮把动力“分发”到各台机器。

结果效率提升很有限。因为组织生产的**逻辑**没有变，只是动力来源变了。

真正的飞跃发生在后来：工程师逐渐意识到，电动机可以做得足够小、足够便宜，于是可以给**每一台机器单独配一个电动机**。中央传动轴不再是必须存在的东西，机器可以按照工作流程本身重新排列，工厂的空间、节奏和责任边界都随之改变。

电力真正改变的，不只是“动力从哪里来”，而是：

> **当新的动力源拥有和旧动力源完全不同的特性时，整个工厂应该怎样重新组织。**

【推断】今天很多 AI 编程可能还处在类似的阶段：

```text
原来的软件生产流程
+
把“人写代码”换成“AI 帮忙写代码”
```

IDE、代码库、共享模块、API、Git、人工审查、Debug、发布流程基本没变。

这就像：

> **把蒸汽机换成电动机，却还保留整套中央传动轴。**

真正的问题可能不是“怎样让电动机更像蒸汽机”，而是：

> **如果 AI 的生产特性和人类根本不同，软件这座工厂是不是也应该重新布局？**

---

## 那么，生成式 AI 到底有哪些“不同的生产特性”？

在回到软件之前，我们先看那些 AI 已经表现得比较自然的领域。这个过程带出了五个方向。它们不是结论，而是帮助我们摆脱“只把 AI 当更快的人”这一前提的思考实验。

### 方向一：从“版本”变成“谱系”

传统工业产品习惯 v1、v2、v3：后一版替代前一版。

但生成式 AI 的每次输出更像一次独立采样。同一个目标可以长出许多不同但都可用的结果。

【推断】更自然的组织方式也许不是只保留“当前正确版本”，而是保留一片**生成谱系**：哪些分支从哪里长出来，哪些被淘汰，哪些值得嫁接，哪些在特定场景更好。

人的工作因此可能从“把 v1 修改成 v2”，逐渐转向“在大量可能性中选择、组合和继续投入”。

### 方向二：从“完工”变成“持续生成”

传统产品有一个明确的完成时刻。但如果生成本身足够便宜，一部分产品可能根本没有固定终版。

页面可以在点击时生成，故事可以在阅读时继续长出来，界面可以针对当前任务临时出现。

【推断】“作品是什么”可能从一个固定物，变成一个**持续响应环境的过程**。

### 方向三：审核从“对不对”变成“值不值得继续”

工业质检通常拿结果和蓝图比较：偏差多少、是否合格。

生成式结果经常没有唯一蓝图。于是审核的一部分工作可能变成：

> 这一支值得继续投入吗？应该停在这里，还是继续生成？

这更像策展、猎头或风险投资，而不是传统质检。

### 方向四：低边际成本允许“故意浪费”

过去同时做一百个方案最后只留一个，是极其昂贵的浪费。

但如果候选生成足够便宜，**大量试错后筛选**可能反而成为合理流程。

图像生成里“一次出几张、挑一张”只是最初级的样子。更激进的版本可能是：先制造很多平行可能性，再把资源集中到少数真正值得继续的分支上。

### 方向五：人的稀缺能力可能变成“把品味和意图说清楚”

如果生产本身越来越便宜，那么更稀缺的可能不是“亲手把东西做出来”，而是：

> **知道自己到底想要什么，并能把模糊的感觉变成足够清晰的约束。**

这种能力现在散落在产品经理、艺术总监、编辑、编剧顾问等工作里，但很少被单独当成一门工程能力来讨论。

---

## 几个现实案例让这件事突然具体起来

讨论过程中，有三个案例尤其重要：**Flipbook、MiniMax H3 AI 电视台，以及 AICG 内容生产中的“抽卡式”工作流。**

我们并不把它们当成“新软件架构已经成立”的证明。它们更像三个窗口，让一些共同特征变得可见：

1. **消费行为直接进入下一轮生成。** 点击、弹幕、选择不只是结果之后的反馈，而会立刻成为下一次生成的输入。
2. **不需要完整预先规划，只需要轻量锚点维持连续。** 例如上一帧、世界观、角色设定、当前页面上下文。
3. **作品从固定成品变成持续过程。** “什么时候算做完”开始变得模糊。

这三个案例还暴露出另一个更底层的共同点：

> **它们都允许把生产拆成很多相对独立的小单元，而且某一个单元失败的代价不高。**

于是我们提出了一个早期诊断框架：

> **离散度越高 + 容错率越高，生成式 AI 越容易自然地发挥优势。**

这不是最终模型。后来的讨论又补上了可验证性、可逆性、错误相关性等维度。但“离散化 + 容错”第一次让我们看见了一个可能非常重要的方向。

---

## 也许“离散化 + 容错”才是电动机时代的工厂布局

传统流水线要求每一步都尽量正确，因为下一步依赖上一步的精确输出：

```text
A → B → C → D → E
```

B 错了，C 往后可能全部被污染。

而生成式 AI 的一个现实特征是：它很强，但不能保证“每一步都绝对正确”。

那么一个值得认真考虑的推论就是：

> **如果生产者本身具有随机性，把它塞进长而紧的依赖链，也许天然就会处处碰壁。**

相反，如果可以把工作拆成：

```text
单元 A   单元 B   单元 C   单元 D
  ↓        ↓        ↓        ↓
独立尝试  独立失败  独立验证  独立替换
```

那么一次失败就不一定要拖垮整条链。

【推断】这可能正是为什么 AI 在短视频、插画、互动内容等**低耦合、高容错**场景中显得格外顺，而在大型软件、金融核心逻辑等**高耦合、低容错**场景中显得特别别扭。

这也让“电力革命”的类比第一次和软件问题接上：

> **离散化、局部自治和容错，也许就是“每台机器一台电动机”在 AI 软件里的对应物；而紧耦合的长调用链，可能更像中央传动轴。**

我们还不知道这是否正确。但它终于变成了可以实验的问题。

---

## 所以一开始，我们只想验证两个很小的问题

不是先发明“下一代软件工程”，也不是先做一个完整的自愈系统。

### 1. 软件一定要靠固定的长期代码和刚性的长调用链才能完成任务吗？

有没有可能出现一种临时的软件产物：用户提出意图，系统即时合成一小段程序、界面或工作流，在隔离环境中完成任务，然后结束甚至被丢弃？

哪怕它只能工作一次，也足以帮助我们检验：

> **“代码必须长期存在并被持续维护”，究竟是软件的本质要求，还是过去生产成本下形成的默认方式？**

### 2. 一个功能单元能不能在失败后被重新生成，而不是必须由人逐行 Debug？

我们先不要求它自主进化，也不要求它自己判断什么时候“生病”。只要求一个最小闭环：

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
修补 / 重新生成
  ↓
再次验证
  ↓
必要时回滚
```

如果连这两件小事都做不到，后面的宏大理论没有意义。

如果它们可以工作，我们才有理由继续问：这些单元能否组合、能否继承历史、能否在长期演进中真的减少人的全局协调。

---

## 到这里，才逐渐长出现在这些原则

这些不是起点，而是阶段性推论：

- **知识 DRY，实现允许 WET**：业务真相需要权威来源，但具体实现未必必须共享；
- **状态持久，实现可临时**：事实、身份、规则、历史不能随着某份代码一起消失；
- **试错前置，提交严格**：隔离环境里可以大量失败，真正改变现实状态前必须严格验证；
- **目标可检验，过程可变化**：不要求每一步都按固定脚本执行，但最终结果必须落在可验收范围内；
- **环境保存知识，AI 按需获取**：不要把系统记忆等同于无限拉长对话历史。

详见 [核心命题](理论-Theory/核心命题-Core-Thesis.zh-CN.md) 与 [设计原则](理论-Theory/设计原则-Design-Principles.zh-CN.md)。

---

## 我们现在怎么验证？

研究分三层，不从“大一统理论”开始。

### Level 1：这种软件形态存在吗？

先验证最小可行性：临时生成的软件能否完成真实任务？功能单元能否经历“失败 → 重写/重生 → 验证 → 回滚”？

### Level 2：它在某些局部问题上更好吗？

例如：更自包含的实现能否减少级联修改？从环境按需取知识是否比不断塞长上下文稳定？多候选 + 独立验证是否能减少错误进入正式状态？

### Level 3：它最终能形成不同的软件生产组织吗？

当产品越来越复杂、需求持续变化、历史不断积累以后，人是否仍然必须理解全部代码、协调全部依赖、处理全部异常？

如果答案仍然是“必须”，那只是把复杂度从编码搬到了审查和集成。

如果大部分工作可以长期维持在局部、可验证、可替换的范围里，而人主要处理目标、冲突和真正的新问题，那么生产方式才可能真的改变。

---

## 当前状态

【已确认】这个仓库已经整理了理论、提案、实验索引和研究演进记录；原始讨论中特别保留了失败、反例和被推翻的判断，因为这些转折本身就是研究结果。

【不确定】我们还没有证明这是一种更好的通用软件生产方式，也没有必要先证明它适用于所有软件。

真正要找的是：

> **是否存在一类真实软件，在相同质量和资源条件下，改变生产单位、验证方式、知识保存和责任分配以后，能持续得到更高有效产出，并显著减少人的全局协调与救场。**

### 从这里继续

| 想了解什么 | 入口 |
|---|---|
| 为什么会走到这里 | [我们为什么开始](研究记录-Research-Notes/我们为什么开始-Why-We-Started.zh-CN.md) · [研究演进](研究记录-Research-Notes/研究演进-Research-Evolution.zh-CN.md) |
| 当前理论 | [核心命题](理论-Theory/核心命题-Core-Thesis.zh-CN.md) · [设计原则](理论-Theory/设计原则-Design-Principles.zh-CN.md) · [生产闭环](理论-Theory/生产闭环-Production-Loop.zh-CN.md) |
| 首批提案 | [知识 DRY / 实现 WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.zh-CN.md) · [状态持久 / 实现临时](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.zh-CN.md) · [试错前置 / 提交严格](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.zh-CN.md) |
| 实验 | [实验索引](实验-Experiments/实验索引-Experiment-Index.zh-CN.md) · [持续演进对照计划](实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.zh-CN.md) |
| 依据与状态 | [证据与参考](证据-Evidence/证据与参考-Evidence-and-References.zh-CN.md) · [来源摘要](证据-Evidence/来源摘要-Source-Digest.zh-CN.md) |

四类认识状态：**已确认 / Confirmed · 推断 / Hypothesis · 不确定 / Open · 建议 / Proposal**。

---

<a id="english"></a>
## English

## Why can AI programming feel a little like alchemy?

“Alchemy” here does not mean the science behind AI is unsound. The models are grounded in modern machine learning, statistics, and optimization.

The alchemy-like feeling is practical: **the capability has advanced faster than the engineering methods around it.**

In real use, the same tensions keep appearing:

- code can be produced extremely fast without being reliably correct;
- fluent explanation does not guarantee that the explanation matches the code;
- more context does not always mean more reliability;
- a local edit can travel surprisingly far through shared modules and dependency chains;
- AI can generate many candidates cheaply, while human review capacity does not scale the same way;
- as generation gets cheaper, validation, knowledge organization, coordination, and human attention become the scarce resources.

So the question gradually changes from:

> **“How do we make AI behave more like a reliable programmer?”**

into:

> **“What if the deeper problem is that we are forcing a new kind of producer into a software-production system designed around humans?”**

That is where this repository begins. See [Why we started](研究记录-Research-Notes/我们为什么开始-Why-We-Started.en.md) for the full story.

---

## Why did electrification fail to transform factories immediately?

This is one of the most important analogies in the project.

When electric power first spread, many factory owners replaced the steam engine with an electric motor but kept the entire steam-era layout: one central power source driving shafts and belts that distributed mechanical power throughout the building.

Productivity gains were limited because the **logic of production had not changed**. Only the source of power had changed.

The larger gains came later, when engineers realized that electric motors could become small and cheap enough to place one directly on each machine. Once the central shaft was no longer necessary, machines could be rearranged around the actual flow of work. The spatial layout, rhythm, and responsibility structure of the factory changed with it.

Electricity mattered not only because it supplied a new source of power, but because:

> **a power source with different physical properties allowed the entire factory to be reorganized.**

[Hypothesis] Much of AI programming today may still look like:

```text
old software-production process
+
replace “human writes code” with “AI helps write code”
```

IDEs, repositories, shared libraries, APIs, review, debugging, and release practices remain largely unchanged.

That resembles replacing the steam engine with an electric motor while keeping the shaft system.

The deeper question is therefore:

> **If AI has fundamentally different production characteristics from humans, should the software factory itself be rearranged?**

---

## What production characteristics are actually different?

Before returning to software, we looked at domains where generative AI already feels comparatively natural. Five directions emerged. They are not conclusions; they are thought experiments that help us stop assuming AI is simply a faster human producer.

### 1. From versions to lineages

Industrial products are organized as v1, v2, v3, with later versions replacing earlier ones.

Generative systems sample many valid possibilities from the same intent. A more natural structure may be a **lineage of variants**: what branched from what, which branches were discarded, which are useful for a specific context, and which deserve further investment or recombination.

### 2. From completion to continuous generation

Traditional products have a clear completion point. If generation is cheap enough, some products may never have a fixed final form.

A page can be generated when clicked, a story can continue when read, and an interface can appear only for the task at hand.

[Hypothesis] A product can shift from a fixed artifact toward a **process that continuously responds to its environment**.

### 3. From “is it correct?” to “is this branch worth continuing?”

Industrial quality control compares an output against a blueprint.

Generative outputs often have no single blueprint. Part of review therefore changes into a different question: should this branch stop, continue, or receive more resources?

That looks more like curation, recruiting, or venture selection than classical inspection.

### 4. Cheap generation enables deliberate waste

Producing one hundred candidates and keeping one is absurdly wasteful when each candidate is expensive.

When candidate generation becomes cheap, **mass experimentation followed by selection** can become rational. Image generation’s “make several, choose one” pattern is only the simplest version of this idea.

### 5. Human scarcity may move toward making taste and intent explicit

If production becomes abundant, a scarcer capability may be:

> **knowing what you actually want and turning a vague preference into constraints that can steer generation.**

That skill exists today across product management, editing, art direction, and creative consulting, but it is rarely treated as a first-class engineering capability.

---

## A few real examples made the pattern concrete

Three examples became especially useful in the discussion: **Flipbook, the MiniMax H3 AI television experiment, and “gacha-style” AIGC production workflows.**

We do not treat them as proof of a new software architecture. They are windows into a few recurring properties:

1. **Consumption becomes part of the next generation input.** A click, comment, or choice directly shapes what is produced next.
2. **Continuity can be maintained with lightweight anchors rather than a complete preplanned artifact.** Previous frames, world rules, characters, or the current page can be enough.
3. **The product becomes a continuing process rather than a fixed final object.**

Another common property then became visible:

> **production is split into relatively independent units, and the cost of one unit failing is often low.**

This led to an early diagnostic frame:

> **The more discrete the production units, and the more failure the domain can tolerate, the more naturally generative AI tends to fit.**

This was never meant to be the final model. Later work adds verifiability, reversibility, and failure correlation. But discreteness and tolerance were the first variables that connected the successful examples back to software.

---

## Maybe discreteness and tolerance are the AI equivalent of “one motor per machine”

A traditional pipeline assumes each stage is dependable because the next stage consumes its precise output:

```text
A → B → C → D → E
```

If B is wrong, everything downstream can be contaminated.

Generative AI is powerful, but it cannot guarantee that every intermediate result is always correct.

That suggests a serious possibility:

> **A stochastic producer may be a poor fit for long, tightly coupled chains by construction.**

A different layout would make work more local:

```text
unit A   unit B   unit C   unit D
  ↓        ↓        ↓        ↓
try       fail      verify    replace
locally   locally   locally   locally
```

[Hypothesis] This may help explain why generative AI often feels unusually natural in low-coupling, high-tolerance domains such as short-form media and illustration, while feeling awkward in tightly coupled, low-tolerance systems such as large software systems or financial core logic.

This is where the factory analogy finally connects back to software:

> **discreteness, local autonomy, and tolerance may be the software equivalent of one electric motor per machine; long dependency chains may be closer to the central shaft.**

We do not yet know whether that analogy survives real experiments. But it gives us something testable.

---

## So we began with only two small questions

We did not start by trying to invent the next software paradigm or a complete self-healing system.

### 1. Does useful software always require long-lived code and rigid call chains?

Could a user express an intent, have a small program, interface, or workflow synthesized for the moment, run it in isolation, get the result, and then discard it?

Even a one-use artifact would test whether “code must be a long-lived maintained asset” is a fundamental requirement or simply a historical default.

### 2. Can a functional unit be regenerated after failure instead of being manually debugged line by line?

No autonomous evolution is required. We only need a minimal loop:

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
repair / regenerate
  ↓
validate again
  ↓
rollback when needed
```

If these two small things do not work, the larger theory is irrelevant.

If they do, we can begin asking whether such units can compose, preserve history, and reduce global human coordination over long periods of change.

---

## Only later did the current principles emerge

These are outcomes of the exploration, not starting assumptions:

- **Knowledge DRY; implementations may be WET** — business truth needs an authoritative source, while concrete implementations need not always be shared;
- **Persistent state; potentially ephemeral implementation** — facts, identity, rules, and history should survive implementation replacement;
- **Speculate before commitment; commit strictly** — allow many failures in isolation, but verify carefully before changing authoritative state;
- **Testable outcomes; flexible processes** — the path may vary, but acceptable results must remain checkable;
- **Keep knowledge in the environment; let AI retrieve it as needed** — system memory should not mean infinitely extending a conversation transcript.

See the [core thesis](理论-Theory/核心命题-Core-Thesis.en.md) and [design principles](理论-Theory/设计原则-Design-Principles.en.md).

---

## How are we testing this?

The research has three levels.

### Level 1: can this software shape exist at all?

Can temporary generated software complete a real task? Can a functional unit repeatedly go through failure → repair/regeneration → validation → rollback?

### Level 2: is it better for some local problems?

Can more self-contained implementations reduce cascading change? Is retrieving knowledge from an external environment more stable than stuffing everything into long context? Can multiple candidates plus independent validation reduce errors reaching authoritative state?

### Level 3: can it become a different production organization?

As the product grows, requirements change, and history accumulates, do humans still need to understand all code, coordinate all dependencies, and rescue all exceptions?

If yes, complexity has merely moved from coding into integration and review.

If most work can remain local, testable, and replaceable while humans focus on goals, conflicts, and genuinely new problems, then the production model may actually have changed.

---

## Current status

[Confirmed] This repository now preserves theory, proposals, experiment indexes, and the evolution of the discussion. Failed experiments and rejected ideas are intentionally retained because the corrections are part of the research result.

[Open] We have not established that this is a generally better way to build software, and we do not need to prove that it applies to all software.

The real target is narrower:

> **Is there a meaningful class of software where changing the unit of production, validation, knowledge retention, and responsibility allocation repeatedly produces more accepted functionality with substantially less global human coordination and rescue work?**

### Continue reading

| Interest | Entry points |
|---|---|
| Why this started | [Why we started](研究记录-Research-Notes/我们为什么开始-Why-We-Started.en.md) · [Research evolution](研究记录-Research-Notes/研究演进-Research-Evolution.en.md) |
| Current theory | [Core thesis](理论-Theory/核心命题-Core-Thesis.en.md) · [Design principles](理论-Theory/设计原则-Design-Principles.en.md) · [Production loop](理论-Theory/生产闭环-Production-Loop.en.md) |
| Initial proposals | [Knowledge DRY / code WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.en.md) · [Persistent state / ephemeral implementation](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.en.md) · [Speculate before commitment](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.en.md) |
| Experiments | [Experiment index](实验-Experiments/实验索引-Experiment-Index.en.md) · [Longitudinal comparison protocol](实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md) |
| Evidence and status | [Evidence and references](证据-Evidence/证据与参考-Evidence-and-References.en.md) · [Source digest](证据-Evidence/来源摘要-Source-Digest.en.md) |

Knowledge-status labels correspond exactly: **已确认 / Confirmed · 推断 / Hypothesis · 不确定 / Open · 建议 / Proposal**.
