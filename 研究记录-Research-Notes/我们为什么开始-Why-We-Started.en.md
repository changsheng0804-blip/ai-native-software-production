[Home](../README.md) · [中文](我们为什么开始-Why-We-Started.zh-CN.md)

Version: v0.3 · Updated: 2026-09-14 · Paired language revision: v0.3

# Why we started

## This did not begin with “let’s invent a new architecture”

It began with a much simpler question:

> **Why can AI programming feel a little like alchemy?**

Not because the science underneath AI is dubious. Modern models are grounded in machine learning, statistics, and optimization.

The alchemy-like feeling comes from use:

- the capability is extraordinary, yet it is often unclear when to trust the result;
- changing a few words in a prompt can suddenly improve or derail the output;
- a model can confidently explain code it has not actually validated;
- adding more context does not always help and can create interference;
- a local edit can propagate through shared dependencies in surprising ways;
- AI can produce code very quickly while humans still have to inspect, validate, coordinate, and rescue slowly.

It feels like practice has outrun engineering method.

So the question gradually moved beyond prompt technique:

> **Have we actually learned how to organize software production around this new kind of producer?**

---

## First turn: “the model says it checked” is not evidence

One of the earliest problems was the gap between code and explanation.

AI can generate code and then generate a fluent explanation of that code. The explanation does not prove that every concrete claim was checked against execution.

That led to a simple principle:

> **Running the system matters more than asking the model to keep explaining.**

Useful evidence should come from outside the model’s narrative wherever possible:

- real execution;
- tests;
- type and data constraints;
- permission checks;
- repeatable observable behavior.

This later became the idea that generation and validation should be treated as separate concerns.

But even with better validation, another problem remained: if AI is placed inside the same long dependency structures as human-written software, local work still turns into a global cognition problem.

---

## Second turn: maybe the problem is not just model capability — maybe the factory layout is wrong

A historical analogy became central here.

When electric power first spread, factory owners often replaced the steam engine with an electric motor while preserving the entire steam-era layout: one large central power source driving shafts and belts that distributed mechanical power throughout the factory.

Productivity gains were limited because the **logic of production had not changed**. Only the power source had changed.

The larger gains came later, when engineers realized that electric motors could be made small and cheap enough to attach directly to individual machines. Once the central shaft was no longer necessary, machines could be rearranged around the actual flow of work.

Electricity’s deeper value did not appear when it merely occupied the old steam engine’s place. It appeared when the factory was reorganized around electricity’s different physical properties.

That raised a harder question:

> **Is much of today’s AI programming simply replacing “the programmer” with AI while leaving the software factory almost unchanged?**

We still tend to assume that:

- code is the main durable asset;
- a feature should live in fixed code;
- modules compose through long-lived call relationships;
- shared implementations should be reused aggressively;
- humans understand and review the system by reading code;
- failures should be debugged, localized, and repaired in the original implementation.

Those assumptions were not arbitrary. They made sense when human coding was slow, understanding large systems was expensive, and duplicate maintenance was dangerous.

The question is whether they should remain unchanged when the producer is a system that can generate quickly, resample repeatedly, but is stochastic and context-limited.

---

## Before returning to software, we looked at domains where AI already feels natural

If generative AI fits some domains smoothly and others awkwardly, perhaps there are structural differences between them.

That led to five directions. They were not architecture proposals at first. They were attempts to ask:

> **What would production look like if we actually respected the properties of generative production instead of treating AI as a faster human?**

---

## Direction 1: “versions” may partly give way to “lineages”

Industrial products are usually organized as v1, v2, v3 — later versions replace earlier ones.

Generative AI behaves more like repeated sampling. The same intent can produce many different but usable results.

[Hypothesis] A more natural structure may preserve a **generation lineage**:

- which branch came from which parent;
- which variants were discarded;
- which work better in particular contexts;
- which deserve more resources;
- which branches should be recombined.

Human work then becomes less about turning v1 into v2 and more about navigating, selecting, and recombining a branching space of possibilities.

Git already has branches, but it still assumes a long-lived code artifact whose modification history matters. Tools designed around large-scale generation might look more like evolutionary-tree browsers than commit histories.

---

## Direction 2: “completion” may partly give way to “continuous generation”

Industrial products have a clear completion point.

If generation becomes cheap enough, some products may not need to exist fully in advance.

- a page can be created when clicked;
- a story can continue only when the reader reaches the next point;
- a UI can exist only for the current task;
- music, imagery, and narrative can keep responding to the user and environment.

[Hypothesis] This changes the boundary of the product itself:

> **When does something count as existing? When is it finished?**

Some products may become processes rather than fixed deliverables.

---

## Direction 3: quality control may partly shift from “is it correct?” to “should this branch continue?”

Traditional inspection has a blueprint. A part should be 10 mm; deviation can be measured.

Generative output often has no single correct answer. A page, story, image, or design can have many viable versions with different value.

So part of review changes:

> **Not only “how far is this from the standard?” but “is this branch worth continuing, stopping, or funding for another round?”**

That resembles curation, recruiting, or venture selection more than classical inspection.

[Hypothesis] Some future editorial, review, and product roles may shift from checking every artifact toward deciding which possibilities deserve the next unit of attention or compute.

---

## Direction 4: when generation is cheap, deliberate waste can become rational

Producing one hundred variants and keeping one is unacceptable when each candidate is expensive.

If candidates are cheap, the logic can reverse:

```text
generate many diverse candidates
        ↓
run / inspect quickly
        ↓
discard most
        ↓
concentrate resources on a few branches
```

Image generation’s “make several, choose one” pattern is only the simplest form.

[Hypothesis] Writing, code, and product design may adopt more aggressive versions: not “make one improved version,” but “generate many parallel worlds and continue only a few.”

---

## Direction 5: a scarce human skill may become making taste and intent explicit

If production becomes abundant, a scarcer capability may be:

> **knowing what you actually want and turning a vague preference into constraints precise enough to guide generation.**

This is not just prompt technique.

It sits between judgment, goal definition, tradeoffs, and precise expression.

The skill exists today across art direction, product management, editing, and creative consulting, but it is rarely treated as a first-class engineering capability.

[Hypothesis] If generative capacity keeps expanding, translating taste and intent into constraints may become more valuable rather than less.

---

## Three examples made these ideas feel concrete

Three examples mattered especially in the discussion:

- **Flipbook** — clicking the current page can directly trigger generation of what comes next;
- **the MiniMax H3 AI television experiment** — live audience feedback is fed back into continued generation;
- **“gacha-style” AIGC production workflows** — generate many, filter quickly, discard failures, generate again.

These do not prove an AI-native software architecture. They simply reveal recurring properties.

### 1. Consumption becomes part of production

Instead of production ending before consumption begins:

```text
click / consume / react
        ↓
becomes next-generation input
        ↓
new output
        ↓
new consumption
        ↺
```

Production and use form one loop.

### 2. Continuity can be carried by lightweight anchors

A complete future plan is not always necessary.

The previous frame, the current page, character notes, world rules, or current state can be enough to keep the next generation coherent.

### 3. The product becomes a process over time

There may be no absolute “final version.” What exists is a continuing process of triggering, generation, and adaptation.

---

## Then a deeper common structure appeared: discreteness + high tolerance

These domains also share something else:

> **their smallest production units can fail relatively independently, and the cost of a single failure is often low.**

A bad image can be discarded.

A weak video shot can be regenerated.

An uninteresting generated page need not destroy the entire product.

That led to an early diagnostic frame:

> **The more discrete the production units, and the more failure the domain can tolerate, the more naturally generative AI tends to fit.**

This frame was later revised. Discreteness and tolerance are not enough. We also need to consider:

- **verifiability** — how cheaply can we decide whether a result is acceptable?
- **reversibility** — can failure be rolled back, replaced, or retried?
- **failure correlation** — do multiple candidates tend to make the same mistake?
- **composition cost** — do individually valid units still fail when combined?

But discreteness + tolerance was the first clue that AI-friendly and AI-hostile domains might differ structurally, not only in model capability.

---

## This is where the electrification analogy finally connected back to software

A traditional pipeline looks like:

```text
A → B → C → D → E
```

Each step is expected to be correct because the next step depends on its exact output.

Generative AI is powerful, but in practice it cannot guarantee that every intermediate result is always correct.

Put that producer into a long, tight dependency chain and several problems become natural:

- an early mistake propagates;
- a local edit causes distant cascading effects;
- solving a local task requires ever larger global context;
- generation gets faster while integration and review become the bottleneck.

That led to a stronger hypothesis:

> **Discreteness + tolerance may be the AI-era equivalent of “one motor per machine,” while tightly coupled linear pipelines may resemble the steam-era central shaft.**

This may help explain a familiar experience:

- generative AI often feels unusually smooth in short-form media, illustration, and interactive content;
- it often feels unusually awkward in large software systems with deep dependencies, low tolerance, and long histories.

Not because “code cannot be generated,” but because large software is often a **high-coupling, low-tolerance, history-heavy environment**.

If that diagnosis is right, the real question is no longer “how do we make AI make fewer mistakes inside the old pipeline?” It becomes:

> **Can software be reorganized so that more work naturally falls into discrete, local, verifiable units where AI performs well?**

---

## Only then did we narrow the research to two basic experiments

The discussion had already expanded into self-healing, immune systems, disease detection, environmental signals, and emergence.

We deliberately stepped back.

If the most basic software shapes do not exist, the larger theory is irrelevant.

So we asked two restrained questions.

### Question 1: can useful software exist without being organized as a long-lived code asset and a rigid long call chain?

It does not need to run forever.

Even an artifact that lives for seconds is enough:

```text
user expresses intent
        ↓
generate small program / UI / workflow
        ↓
run in isolation
        ↓
return result
        ↓
implementation ends or is discarded
```

If this can perform a real function, then “software must be written in advance, stored permanently, and continuously maintained” is not necessarily a universal property of software.

### Question 2: can a functional unit improve after failure without requiring a human to debug it line by line?

“Improve” here does not mean autonomous evolution.

The unit does not decide what its purpose should become. It only needs:

```text
functional specification
      ↓
AI generates implementation
      ↓
real execution / tests
      ↓
failure
      ↓
return failure evidence to AI
      ↓
repair / regenerate
      ↓
validate again
      ↓
rollback when needed
```

Most underlying components for this loop already exist.

The meaningful experiment is to observe where it works, where it breaks, and whether it can become a genuine independent production unit rather than another button inside a human-led workflow.

---

## The biological and emergence experiments came later

Once we were thinking in terms of local units, isolated failure, and regeneration, the next question became:

> What happens if local units do not follow one central script, but respond mainly to local environment and constraints?

That led to experiments with state-machine swarms, spatial fields, growth rules, Potts models, differential adhesion, and hierarchical promotion.

They revealed useful design lessons:

- local rules do not automatically produce correct global function;
- irreversible decisions create traps;
- higher-level units need persistent identity;
- local stability does not imply global correctness;
- overly strong target fields can eliminate genuine exploration.

But they also led to another important turn:

> **Biology can expose design variables, but it cannot do the software engineering for us.**

Any useful result must eventually return to real software production and demonstrate what cost it reduces or what capability it enables.

---

## Only at the end did the research object become clear

We are not primarily studying one specific “self-healing software” technique.

Nor are we studying how AI can take over old systems.

The higher-level question is:

> **Software engineering was organized around humans writing deterministic code. If a major producer becomes an AI that is excellent at generation but stochastic and context-limited, how should software production itself be reorganized?**

That includes:

- how to decompose work so local tasks stay inside AI’s effective range;
- where knowledge should live so it does not exist only inside one conversation;
- how to accept results without treating model explanation as evidence;
- how to compose units so local mistakes do not become global failures;
- how to prevent cheap generation from becoming cheap noise;
- where human attention should move if humans are no longer expected to produce and inspect every line.

---

## The current principles are outcomes, not starting assumptions

Several working principles emerged later:

- **Knowledge DRY; implementations may be WET**;
- **Persistent state; potentially ephemeral implementation**;
- **Speculate before commitment; commit strictly**;
- **Testable outcomes; flexible processes**;
- **Keep knowledge in the environment; let AI retrieve it as needed**.

They remain [Proposal] or [Hypothesis], not a proven “new paradigm.”

They are worth testing because they emerged from actual usage problems, real-world cases, failed experiments, and repeated corrections — not because they sound elegant in isolation.

---

## How we plan to test this

The research proceeds in three levels.

### Level 1: can this software shape exist?

Establish minimum feasibility.

### Level 2: is it actually better for some local problems?

Compare isolation, validation, knowledge retrieval, and candidate selection mechanisms against conventional alternatives.

### Level 3: can it become a different production organization?

Only then ask whether global human coordination and rescue work grow more slowly as product complexity and change accumulate.

If humans still need to understand every code path, dependency, and historical exception, complexity has only moved from coding into integration and review.

If most work can remain local, verifiable, and replaceable while humans focus on goals, value tradeoffs, and genuinely new problems, then the production organization may have changed.

---

## What this repository should preserve

Not just conclusions, but the full loop:

```text
real friction in everyday use
        ↓
hypothesis
        ↓
real-world examples
        ↓
small experiment
        ↓
failure or counterexample
        ↓
revised claim
        ↓
new question
```

Rejected ideas, failed experiments, and questions that turned out to be badly framed should remain visible.

If this work eventually contributes to a different way of producing software, the valuable artifact will not only be a final set of principles. It will also be the record of:

> **how a series of ordinary “something feels wrong” experiences in AI programming gradually turned into a testable research direction.**
