[Back to Home](../README.md) · [中文版](0004-瞬时视觉表层与意图反推-Ephemeral-Visual-Surface.zh-CN.md)

Version: v0.1 · Updated: 2026-09-15 · Sync version: v0.1

# RFC-0004: Ephemeral Visual Surface and Intent Grounding

Epistemic status: [Proposal / 建议]<br>
Process: Draft / 草案<br>
Associated hypotheses: H2 (persistent state, ephemeral implementation), H4 (interface rigidity spectrum); Questions: Q1 (software without linear interfaces), Q3 (verification cost); Experiments: EX-08 interaction extension

## Problem and Hypothesis

[Hypothesis] Traditional Graphical User Interfaces (GUIs) depend on long, rigid implementation pipelines (database → backend API → state management → component tree → style system → DOM layout). This causes peripheral views and transient interactions to become an unmanageable maintenance burden (often accounting for 60%–80% of total commercial software codebases).

If the user interface is re-conceived as a transient projection of persistent semantic state—eliminating static frontend codebases, synthesizing visual surfaces on demand via generative engines, and grounding interactions into verified business intents via multimodal visual grounding—can we eliminate frontend maintenance debt without sacrificing transactional data integrity?

## Proposal

[Proposal] Establish a two-layer decoupled interaction model:

| Layer | Asset Form | Lifecycle and Characteristics |
|---|---|---|
| Underlying: Ground Truth and Invariants | Database records, identity, balances, business assertions (conservation of totals, permission barriers) | Long-lived, strictly deterministic; accepts only verified state transitions |
| Surface: Ephemeral Visual Surface | Synthesized visual artifacts (transient HTML/Tailwind, SVG, or multimodal images) | Ephemeral (destroyed after single session/interaction); no static codebase; holds no persistent facts |

The interaction loop consists of four steps:
1. **State Projection**: Generative engine reads underlying persistent state and directly synthesizes a visual surface tailored to current intent and context (e.g., Flipbook-style continuous stream or lightweight ephemeral HTML).
2. **Action Capture**: Captures raw user interactions on the visual surface (screen coordinates, clicked regions, speech, or text), rather than relying on pre-compiled DOM event listeners.
3. **Intent Grounding**: Multimodal model resolves coordinates and visual context into structured business intent (e.g., 'User clicked to purchase red coat #1024').
4. **Gated Commitment**: The structured intent passes through the gatekeeper defined in RFC-0003, verified by deterministic hard invariants, committed to the underlying database, and triggers the next state projection.

## Safe Boundaries for Discard-and-Regenerate

[Proposal] This mechanism, and the broader strategy of 'discarding old code and regenerating from scratch,' must NOT be applied indiscriminately. It is strictly bounded by three physical criteria:

1. **Computational Self-Containment (No irreversible side effects)**: Execution must be fully hermetic in a sandbox. Real-world physical side effects (dispatching bank wire transfers, mass SMS broadcasts, hardware actuations) must be gated until after state commitment; speculative trial-and-error in external environments is strictly forbidden.
2. **Verification Asymmetry (NP Characteristic)**: Generating the code/surface may require complex probabilistic inference, but checking compliance must be deterministic and instantaneous (e.g., verifying mathematical conservation of funds or row counts in milliseconds).
3. **Low Inversion Cost (Costless rollback and retry)**: Failed generations leave zero state residue, making sampling retries economically trivial.

## Minimal Experimental Design

[Proposal] Design a micro-business benchmark (e.g., dynamic reporting dashboard or shopping cart checkout with promotion rules):
- Group A (Traditional GUI): Standard REST APIs, React component libraries, state stores, and CSS; Agent patches existing frontend code upon format/layout changes.
- Group B (Ephemeral Visual Surface): Retains only SQLite store and invariant checker; frontend is synthesized as zero-dependency single-page projections or canvas, with interactions resolved via coordinate grounding.

Inject 30 sequential layout perturbations, special-case filtering rules, and edge-case inputs. Measure:
- Lines of code growth and technical debt residue;
- Regression defect rate (whether new requirements break existing rendering or validation);
- Total human coordination and review time.

## Stopping Conditions

[Proposal] If Group B experiences unacceptable latency (> 3s per interaction) due to multimodal ambiguity, or if invariant rejections cause excessive user-facing retries, stop pursuing fully interfaceless operation and fall back to dynamically generated lightweight structured contracts.

Sources: [S1 interfaceless artifacts and just-in-time synthesis](../证据-Evidence/来源摘要-Source-Digest.zh-CN.md#s1); Reference cases: Flipbook dynamic generation and multimodal visual grounding.
