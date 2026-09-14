[Home](../README.md) · [中文](研究演进-Research-Evolution.zh-CN.md)

Version: v0.3 · Updated: 2026-09-14 · Paired language revision: v0.3

# Research evolution: what forced us to keep changing our minds

This was not a path where we first proposed a theory and then accumulated proof.

The actual pattern was closer to this: a claim would begin to look convincing, then a real usage experience, outside example, or failed experiment would break part of it and force us to restate the question.

This document records those turns.

---

## 1. The starting point was not “a new architecture,” but the alchemy-like feel of AI programming

The first question was simply:

> **Why can AI programming feel strangely empirical even when the capability is so strong?**

Code generation was already fast, but problems around reliability, context, explanation, dependencies, and human review kept recurring.

It was easy to explain all of this as “the model is not strong enough yet” or “the prompt needs improvement.”

The first deeper turn was: **maybe the problem is not only the model, but how we organize its work.**

See [Why we started](我们为什么开始-Why-We-Started.en.md).

---

## 2. Observation: code and explanation can both sound convincing without actually matching

This forced us to drop an implicit assumption:

> “If the model can explain what it just wrote, that explanation can serve as validation.”

The revised view became:

> **The producer’s narrative and the evidence for the result must be separated.**

Execution, tests, types, permissions, and data constraints matter more than a model saying it has checked its work.

This later became the generation-versus-validation thread.

---

## 3. Observation: adding more context did not automatically solve complexity

The obvious response was to feed the model more code, more history, and more rules.

But larger context also created interference, contradictions, omission, and difficulty identifying which facts mattered to the current task.

That forced the question to change from:

> “How do we make AI remember more?”

into:

> **“Why does all of this information need to live inside one conversation?”**

This led toward durable environmental state and on-demand retrieval: business rules, historical exceptions, permissions, and state should become system assets rather than transient conversation memory.

---

## 4. The electrification analogy changed the scale of the question

If we only ask “how do we make AI write code more reliably,” we assume the software factory itself does not need to change.

The historical analogy challenged that assumption:

> Early factories often replaced steam engines with electric motors while keeping the central shaft system. The large productivity gains came later, when individual machines received their own motors and the factory could be rearranged around the flow of work.

That led to a new question:

> **Is AI programming today another case of “new power source, old factory layout”?**

From that point, the research object expanded from coding technique to production organization.

---

## 5. We did not immediately return to code; we first studied domains where AI already feels natural

This step was compressed too aggressively in the first repository draft, but it was essential.

If generative AI feels unusually natural in images, short-form media, and interactive content but unusually awkward in large software systems, perhaps the difference is structural rather than merely a matter of model capability.

That led to five directions:

1. **Versions → lineages** — generated artifacts may be better organized as branching families than one latest version;
2. **Completion → continuous generation** — some products may have no fixed final state;
3. **Inspection → deciding what deserves another round** — review can become resource allocation among candidate branches;
4. **Avoiding waste → deliberate large-scale experimentation** — cheap candidates make generate-many-then-select workflows rational;
5. **Production skill → making taste and intent explicit** — when generation is abundant, knowing what to ask for becomes scarcer.

These were not conclusions. They were tools for escaping the assumption that AI is simply a faster programmer or creator.

---

## 6. Flipbook, the H3 AI television experiment, and gacha-style AIGC workflows revealed a common pattern

The examples made several properties tangible:

- consumption feeds directly into the next generation step;
- continuity can be carried by lightweight anchors rather than a full preplanned artifact;
- the product shifts from a fixed deliverable toward an ongoing process.

More importantly, they often allow production to be decomposed into relatively independent units where one local failure does not destroy the entire chain.

This produced the first “discreteness + tolerance” diagnostic frame.

---

## 7. Observation: AI-friendly domains often tolerate local failure; large software often does not

This was where the electrification analogy finally connected back to software.

Traditional software frequently contains long call chains:

```text
A → B → C → D → E
```

Each stage is expected to be dependable because downstream stages rely on its precise output.

Generative AI is powerful but cannot guarantee perfect intermediate output every time.

That suggested a key hypothesis:

> **Discreteness + tolerance may be the AI-era equivalent of “one motor per machine,” while long, tightly coupled dependency chains may resemble the central shaft.**

This was later expanded to include verifiability, reversibility, failure correlation, and composition cost. But it was the first structural explanation for why AI feels smooth in some domains and awkward in others.

---

## 8. That forced us to shrink the big theory back into two minimum experiments

The discussion had already expanded into self-healing, immune systems, disease detection, environmental signals, and emergence.

We stepped back because the basic software shapes had not been established.

So we asked two questions.

### Q1: can temporary, on-demand generated software perform a real function?

Even if it lives for only seconds.

If yes, “software implementation must be a durable asset” is not a universal prerequisite.

### Q2: can a functional unit go through failure → LLM repair/regeneration → validation → rollback?

No autonomous evolution is required. It does not need to decide when it should die.

It only needs a minimum lifecycle that can be tested honestly.

These questions pulled the work back from philosophy into experiments.

---

## 9. The self-healing prototype showed that the loop can be assembled — and exposed a larger problem

A minimal loop using generation, real execution, testing, failure feedback, regeneration, and version rollback does not require entirely new infrastructure.

That established one thing:

> regeneration after failure is not purely hypothetical.

But it immediately exposed harder questions:

- are the tests complete enough?
- can AI-generated implementation and AI-generated tests share the same blind spot?
- a unit can regenerate, but can a whole system remain stable over time?
- how should units be decomposed, composed, and supplied with historical knowledge?

So “self-healing” was demoted from the research goal to one local mechanism.

---

## 10. Local-rule experiments pushed us toward systems thinking and biology, but the failures mattered more than the successes

To explore how local units might organize without one central script, we built experiments using state-machine swarms, spatial fields, growth rules, Potts models, differential adhesion, and hierarchical promotion.

They did not yield a ready-made architecture, but their failures exposed harder design variables:

- purely local rules can create irreversible topological traps;
- overly strong target fields turn supposed self-organization back into a pre-specified answer;
- without conservation constraints, systems can converge to mathematically simple but functionally meaningless states;
- without persistent identity, higher-level structures fail to become real units;
- one-time promotion can freeze bad boundaries, so higher-level units may need continued absorption and correction.

This led to another turn:

> **Biology can reveal design variables, but imitating biological detail does not automatically produce correct software.**

The work had to return to real software-production outcomes.

---

## 11. Important correction: generative errors cannot simply be treated as independent noise

Early on, it was tempting to describe model errors as local, independent, unpredictable noise and conclude that discreteness and redundancy would naturally absorb them.

That formulation was too strong.

Multiple candidates can share:

- the same model bias;
- the same ambiguous specification;
- the same missing boundary condition.

So “generate several versions” does not automatically create reliability.

This forced us to add **failure correlation** to the diagnostic framework and strengthened the case for heterogeneous generation and validation sources.

---

## 12. Another correction: discreteness + tolerance is not enough

Low failure cost is useful only if we can tell whether a result is acceptable.

If evaluation itself is unreliable, cheap generation simply produces cheap noise.

The framework therefore expanded to include at least:

- decomposability;
- verifiability;
- reversibility;
- failure correlation;
- composition cost.

Discreteness + tolerance remains important because it was the first useful clue, but it is no longer treated as a complete theory.

---

## 13. Principles such as “Knowledge DRY, implementation WET” appeared only after these failures

These were not invented as slogans first.

Each responded to a concrete tension:

- **Knowledge DRY; implementations may be WET** — reduce change coupling from shared implementation without letting business truth drift across copies;
- **Persistent state; potentially ephemeral implementation** — implementation can regenerate, but history, permissions, rules, and identity cannot disappear with it;
- **Speculate before commitment; commit strictly** — cheap generation permits abundant trials, but real state changes still need hard gates;
- **Keep knowledge in the environment; let AI retrieve it as needed** — avoid accumulating facts that “only one past conversation knew”;
- **Testable outcomes; flexible processes** — allow stochastic paths without making acceptance itself vague.

They remain testable design principles, not established universal best practices.

---

## 14. The research object finally shifted from “self-healing software” to software-production organization

The question that survived was:

> **Software engineering was organized around humans writing deterministic code. If a major producer becomes an AI that is excellent at generation but stochastic and context-limited, how should software production itself be reorganized?**

That leaves four central costs:

1. **Decomposition cost** — does splitting work into AI-friendly units still require humans to understand the whole system?
2. **Validation cost** — once implementation gets cheap, does acceptance become the new expensive bottleneck?
3. **Composition cost** — can individually valid units still fail in combinations that only global reasoning can detect?
4. **Knowledge continuity** — if implementations are replaceable, how do business meaning, state, and historical experience survive?

Regeneration is only one failure-handling strategy.

The real test is whether the production organization can keep most work inside AI’s effective range over time rather than merely moving complexity from coding into integration and human rescue.

---

## 15. Current experiment path: existence → local benefit → organizational benefit

To avoid jumping from a small mechanism to a grand theory again, the work now has three levels.

### Level 1: existence

Can these software shapes work at all?

### Level 2: local benefit

Are they actually better for clearly defined problems than conventional alternatives?

### Level 3: organizational benefit

As a real product evolves, can they reduce global human coordination, review, and rescue work?

Only repeated Level-3 success would justify serious talk of a new production paradigm.

---

## Current research discipline

[Proposal] Any important claim should preserve four things:

1. **What we originally believed;**
2. **what observation, case, or failure made us doubt it;**
3. **the revised formulation;**
4. **how the revised claim could be falsified next.**

The repository’s status labels — **Confirmed / Hypothesis / Open / Proposal** — exist to prevent a compelling analogy from quietly turning into an established fact as the story gets retold.
