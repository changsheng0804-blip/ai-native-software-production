# AI 原生软件生产 · AI-Native Software Production

[中文](#中文) · [English](#english)  
五分钟入口 / Five-minute introduction · v0.4 · 2026-09-14

<a id="中文"></a>
## 中文

## AI 编程现在有点像炼金术

AI 编程已经可以在几分钟里完成过去需要很久的编码工作。但真正长期使用以后，会反复遇到一些很难忽视的体验：

- **解释得很流畅，但解释和实际代码好像是两码事。** 它说“已经修好了”，并不等于真的运行过、验证过；
- **看起来越来越能干，但你总觉得它有一部分是在猜。** 同一个问题换一种说法、换一次上下文，结果可能明显不同；
- **它很擅长继续生成，却不天然擅长停下来删东西。** 一轮轮“修复”经常变成继续加判断、加兼容、加补丁，系统越来越厚；
- **一旦进入你自己也不熟悉的领域，AI 编程很像抽卡。** 你知道它大概率能给出某种东西，却很难提前知道下一步会走向哪里；
- **代码生成越来越快，人的验证速度却没有一起增长。** 最后真正稀缺的，往往变成了验证、知识整理、依赖协调和人的注意力。

所以我们最初的问题是：

> **怎么让 AI 更像一个靠谱的程序员？**

但讨论越往后，一个更不舒服的问题开始出现：

> **会不会不是 AI 还不够像程序员，而是我们仍然在强迫一种新的生产者，按照为人类程序员设计的软件工程方式工作？**

这个仓库就是从这里开始的。更完整的思考过程见 [《我们为什么开始》](研究记录-Research-Notes/我们为什么开始-Why-We-Started.zh-CN.md)。

---

## 电动机出现以后，为什么工厂没有立刻变得更高效？

这可能是整个研究里最重要的一个类比。

电力刚普及的时候，很多工厂主只是把蒸汽机换成了电动机，却保留了蒸汽时代的整个空间布局：一个巨大的中央动力源，通过一根根传动轴、皮带轮把动力“分发”到各台机器。

效率提升很有限，因为组织生产的**逻辑**根本没变，只是换了动力来源。

真正的飞跃发生在后来。工程师逐渐意识到，电动机可以做得足够小、足够便宜，于是可以给**每一台机器单独配一个电动机**。中央传动轴不再是工厂布局的前提，机器可以围绕实际工作流程重新排列，生产空间、节奏、故障边界甚至管理方式都跟着改变。

电力真正释放潜力，不只是因为“动力更先进”，而是因为人们终于开始围绕电动机自己的特性重新设计工厂。

> **新的动力源，如果拥有和旧动力源完全不同的特性，真正的变化往往不是替换动力，而是重排整个生产系统。**

【推断】今天很多 AI 编程可能还停留在第一阶段：

```text
原来的软件生产流程
+
把“人写代码”换成“AI 帮忙写代码”
```

IDE（集成开发环境）、代码库、共享模块、API（应用程序接口）、Git（版本控制）、人工审查、Debug（调试）、发布流程，大体还是原来的布局。

这就像：

> **把蒸汽机换成了电动机，却还保留着整套中央传动轴。**

真正的问题也许不是“怎样让电动机更像蒸汽机”，而是：

> **如果 AI 的生产特性和人类根本不同，软件这座工厂是不是也应该重新布局？**

---

## 先别急着谈软件：生成式生产到底哪里不一样？

要回答这个问题，先得弄清楚 AI 这种“生产者”到底和过去有什么不同。

### 工业生产的核心逻辑：设计一次，复制无数次

工业时代最重要的一次分工，是把“设计”和“制造”彻底分开。

先画图纸、开模具、设计产线——这是一次性、高成本的工作。之后每一件产品都尽量忠实复制同一个蓝图。质量控制也因此非常自然：

> **这件产品和蓝图偏差了多少？**

在这种逻辑里，规模化意味着不断复制；产品之间的差异通常是应该消灭的公差和缺陷。

### 生成式 AI 的逻辑可能正好相反：每次生产都带着一次重新设计

同一个提示词运行两次，结果可以不同。它不是从一个固定母版复制出下一件产品，而是在一个可能性空间里重新采样。

这在工业生产里可能叫“公差超标”，但在图像、文本、音乐等生成任务里，差异本身恰恰是价值的一部分。

于是“设计”和“生产”的界线开始模糊：

> **生成的那一刻，同时也是一次新的设计。**

这也解释了为什么“质检”在生成式 AI 里经常显得别扭。

工业质检问的是“像不像蓝图”；生成式结果更常面对的是另外两类问题：

- **有硬标准的地方：它到底对不对、能不能通过验证？**
- **没有唯一答案的地方：这个结果好不好、值不值得继续？**

两者需要的根本不是同一种审核方式。

### 另一个变化：复杂度和边际生产成本之间的关系变弱了

工业生产里，多一个零件、多一道工序，通常都会直接增加材料、时间和制造成本。

AI 生成当然也有成本，长输出、更多推理、更多验证都会花钱；但和物理制造相比，**“做一个更复杂的候选”不再必然按同样比例变贵**。这让过去因为“太浪费”而不敢采用的工作方式，第一次变得值得重新考虑。

从这里，我们开始推演五个可能的变化方向。

---

## 五个方向：如果不再把 AI 当成“更快的人”

这些都不是结论，而是思考实验。它们的作用，是帮助我们暂时放下传统软件工程的默认前提，看看生成式生产本身可能长成什么样。

### 方向一：从“版本”变成“谱系”

传统产品习惯 v1、v2、v3：后一版替代前一版，历史主要是一条不断向前的线。

但生成式 AI 的每次输出更像一次独立采样。同一个目标可以长出很多不同、甚至都可用的结果。

【推断】更自然的组织方式也许不是只保留一个“当前正确版本”，而是保留一片**生成谱系**：哪些分支从哪里长出来，哪些被淘汰，哪些值得嫁接，哪些只在特定场景里更好。

人的工作也可能从“把 v1 修改成 v2”，逐渐变成“在大量可能性中选择、组合和决定哪一支值得继续投入”。

### 方向二：从“完工”变成“持续生成”

传统产品有一个很清楚的完成时刻：书写完了，电影剪完了，软件版本发布了。

但如果生成足够便宜，一部分产品可能根本没有固定终版。

页面可以在点击时才出现下一层，故事可以在阅读时继续生成，界面可以只为眼前这个任务临时存在。

【推断】“作品”可能从一个固定物，变成一个**持续响应用户和环境的过程**。

### 方向三：审核从“对不对”变成“值不值得继续”

有硬约束的任务仍然需要判断对错；但对于没有唯一蓝图的生成任务，审核会多出另一种角色：

> **这一支值得继续投入吗？应该停在这里，还是继续生成？**

这更像策展人、猎头或者风险投资，而不是传统流水线上的质检员。

【推断】未来很多“编辑、审核、产品”工作，可能会更多地变成对可能性进行资源配置：不是逐件修到一样，而是决定哪一支值得继续长大。

### 方向四：低边际成本允许“故意浪费”

过去同时做一百个方案，最后只留一个，通常意味着极其糟糕的投入产出比。

但如果候选生成足够便宜，**故意制造大量失败，再从中筛选**，可能反而是合理策略。

图像生成里“一次出几张，挑一张”只是最初级的样子。更激进的版本可能是：先生成很多平行世界，再把验证和人的注意力集中到少数真正值得继续的分支上。

### 方向五：人的稀缺能力可能变成“把品味和意图具象化”

如果生产本身越来越便宜，真正稀缺的可能不再只是“把东西亲手做出来”，而是：

> **知道自己到底想要什么，并且能把一种模糊的感觉，转成足够清晰、可以驱动生成和筛选的约束。**

这种能力今天散落在产品经理、艺术总监、编辑、编剧顾问等职业里，但很少被当作一种独立的方法论来训练。

---

## 三个现实案例，让这些推演突然变得具体

讨论过程中，有三个案例尤其重要：**Flipbook、MiniMax H3 AI 电视台，以及 AIGC（人工智能生成内容）生产中的“抽卡式”工作流。**

它们不能证明“新的软件生产方式已经成立”，但它们让几个共同特征突然变得可见：

1. **消费行为直接进入下一轮生产。** 点击、弹幕、选择不只是结果之后的反馈，而会立刻成为下一次生成的输入；
2. **连续性不一定来自完整预先规划，也可以依赖很轻的锚点。** 例如上一帧、世界观、角色设定、当前页面上下文；
3. **作品从固定成品变成持续过程。** “什么时候才算做完”开始变得模糊。

更重要的是，我们开始看到两个反复一起出现的条件。

### 1. 离散：一个单元可以失败，而不会把整条链拖死

在这些案例里，最小生产单元都比较小：一幕、一个页面节点、一张图、一个镜头。

某一幕生成得差，可以跳过或者重来；某一页不理想，可以换一个方向继续；一次“抽卡”失败，本来就是流程预期的一部分。

这和传统紧耦合流水线很不一样：如果下一步必须精确依赖上一步的输出，那么前面一个错误就可能一路传播下去。

### 2. 容错：单个单元不完美，整体仍然可以继续

一个转场有点尴尬、一张图不够准确、一次生成没有抽中好结果，并不会必然让整个体验失败。

甚至有些产品直接把“生成质量不稳定”设计进了交互本身：用户从一开始就知道会试很多次，只挑其中满意的结果。

于是我们得到一个很早期、也很粗糙的诊断框架：

> **生产越容易离散化，单元失败的代价越低，生成式 AI 往往越容易自然地发挥优势。**

---

## 为什么“离散 + 容错”可能比模型大小更重要？

这里需要一个重要修正。

生成式模型的错误并不一定“彼此独立”。同一个模型、同一种提示方式，完全可能反复犯相似的系统性错误。

但它和传统确定程序仍然有一个很现实的区别：**输出具有采样波动，某一次修好并不自动意味着下一次生成永远不会再犯；而且很多错误只有真正运行后才暴露。**

因此，如果一个生产流程要求：

```text
A 必须正确
  ↓
B 才能正确
  ↓
C 才能正确
  ↓
D 才能正确
```

那么一个具有随机性的生产者被放进这样的长链里，错误就很容易积累、传播和放大。

相反，如果结构允许：

```text
单元 A   单元 B   单元 C   单元 D
  ↓        ↓        ↓        ↓
独立尝试  独立失败  独立验证  独立替换
```

一次失败就有机会被限制在局部。

这解释了一个非常直观的现象：

【推断】AI 在短视频、插画、单条文案、局部生成等**低耦合、高容错**场景中往往显得格外顺；而在大型软件、金融核心逻辑、法律关键条款等**高耦合、低容错**场景中，会显得特别别扭。

这也意味着，一个领域要想把 AI 用好，可能不只是“等模型再变强”，还可以主动改变自己的生产结构：

> **能不能把原来必须一次性维持全局正确的问题，重新组织成更小、可独立验收、可独立失败的单元？**

这不是说离散化可以解决一切。后来的讨论又补上了至少三个重要维度：

- **可验证性**：我们能不能低成本判断一个结果是否真的合格？
- **可逆性**：错了以后能不能安全撤销、替换或重来？
- **错误相关性**：多个候选是不是其实在一起犯同一种错？

所以“离散度 + 容错率”不是最终公式，但它第一次让我们看到了一个可能比“模型有多大”更接近生产组织的问题。

---

## 这时候，电力革命的类比重新接了回来

也许：

> **离散化、局部自治和容错，就是“每台机器一台电动机”在 AI 软件里的对应物；而长而紧的依赖链，更像中央传动轴。**

传统软件的很多结构，本来就是在另一组约束下形成的：

- 人写代码很慢，所以要尽量复用；
- 人记忆有限，所以用固定抽象压缩复杂度；
- 修改很贵，所以追求长期稳定的实现；
- 每一步都由确定程序执行，所以可以建立很长的精确调用链。

这些选择在它们产生的时代非常合理。

但如果主要生产者变成了一个**生成很快、可以并行尝试、却有随机性、上下文有限而且需要外部验证**的 AI，那么原来的最优解未必还是最优解。

这可能正是为什么“AI 写代码”比 AI 生成图片、短视频、互动内容更容易让人感到别扭：软件通常恰好是一个**高耦合、低容错、历史状态很多、局部修改容易产生全局影响**的世界。

于是问题终于从抽象类比落回软件：

> **能不能重新设计软件的生产单位，让大部分 AI 工作发生在小而清楚、可以独立运行、独立验证、独立失败的范围里？**

我们还不知道答案。但这已经是一个可以动手实验的问题了。

---

## 所以一开始，我们只想验证两个很小的问题

不是先发明“下一代软件工程”，也不是先做一个完整的自愈系统。

### 1. 软件一定要靠长期存在的固定代码和刚性的长调用链才能完成任务吗？

有没有可能出现一种临时的软件产物：用户提出意图，系统即时合成一小段程序、界面或工作流，在隔离环境里完成任务，然后结束、冻结，甚至直接丢弃？

哪怕它只能工作一次，也足以帮助我们检验：

> **“代码必须长期存在并被持续维护”，究竟是软件的本质要求，还是过去生产成本下形成的默认方式？**

### 2. 一个功能单元能不能在失败后被重新生成，而不是必须由人逐行 Debug（调试）？

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

【已确认】这个仓库已经整理了理论、提案、实验索引和研究演进记录；失败、反例和被推翻的判断会被刻意保留，因为这些转折本身就是研究结果的一部分。

【不确定】我们还没有证明这是一种更好的通用软件生产方式，也没有必要先证明它适用于所有软件。

真正要找的是：

> **是否存在一类真实软件，在相同质量和资源条件下，改变生产单位、验证方式、知识保存和责任分配以后，能持续得到更高的有效产出，并显著减少人的全局协调与救场。**

### 从这里继续

| 想了解什么 | 入口 |
|---|---|
| 为什么会走到这里 | [我们为什么开始](研究记录-Research-Notes/我们为什么开始-Why-We-Started.zh-CN.md) · [研究演进](研究记录-Research-Notes/研究演进-Research-Evolution.zh-CN.md) |
| 当前理论 | [核心命题](理论-Theory/核心命题-Core-Thesis.zh-CN.md) · [设计原则](理论-Theory/设计原则-Design-Principles.zh-CN.md) · [生产闭环](理论-Theory/生产闭环-Production-Loop.zh-CN.md) · [接口刚性](理论-Theory/接口刚性-Interface-Rigidity.zh-CN.md) |
| 首批提案 | [知识 DRY / 实现 WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.zh-CN.md) · [状态持久 / 实现临时](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.zh-CN.md) · [试错前置 / 提交严格](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.zh-CN.md) · [瞬时视觉表层](提案-RFCs/0004-瞬时视觉表层与意图反推-Ephemeral-Visual-Surface.zh-CN.md) |
| 实验 | [实验索引](实验-Experiments/实验索引-Experiment-Index.zh-CN.md) · [持续演进对照计划](实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.zh-CN.md) · [文档生产试验田](实验-Experiments/09-文档生产试验田-Document-Production-Trial-Field.zh-CN.md) |
| 依据与状态 | [证据与参考](证据-Evidence/证据与参考-Evidence-and-References.zh-CN.md) · [来源摘要](证据-Evidence/来源摘要-Source-Digest.zh-CN.md) |

四类认识状态：**已确认 / Confirmed · 推断 / Hypothesis · 不确定 / Open · 建议 / Proposal**。

---

<a id="english"></a>
## English

## AI programming can feel a little like alchemy

AI can now complete in minutes coding work that used to take much longer. But after using it seriously for a while, the same strange tensions keep returning:

- **Its explanations can be fluent while still feeling disconnected from the actual code.** “Fixed” is not the same as executed and verified;
- **It looks increasingly capable, yet part of the process still feels like guessing.** Rephrasing the task or changing the context can send it down a noticeably different path;
- **It is naturally good at adding more output, but not at deciding what should disappear.** Repeated “fixes” often become more conditions, more compatibility layers, and more patches;
- **In a domain you do not understand yourself, AI programming can feel like pulling from a gacha machine.** You expect something plausible to appear, but you cannot reliably predict what the next move will be;
- **Generation speed is scaling faster than human verification speed.** The scarce resources increasingly look like validation, knowledge organization, dependency coordination, and human attention.

So the first question was:

> **How do we make AI behave more like a reliable programmer?**

But the discussion gradually produced a more uncomfortable question:

> **What if the problem is not only that AI is not yet enough like a programmer? What if we are forcing a new kind of producer into a software-production system designed around human programmers?**

That is where this repository begins. See [Why we started](研究记录-Research-Notes/我们为什么开始-Why-We-Started.en.md) for the fuller story.

---

## Why did factories not become dramatically more productive as soon as electric motors arrived?

This may be the most important analogy in the project.

When electricity first spread, many factory owners simply replaced the steam engine with an electric motor while keeping the steam-era layout: one large central power source, with shafts and belts distributing mechanical power to every machine.

The improvement was limited because the **logic of production had not changed**. Only the source of power had changed.

The larger shift came later, when engineers realized that motors could become small and cheap enough to put **one motor on each machine**. The central shaft no longer had to dictate the factory layout. Machines could be arranged around the actual flow of work, and the spatial layout, operating rhythm, failure boundaries, and even management structure could change with them.

Electricity released its real potential not merely because it was “better power,” but because factories were eventually redesigned around the properties of electric motors themselves.

> **When a new source of production has fundamentally different properties, the deepest change may come not from replacing the old source, but from reorganizing the whole production system around the new one.**

[Hypothesis] Much of AI programming today may still be in the first stage:

```text
old software-production process
+
replace “human writes code” with “AI helps write code”
```

IDEs, repositories, shared modules, APIs, Git, human review, debugging, and release practices remain largely inherited from the old layout.

That resembles:

> **replacing the steam engine with an electric motor while keeping the entire shaft system.**

The deeper question may not be “how do we make the motor behave more like a steam engine?” but:

> **If AI has production characteristics that are fundamentally different from humans, should the software factory itself be rearranged?**

---

## Before returning to software: what is actually different about generative production?

To answer that, we first need to ask what kind of producer AI actually is.

### Industrial production: design once, reproduce many times

A defining move of industrial production was separating design from manufacturing.

The blueprint, tooling, and production line were expensive one-time investments. After that, each product was expected to reproduce the same design as faithfully as possible. Quality control therefore had a natural question:

> **How far does this item deviate from the blueprint?**

At scale, variation was usually something to eliminate.

### Generative AI may work in the opposite direction: every act of production includes another act of design

Run the same prompt twice and the result may differ. The system is not simply copying a fixed master; it is sampling again from a space of possibilities.

In industrial manufacturing, that might look like unacceptable variance. In images, writing, music, and other generative tasks, variation is often part of the value.

The boundary between “design” and “production” therefore starts to blur:

> **the act of generating is also another act of designing.**

That helps explain why “quality control” feels awkward in generative systems.

Industrial inspection asks whether the product matches the blueprint. Generative work often has to answer two very different questions:

- **Where hard requirements exist: is this actually correct and verifiable?**
- **Where no single answer exists: is this result good, useful, or worth continuing?**

Those are not the same kind of review.

### Another shift: the relationship between complexity and marginal production cost becomes weaker

In physical manufacturing, an extra part or extra process usually adds direct material and production cost.

AI generation still costs money: longer outputs, more reasoning, more trials, and more validation all consume resources. But compared with physical production, **a more complex candidate does not necessarily become expensive in the same proportion**.

That makes workflows once dismissed as “too wasteful” worth reconsidering.

From here, five possible directions emerged.

---

## Five directions if we stop treating AI as merely a faster human

These are not conclusions. They are thought experiments intended to loosen assumptions inherited from traditional production.

### Direction 1: from versions to lineages

Traditional products are organized as v1, v2, v3: a later version replaces an earlier one, and history is mostly a line.

Generative AI behaves more like repeated sampling. The same intent can produce many different outcomes, several of which may be useful.

[Hypothesis] A more natural structure may be a **generation lineage**: which branch came from which, which branches were discarded, which deserve recombination, and which are better only in a particular context.

Human work may shift from “turn v1 into v2” toward choosing, combining, and deciding which branches deserve more resources.

### Direction 2: from completion to continuous generation

Traditional products have a clear completion point: the book is finished, the film is cut, the software release ships.

If generation becomes cheap enough, some products may never have a fixed final form.

A page may appear only when clicked, a story may continue while it is being read, and an interface may exist only for the task at hand.

[Hypothesis] A “product” may shift from a fixed object toward a **process that continuously responds to users and its environment**.

### Direction 3: from “is it correct?” to “is this branch worth continuing?”

Tasks with hard constraints still require correctness checks. But when there is no single blueprint, review acquires another role:

> **Is this branch worth more investment? Should it stop here, or continue generating?**

That looks more like curation, recruiting, or venture selection than classical factory inspection.

[Hypothesis] Editing, review, and product work may increasingly become resource allocation across possibilities: not making every branch identical, but deciding which branches deserve to grow.

### Direction 4: cheap generation enables deliberate waste

Producing one hundred candidates and keeping one used to be an obviously bad production strategy.

If candidates become cheap enough, however, **deliberately producing many failures and selecting afterward** can become rational.

Image generation’s “make several, choose one” pattern is only the simplest form. A more radical workflow would generate many parallel worlds first, then concentrate validation and human attention on the few branches worth continuing.

### Direction 5: human scarcity may move toward making taste and intent explicit

If production itself becomes abundant, a scarce skill may no longer be only “making the artifact by hand,” but:

> **knowing what you actually want and turning a vague feeling into constraints that can steer generation and selection.**

That capability already exists across product management, art direction, editing, and creative consulting, but it is rarely trained as a distinct discipline.

---

## Three real-world examples made the pattern concrete

Three examples became especially useful in the discussion: **Flipbook, the MiniMax H3 AI television experiment, and gacha-style AIGC production workflows.**

They do not prove that a new software-production model already exists. They are useful because they expose several recurring properties:

1. **Consumption directly enters the next production cycle.** Clicks, comments, and choices become inputs to the next generation rather than merely feedback after the fact;
2. **Continuity can rely on lightweight anchors instead of a fully preplanned artifact.** A previous frame, world rules, character definitions, or the current page may be enough;
3. **The product becomes a continuing process instead of a fixed final artifact.** The boundary of “finished” becomes less clear.

More importantly, two conditions kept appearing together.

### 1. Discreteness: one unit can fail without killing the whole chain

The production units in these examples are relatively small: a scene, a page node, an image, a shot.

A weak scene can be skipped or regenerated. A poor page can be abandoned for another branch. A bad “draw” is already an expected part of a gacha-style workflow.

That is very different from a tightly coupled pipeline where the next stage depends precisely on the previous stage’s output.

### 2. Tolerance: one imperfect unit does not necessarily ruin the whole experience

An awkward transition, an inaccurate image, or one bad generation does not automatically destroy the overall product.

Some experiences even make unstable generation part of the product design: users expect multiple attempts and only keep the results they like.

This produced an early, deliberately rough diagnostic frame:

> **The easier production is to discretize, and the lower the cost of one unit failing, the more naturally generative AI tends to fit.**

---

## Why “discreteness + tolerance” may matter as much as model size

One correction is important here.

Generative-model errors are not necessarily independent. The same model, prompted in similar ways, can repeatedly make correlated or systematic mistakes.

But there is still a practical difference from deterministic program execution: **outputs vary across samples, one successful repair does not guarantee that the next generation can never repeat the mistake, and many failures only become visible when the result is actually executed or observed.**

So if the production structure assumes:

```text
A must be correct
  ↓
then B can be correct
  ↓
then C can be correct
  ↓
then D can be correct
```

putting a stochastic producer into that long chain creates many opportunities for errors to accumulate, propagate, and amplify.

A more local structure would instead allow:

```text
unit A   unit B   unit C   unit D
  ↓        ↓        ↓        ↓
try       fail      verify    replace
locally   locally   locally   locally
```

This suggests a very intuitive pattern:

[Hypothesis] AI often feels unusually natural in **low-coupling, high-tolerance** domains such as short-form media, illustration, and local generation, while feeling much more awkward in **high-coupling, low-tolerance** domains such as large software systems, financial core logic, or legally critical text.

That means improving AI use may not be only about waiting for a stronger model. We can also ask whether the production structure itself can change:

> **Can a problem that currently requires global correctness be reorganized into smaller units that can be independently accepted and independently fail?**

Discreteness is not enough on its own. Later discussion added at least three more dimensions:

- **Verifiability:** can we cheaply determine whether a result is actually acceptable?
- **Reversibility:** can a bad result be safely undone, replaced, or retried?
- **Failure correlation:** are multiple candidates secretly failing in the same way?

So “discreteness + tolerance” is not the final formula. It was simply the first frame that moved the conversation from model capability toward production organization.

---

## At this point, the electrification analogy came back into focus

Perhaps:

> **discreteness, local autonomy, and tolerance are the AI-software equivalent of one electric motor per machine, while long tightly coupled dependency chains are closer to the central shaft.**

Many traditional software structures were sensible responses to a different set of constraints:

- human beings write code slowly, so reuse is valuable;
- human memory is limited, so stable abstractions compress complexity;
- modification is expensive, so implementations are designed to live for a long time;
- deterministic programs execute every step predictably, so very long precise call chains are viable.

Those choices were rational in the environment that produced them.

But if the primary producer becomes an AI that is **fast at generation, cheap to parallelize, stochastic, context-limited, and dependent on external verification**, the old optimum may no longer be the new optimum.

That may help explain why AI programming often feels more awkward than AI image generation, short-form media, or interactive content: software is typically a **high-coupling, low-tolerance world full of historical state where local edits can have global consequences**.

The analogy finally turns into a concrete software question:

> **Can we redesign software production units so that most AI work happens inside small, clear scopes that can run, be verified, fail, and be replaced independently?**

We do not yet know. But that is now an experimental question rather than only a metaphor.

---

## So we began with only two small questions

We did not start by trying to invent “the next software-engineering paradigm” or a complete self-healing system.

### 1. Does useful software always require long-lived fixed code and rigid call chains?

Could a user express an intent, have a small program, interface, or workflow synthesized for the moment, run it in isolation, get the result, and then let it end, freeze, or disappear?

Even a one-use artifact would test whether:

> **“code must be a long-lived maintained asset” is a fundamental property of software, or a historical default created by past production costs.**

### 2. Can a functional unit be regenerated after failure instead of being debugged line by line by a human?

No autonomous evolution is required. The unit does not need to decide when it is “sick.” We only need a minimal loop:

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

If they do, we can begin asking whether such units can compose, inherit history, and reduce global human coordination over long periods of change.

---

## Only later did the current principles emerge

These are outcomes of the exploration, not starting assumptions:

- **Knowledge DRY; implementations may be WET** — business truth needs an authoritative source, while concrete implementations do not always need to be shared;
- **Persistent state; potentially ephemeral implementation** — facts, identity, rules, and history should survive implementation replacement;
- **Speculate before commitment; commit strictly** — allow many failures in isolation, but verify carefully before changing authoritative state;
- **Testable outcomes; flexible processes** — the path may vary, but acceptable results must remain checkable;
- **Keep knowledge in the environment; let AI retrieve it as needed** — system memory should not mean infinitely extending a conversation transcript.

See the [core thesis](理论-Theory/核心命题-Core-Thesis.en.md) and [design principles](理论-Theory/设计原则-Design-Principles.en.md).

---

## How are we testing this?

The research has three levels rather than beginning with a grand unified theory.

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

[Confirmed] This repository now preserves theory, proposals, experiment indexes, and the evolution of the research. Failures, counterexamples, and rejected ideas are intentionally retained because the corrections are part of the result.

[Open] We have not established that this is a generally better way to build software, and we do not need to prove that it applies to all software.

The real target is narrower:

> **Is there a meaningful class of software where changing the unit of production, validation, knowledge retention, and responsibility allocation can repeatedly produce more accepted functionality with substantially less global human coordination and rescue work under comparable quality and resource constraints?**

### Continue reading

| Interest | Entry points |
|---|---|
| Why this started | [Why we started](研究记录-Research-Notes/我们为什么开始-Why-We-Started.en.md) · [Research evolution](研究记录-Research-Notes/研究演进-Research-Evolution.en.md) |
| Current theory | [Core thesis](理论-Theory/核心命题-Core-Thesis.en.md) · [Design principles](理论-Theory/设计原则-Design-Principles.en.md) · [Production loop](理论-Theory/生产闭环-Production-Loop.en.md) · [Interface rigidity](理论-Theory/接口刚性-Interface-Rigidity.en.md) |
| Initial proposals | [Knowledge DRY / code WET](提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.en.md) · [Persistent state / ephemeral implementation](提案-RFCs/0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.en.md) · [Speculate before commitment](提案-RFCs/0003-试错前置提交严格-Speculate-Freely-Commit-Strictly.en.md) · [Ephemeral visual surface](提案-RFCs/0004-瞬时视觉表层与意图反推-Ephemeral-Visual-Surface.en.md) |
| Experiments | [Experiment index](实验-Experiments/实验索引-Experiment-Index.en.md) · [Longitudinal comparison protocol](实验-Experiments/08-持续演进对照实验-Longitudinal-Comparison.en.md) · [Document production trial field](实验-Experiments/09-文档生产试验田-Document-Production-Trial-Field.en.md) |
| Evidence and status | [Evidence and references](证据-Evidence/证据与参考-Evidence-and-References.en.md) · [Source digest](证据-Evidence/来源摘要-Source-Digest.en.md) |

Knowledge-status labels correspond exactly: **已确认 / Confirmed · 推断 / Hypothesis · 不确定 / Open · 建议 / Proposal**.