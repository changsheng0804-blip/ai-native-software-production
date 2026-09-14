[Home](../README.md) · [中文](研究演进-Research-Evolution.zh-CN.md)

Version: v0.2 · Updated: 2026-09-14 · Paired language revision: v0.2

# Research evolution: how we kept changing our minds

This document is not organized as a theory outline. It follows the observations, failures, and corrections that actually moved the project forward.

[Confirmed] The sequence comes from the original discussion record and subsequent synthesis. It is an intellectual history, not a timestamped experimental log. External evidence and project experiment status are tracked separately in [Evidence and references](../证据-Evidence/证据与参考-Evidence-and-References.en.md).

---

## 1. The starting point was not “new architecture”; it was that AI programming kept feeling slightly wrong

The original question was simple: **does AI programming sometimes feel a little like alchemy?**

Not because the underlying science is dubious, but because two things coexist in practice:

- the capability is extraordinary and generation is fast;
- reliability, explanation fidelity, context stability, and change impact can still feel difficult to reason about.

If the problem is only “the model is not smart enough,” the natural answers are a stronger model, a larger context window, and better prompting.

Repeated use pushed us toward a different possibility: **some of the friction may come from the production system around the model, not only from model capability.**

That became the root question of the project.

---

## 2. First correction: code and explanation are not the same evidence

One of the first concrete observations was that an AI-generated explanation does not always faithfully describe the implementation it just produced.

That forced us to separate two intuitions:

> “the model knows what it wrote”

from

> “the model can generate a plausible explanation of what it wrote.”

The acceptance standard changed accordingly:

[Proposal] **move from trusting explanation to requiring execution evidence.**

Real runs, tests, constraint checks, and independent validation became more important than a statement such as “fixed.”

This later became the principle of separating generation from acceptance, but it began as a practical lesson: **do not let the same natural-language output serve as both the product and the proof that the product is correct.**

---

## 3. Second correction: we may have been stuffing too much into context

The obvious strategy was to give the model more: project docs, historical rules, source code, failures, and exceptions.

In practice, longer context did not always make the system more stable. Relevant information can compete with stale, irrelevant, or conflicting information.

So the question changed from:

> “How much larger does the context window need to be?”

into:

> **“Why should durable knowledge live inside conversation history at all?”**

That opened a different direction:

- durable state and knowledge remain in the environment;
- the AI retrieves only what matters to the current task;
- if a conversation produces new experience that should affect future behavior, that experience is written back into addressable external state.

[Hypothesis] This may be closer to a maintainable long-term production model than simply extending conversational memory.

---

## 4. Third correction: parallel generation is cheap; strong dependency is expensive

We initially treated “many candidates cause combinatorial explosion” as a major barrier.

On closer inspection, two separate issues had been conflated.

Generating many candidates in parallel is already easy. The combinatorial problem appears when every choice constrains long chains of downstream choices.

So the claim changed to:

> **Parallel generation is cheap; strongly dependent composition is expensive.**

This pushed the research toward the boundary of a production unit. If a unit can be understood locally, executed locally, validated locally, and fail locally, stochastic generation is easier to contain.

[Open] How far this localization can go is still an experimental question. Data, resources, timing, and business semantics do not disappear merely because implementation is isolated.

---

## 5. Fourth correction: many supposed infrastructure gaps already have prototypes

At first we treated lightweight constraints, generation gates, parallel execution, and rollback as infrastructure that might need to be invented from scratch.

In practice, existing tools already provide many pieces: hooks, gates, tests, sandboxes, and version control can intercept and constrain generated work.

That changed the research question from:

> “How do we invent all infrastructure for AI-native software?”

into:

> **“Can existing pieces be recombined into different production units and lifecycles?”**

This is why a local unit that regenerates after failure became such a natural first prototype: it does not require solving long-term autonomy, global judgment, and governance before anything useful can be tested.

---

## 6. Fifth correction: do not begin with a universal “is this unit diseased?” function

While exploring self-repair, a familiar engineering instinct appeared: define a function that decides whether a unit is broken and whether it should be abandoned.

That assumption was challenged.

Complex system state is rarely captured by a single threshold. Success rate, resource pressure, neighboring state, historical behavior, and external conditions may jointly determine whether repair, replacement, degradation, or shutdown is appropriate.

So we temporarily set aside the idea of a perfect centralized judge and moved toward a broader question:

> **Can environmental signals, hard boundaries, and feedback make recovery strategy a runtime choice rather than a fixed central verdict?**

[Open] This remains a later systems-engineering problem rather than a prerequisite for the earliest experiments.

---

## 7. Sixth correction: stop trying to prove a “new paradigm”; test two minimum possibilities

The discussion had grown rapidly: self-healing, immunity, emergence, hierarchy, cybernetics.

We deliberately narrowed it back to two small experiments.

### A. Can a temporary software artifact complete a real function?

It does not need to live for long. It only needs to show that some functions can be satisfied by “generate now → execute → discard,” rather than by committing everything to a permanent codebase in advance.

### B. Can a functional unit treat “failure → repair/regeneration → validation → rollback” as a normal lifecycle?

It does not need to invent a new purpose or autonomously evolve. It only tests whether existing LLM interfaces, tests, and version control can form a self-correcting loop.

These became Level 1 of the research path: **first establish that the software shape can exist; only then ask whether it is better.**

---

## 8. Biology and local-rule experiments were useful because they brought us back to reality

A series of prototypes then explored state-machine swarms, spatial fields, growth rules, Potts models, differential adhesion, and hierarchical promotion.

Their value was not to prove that software should imitate biology. Their value was that each failure exposed a hidden design variable.

Reported failures included:

- enclosed regions becoming permanently trapped;
- target fields becoming so strong that “self-organization” collapsed into a pre-specified answer;
- unconstrained dynamics converging to one color because that was the actual optimum;
- missing persistent identity causing fragmented domains;
- one-time promotion freezing higher-level units so they could no longer absorb neighboring regions.

These failures forced a harder conclusion:

> **Local rules can create structure without automatically creating the function we want.**

[Hypothesis] Biology, fields, and emergence are therefore more useful as scaffolding for discovering design variables than as the final software architecture.

This was the point where the research moved back toward real software production.

---

## 9. Seventh correction: self-healing is only one strategy; production organization is the real subject

As the exploration continued, a larger pattern became clear:

- regeneration is not the goal;
- multiple candidates are not the goal;
- dynamic adaptation is not the goal;
- biological analogy is not the goal.

They are mechanisms.

The higher-level question became:

> **If AI becomes one of the primary producers, should the unit of production, knowledge retention, quality control, composition, and responsibility allocation change?**

The most important unknowns now cluster into four areas:

1. decomposition cost;
2. validation cost;
3. composition cost;
4. knowledge continuity.

These are closer to the core of the project than “can software automatically fix a bug?”

---

## 10. Several strong claims were deliberately weakened

External checks and further discussion forced a number of early formulations to become more careful:

| Earlier claim | Current revision | Why |
|---|---|---|
| Generated errors are local independent noise | Errors may be stochastic but correlated; isolation and correlation must be measured separately | Multiple candidates can share the same bias |
| Duplicated implementation can reduce coupling to zero | It can reduce some implementation coupling, not shared data, time, resources, or semantics | The real world still contains shared constraints |
| AI generation is almost free | Count decomposition, generation, validation, retries, runtime, and human effort together | Cheap candidates may create expensive validation |
| Software should be discarded after use | Implementations may be ephemeral; state, knowledge, and evidence may need to persist | History must survive implementation replacement |
| Fixed APIs should disappear | Adapters may be generated dynamically, but critical boundaries still need machine-checkable contracts | Flexibility cannot eliminate verifiability |
| Returning metrics to normal proves correctness | Separate hard constraints from soft objectives | Some boundaries cannot be traded away for optimization |
| Parallel simulated worlds predict the future | They only test candidate behavior under modeled conditions | Simulation is not reality |

A useful habit emerged from these corrections: **whenever a slogan sounds elegant, ask under what conditions it stops being true.**

---

## 11. The current three-level experimental path

To avoid jumping directly from local observations to a grand conclusion, validation is now split into three levels.

### Level 1: existence

Test whether the minimal form can work:

- can temporary generated software complete a real task?
- can a self-correcting unit run through a complete lifecycle?

### Level 2: local benefit

Then compare concrete mechanisms:

- do more local implementations reduce cascading change impact?
- does environment-based retrieval reduce context confusion?
- do multiple candidates plus independent acceptance improve reliability?
- do generated adapters actually reduce evolution cost?

### Level 3: organizational benefit

Only then test the strongest claim:

> As system scale, requirement change, and historical complexity grow, does the amount of global coordination, review, and rescue work required from humans grow more slowly?

If not, the approach may still be a useful local tool. If the result repeats across a clear class of software, it may justify calling the change a new production model.

---

## 12. This repository is a record of changing claims, not a warehouse of conclusions

[Proposal] When a formal conclusion changes, preserve the path:

```text
old claim
   ↓
observation or experiment that broke it
   ↓
revised claim
   ↓
new scope
   ↓
next falsification attempt
```

Results are not grouped by model identity. Useful ideas from different sources enter the same research chain.

[Open] We still do not have a complete comparative experiment showing that the overall production model outperforms established software engineering. The next priority is not more abstract principles; it is completing Level 1 and Level 2 experiments one by one.
