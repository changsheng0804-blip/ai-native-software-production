[Home](../README.md) · [中文](我们为什么开始-Why-We-Started.zh-CN.md)

Version: v0.2 · Updated: 2026-09-14 · Paired language revision: v0.2

# Why we started

## A simple question: why can AI programming feel a little like alchemy?

This project did not begin with a plan to invent a new software architecture.

It began with a recurring feeling from actually using AI to build software: the capability is extraordinary, but the workflow often feels less reliable than the raw capability suggests.

The same patterns keep showing up:

- AI can produce code very quickly, but “generated” does not mean “correct”;
- it can explain its work fluently, yet the explanation may not match the actual behavior;
- giving it more context does not always make it more reliable; longer context can introduce confusion, omission, and misplaced attention;
- a seemingly local edit can travel through shared modules and dependency chains in surprising ways;
- AI can cheaply generate multiple options, while the surrounding process still assumes “one implementation, then a human reads it carefully”;
- as generation gets faster, the scarce resources increasingly look like validation, context management, dependency coordination, and human rescue work.

“Alchemy” is not a claim that the underlying technology is unscientific. Modern AI is built on serious statistical and optimization methods. The alchemy-like feeling is an engineering one: **the capability has advanced faster than the stable methods for organizing, validating, debugging, and operating it.**

That leads to a more uncomfortable possibility:

> **Maybe the problem is not only that AI is not yet enough like a programmer. Maybe we are still forcing a new kind of producer into a software-production system designed around human programmers.**

---

## First turn: “the model says it checked” is not evidence

One of the earliest problems was the gap between code and explanation.

An AI can generate code and then generate a plausible explanation of that code. The explanation itself does not prove that every concrete claim has been re-checked against execution.

That suggests a simple rule:

[Proposal] **Separate what the model says from what the system actually does.**

What matters more than “I fixed it” is evidence such as:

- real execution;
- tests;
- machine-checkable type, permission, and data constraints;
- independent checks against observable behavior.

The goal is not to make AI better at narrating confidence. It is to demote explanation to supporting information and promote execution evidence to acceptance criteria.

---

## Second turn: the problem may not be insufficient generation quality

The natural first response is to ask:

> If the model gets stronger, the context window gets longer, and the prompt gets better, does the problem disappear?

Repeated use suggests another possibility.

If a task requires the model to hold the entire large system, every historical exception, every dependency, and every business rule inside one context, then even a much stronger model is still being asked to solve an ever-growing global cognition problem.

So the question changed from:

> “How do we put more information into the model?”

into:

> **“How do we let the model fetch only the information that matters to the task it is doing now?”**

That means durable knowledge should not live only inside a past conversation. Business rules, historical exceptions, state, permissions, and failure experience should become addressable parts of the environment that can be retrieved, checked, and inherited.

[Hypothesis] If this works, the important form of “memory” may not be a longer conversation. It may be a more reliable external world.

---

## Third turn: parallel generation is not the hard part; dependency is

AI is already good at producing many candidates cheaply. The harder problem is what happens when those candidates sit inside long dependency chains. That creates composition explosions and difficult selection problems.

This led to an important correction:

> **Parallelism itself is not the main problem. Strong chain dependencies are.**

That pushed the discussion toward the boundary of a production unit.

If a unit can be understood in a small context, run independently, be validated independently, and fail independently, then stochastic generation is easier to contain. If everything shares implementation and participates in long call chains, local errors become global coordination problems.

This does not imply that all software can or should have zero dependencies. The real question is:

[Open] **Can enough work be turned into local closed loops that most tasks remain inside the range where AI performs well?**

---

## Fourth turn: do not begin by designing a perfect self-healing system

At one point the discussion became much more ambitious: how should a system detect “disease,” decide between repair and replacement, and build something analogous to an immune system?

We deliberately narrowed the question.

Those are later systems-engineering problems. Two earlier questions are more basic and easier to answer honestly.

### Question 1: can a useful software artifact exist without a traditional rigid call chain?

Even if it is temporary, single-use, and unable to run indefinitely.

For example: a user expresses an intent, the system synthesizes a small program or interface, runs it in isolation, returns the result, then discards it. That is enough to test whether “code must be a long-lived fixed asset” is a necessary assumption.

### Question 2: can a functional unit be regenerated after failure while preserving its functional goal?

No autonomous evolution is required. The unit does not decide what its purpose should become.

It only needs a loop such as:

```text
functional specification
        ↓
generate implementation
        ↓
run and test
        ↓
failure → provide failure evidence to AI
        ↓
repair / regenerate
        ↓
validate again
        ↓
rollback when needed
```

The components required for this already exist. The useful experiment is to observe where such a unit works smoothly, where it breaks down, and whether it can become a genuine production unit with a clear boundary rather than merely another feature inside a human-led development workflow.

---

## Fifth turn: from self-healing to production organization

As the discussion continued, the research object changed.

Repair, regeneration, candidate generation, and dynamic adapters are all local mechanisms. The higher-level question became:

> **If the main producer becomes an AI that is excellent at generation but stochastic and context-limited, how should software production itself be reorganized?**

That includes questions such as:

- how work should be decomposed so local tasks remain in the model’s effective range;
- how information should be stored so the system does not depend on one conversation history;
- how results should be accepted so explanation is not treated as evidence;
- how units should compose so local failures remain local where possible;
- how compute and attention should be budgeted so cheap generation does not become cheap noise;
- what humans should decide if they are no longer expected to produce and inspect every line themselves.

This is where the electrification analogy becomes useful.

Replacing a steam engine with an electric motor did not immediately transform factory productivity. Much of the benefit arrived when factories were reorganized around the fact that power no longer had to be distributed through one central mechanical layout.

[Hypothesis] Much AI programming today may still resemble “new power source, old factory layout”: AI writes the code, but task units, shared dependencies, review practices, and responsibility boundaries remain mostly inherited from human-first software engineering.

This project asks whether the factory itself needs to be rearranged.

---

## The current principles are outcomes, not starting assumptions

Several compact principles emerged later:

- **Knowledge DRY; implementations may be WET:** business truth needs an authoritative source, while implementations do not always need to be shared;
- **Persistent state; potentially ephemeral implementation:** facts, identities, rules, and history must not disappear with one code artifact;
- **Speculate before commitment; commit strictly:** allow many failures in isolation, verify carefully before changing authoritative state;
- **Testable outcomes; flexible processes:** the path can vary, but acceptable results must remain checkable.

[Proposal] These should be treated as research hypotheses and design rules to test, not as declarations of a finished “new paradigm.”

---

## How we are testing the idea

The research path has three levels. We do not begin by trying to prove a grand theory.

### Level 1: can this software shape exist at all?

Test minimum feasibility:

- can temporary generated software complete a real task?
- can a functional unit repeatedly go through “failure → repair/regeneration → test → rollback”?

### Level 2: is it better for some local problems?

Examples:

- does more self-contained implementation reduce cascading change impact?
- is retrieving knowledge from an external environment more stable than stuffing everything into long conversation context?
- can multiple candidates plus independent validation reduce the rate at which errors reach authoritative state?

### Level 3: can it become a different production organization?

Only then do we ask:

> As the product grows, requirements keep changing, and history accumulates, can this organization keep human global coordination and rescue work growing more slowly?

If humans still need to understand all code, dependencies, and historical exceptions, then the complexity has merely moved from “writing” to “integration and review.”

If most work can remain local, testable, and replaceable while humans focus on genuinely new goals, conflicts, and value judgments, then the production model may actually have changed.

---

## What this repository is for

[Proposal] This repository is not meant to protect a theory from being falsified.

It should preserve the loop:

```text
real usage problem
      ↓
hypothesis
      ↓
small experiment
      ↓
failure or counterexample
      ↓
revised claim
      ↓
new test
```

We may never find one architecture that applies to all software. That is not required.

If we can identify even one meaningful class of software where the evidence repeatedly shows that:

> **using AI well requires changing the unit of production, quality control, knowledge retention, and responsibility allocation,**

that would already be a significant result.
