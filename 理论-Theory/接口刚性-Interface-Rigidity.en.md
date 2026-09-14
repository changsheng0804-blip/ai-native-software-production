[Home](../README.md) · [中文](接口刚性-Interface-Rigidity.zh-CN.md)

Version: v0.1 · Updated: 2026-09-15 · Paired language revision: v0.1

# Interface rigidity

[Proposal] This document consolidates a variable that runs through the proposals into a single concept: interface rigidity. It originates from the "linear interface" discussion in the source material and states the object of study, the design principles, and the experiment questions in one frame. This document integrates concepts only; it adds no new evidence.

## 1. The concept: rigidity is a spectrum

[Confirmed] The source discussion proposed: traditional software delivers functionality through deterministic call chains — an upstream output must precisely match the downstream expectation, the match is fixed at design time and admits no runtime deviation; the real question is not "can interfaces be eliminated" but "how loose can interface rigidity become while functionality remains usable" — a continuum, not a binary. [Source digest S0](../证据-Evidence/来源摘要-Source-Digest.en.md)

[Proposal] Three anchor points on this spectrum:

| Anchor | Connection style | Example | Properties |
|---|---|---|---|
| Gear | Precise format meshing, fixed at design time | Traditional function calls, APIs | Reliable composition; demands exact execution at every step; errors propagate along the chain |
| Acceptance check | Does not dictate how work is done; checks only the delivered result | Contracts plus acceptance | Implementation freedom; requires checkable pass criteria |
| Understanding | Semantic handoff, no explicit interface | Click-to-generate single-shot content | Maximum generative freedom; holds only for single-shot, instantaneous, non-composed use |

[Hypothesis] A "retreat line" exists on this spectrum: as soon as persistent operation, reliable repetition, or multi-unit composition is required, current implementations retreat to some explicit interface. That line is the current boundary of generative production; locating it across task types is itself a research result.

## 2. The dial: contracts are the tool for operating rigidity

[Proposal] The essence of a contract is to replace "precise format matching" with "checkable results." A gear demands the other party share its shape; an acceptance check does not care how the other party works, only whether the delivery passes. Adapters convert between two acceptance checks. This lets "loose" avoid meaning "chaotic."

[Proposal] The research program condenses into one sentence:

> **Find out for which tasks the "interface tightness" dial can be loosened, how far, and at what cost.**

This restates existing items: open question Q3 (composition failure) becomes "at what looseness does it fall apart"; the RFC-0003 commit boundary is the guardrail as the dial turns toward loose; EX-08's group B sits in the middle of the acceptance-check range.

## 3. The reconstruction-cost criterion

[Proposal] The criterion for what must be unique and what may be duplicated:

> **Assets that are expensive to rebuild must have a single authoritative version; artifacts that are cheap to rebuild may be freely duplicated and regenerated.**

[Hypothesis] This criterion explains three existing claims at once: knowledge DRY — the authoritative version of a business rule is expensive to rebuild, because it comes from human judgment and accumulated history, not from any model; implementation WET — code is cheap to rebuild, because generation is cheap; persistent state — facts and identity cannot be regenerated; once lost, they are lost. The difference between the human era and the AI era is only that code moved from the expensive side to the cheap side.

## 4. Architectural shape: stable trusted kernel plus regenerable periphery

[Proposal] The three proposals converge on one shape:

- **Kernel**: state store, rule base, contracts and acceptance checks, commit gate, sandbox — everything expensive to rebuild and that must be trusted;
- **Periphery**: generated implementations — when one breaks, replace it; do not repair it.

RFC-0001 governs knowledge assets in the kernel; RFC-0002 draws the kernel–periphery boundary; RFC-0003 defines the only channel from periphery into kernel.

[Hypothesis] This answers the Level-3 question "where do humans ultimately work": in the kernel and the contracts. Human attention retreats from reading every line of implementation to maintaining the kernel, writing acceptance checks, and adjudicating conflicts.

## 5. What keeps these nine principles valuable

[Proposal] Start with a natural doubt: once AI becomes reliable and smart, will these nine principles become useless? The answer depends on why each principle helps. There are only three reasons:

1. **Because generation is cheap** ("cheap" in the table below): allowing duplicated implementations holds because regenerating a copy of code costs almost nothing. The cheaper generation gets, the larger this benefit — as AI advances, this reason grows stronger.
2. **Because AI makes mistakes** ("mistake-proofing"): confining errors to small units is needed so that an error does not drag others down. The more reliable AI becomes, the thinner this benefit — this reason weakens.
3. **Because of the nature of software itself** ("nature"): user data must not be lost has nothing to do with how strong AI is; any real business requires it forever — this reason does not change with AI.

[Proposal] Classify the nine principles by reason (primary reason first):

| Principle | Reason | Which part relies on it |
|---|---|---|
| Knowledge DRY, implementation WET | Cheap + nature | Code may be generated separately in each place because regeneration is cheap (cheap); a business rule may have only one authoritative version, an organizational requirement (nature) |
| Persistent state, ephemeral implementation | Nature + cheap | User data must not be lost (nature); a broken implementation is regenerated whole (cheap) |
| Speculate freely, commit strictly | Cheap + nature | Trying several candidates because trials are affordable (cheap); gating real changes is a matter of responsibility (nature) |
| Testable goals, flexible process | Nature + mistake-proofing | Stating what counts as passing aligns intent (nature); it also intercepts generation errors (mistake-proofing) |
| Generation separated from acceptance | Nature | One's own words cannot testify for oneself, ever |
| Keep contracts, generate adapters | Cheap + nature | Adapters can be generated (cheap); interface agreements keep composition safe (nature) |
| Feedback control serving explicit goals | Nature | A requirement of control, whoever does the work |
| Writing experience back into the environment | Nature + mistake-proofing | Experience must be archived (nature); it also avoids repeated mistakes (mistake-proofing) |
| Budgets for attention and compute | Mistake-proofing + nature | Unlimited retries are not allowed (mistake-proofing); money and time are finite (nature) |

[Hypothesis] Not one of the nine lives on "because AI makes mistakes" alone. So the answer to the opening doubt: model progress thins only a minority of the benefits; the bulk of this system rests on generation being cheap and on the nature of software, neither of which disappears as models grow stronger.

## 6. Scope map: where we expect to win, where to lose

[Proposal] The research stance is not winning everywhere; winning somewhere is enough. Then state where we intend to win, and let experiments check it:

**Where we expect to win.** The task has four properties: it can be split into small pieces; the quality of each piece is easy to judge; mistakes can be rolled back and retried; one failing piece does not drag others down. Examples: reports, forms, internal tools, format conversion, content pipelines. Expected reason: these properties let generate-much, filter-fast, redo-on-failure play to its strengths.

**Where we expect to lose.** Any one of these is dangerous: several pieces must stay consistent at all times and the requirement spans pieces (accounts must not differ by a cent); outward actions cannot be taken back (money paid out, messages sent); errors are hard to notice and costly (safety-critical); split-second response is mandatory (real-time). These settings cannot wait for try-first-then-see.

**The uncertain middle.** Business systems with historical baggage: years of accumulated special cases; each piece is right, yet composition tends to fail.

[Open] This map is inference, unchecked by experiment. Its most valuable use is choosing experiment subjects: winning where it is easiest shows only that the theory is not blind; winning in the middle, on the favorable side, shows the theory is useful. EX-08's product should be chosen there.

## Open items

[Open] How to measure rigidity: a spectrum needs graduations — format-check counts, acceptance-check item counts, inter-unit rework rates are candidates; none is chosen yet.

[Open] Who writes acceptance checks, at what cost: this is the entry to Q2 and possibly the most expensive part of the whole system.

See also: [Design principles](设计原则-Design-Principles.en.md) · [Core thesis](核心命题-Core-Thesis.en.md) · [Production loop](生产闭环-Production-Loop.en.md) · [RFC-0001](../提案-RFCs/0001-知识DRY实现WET-Knowledge-DRY-Code-WET.en.md) · [Open questions](开放问题-Open-Questions.en.md)
