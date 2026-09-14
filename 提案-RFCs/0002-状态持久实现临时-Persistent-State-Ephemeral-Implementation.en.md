[Home](../README.md) · [中文](0002-状态持久实现临时-Persistent-State-Ephemeral-Implementation.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# RFC-0002: Persistent state, potentially ephemeral implementation

Epistemic status: 【建议 / Proposal】<br>
Workflow status: Draft / 草案<br>
Related claims: H3, H5; question: Q4; experiment: EX-08 inheritance and recovery checks

## Problem and hypothesis

[Hypothesis] Business knowledge or runtime state hidden in an implementation or conversation may be lost during replacement. Making them explicit may support repair, replacement, and regeneration alike.

## Proposal

[Proposal] Distinguish three asset classes:

| Asset | Minimum contents | Lifetime and handling |
|---|---|---|
| Facts and state | User data, object identities, state versions, events, operation IDs | Persist under business and retention rules |
| Knowledge and constraints | Rules, exceptions, permissions, validators, sources, scope | Explicit versions with revision history |
| Implementations and runtime evidence | Code or artifacts, configuration, input digests, checks, adoption and supersession links | Implementations may be replaced; retain adopted versions and necessary evidence under a policy |

Durable does not mean immutable, nor indefinite personal-data retention. Determine implementation lifetime from cost, need, and traceability; assume neither 30-second destruction nor millisecond generation.

## Replacement protocol

[Proposal] Start with a reporting or format-conversion unit with limited effects:

1. Record unit identity, implementation version, rule versions, and state schema.
2. Generate a replacement against an isolated copy using explicit knowledge, without hidden exceptions supplied by the old conversation.
3. Check historical cases, current state, compatibility, permissions, and unfinished operations.
4. If the schema changes, validate migration and recovery separately, including concurrent reads and writes and old-version compatibility.
5. Record the adoption point and supersession links; validate runtime behavior and retain a recovery path.

Implementation switching and data migration are different operations. Separately verify whether the old implementation can read migrated data. Irreversible external effects require their own reconciliation and compensation design.

## Comparison and observation

[Proposal] Both arms use the same explicit knowledge and state boundaries: A repairs the existing implementation; B may regenerate the whole unit. Use a fixed sequence of new rules, legacy exceptions, interruptions, repeated requests, and one schema change. Separately compare retained versus fresh conversations to isolate the effect of external knowledge.

Record historical acceptance retention, state discrepancies, recovery time, duplicate executions, human interventions supplying hidden knowledge, and all migration and retention costs. Preserve generator configuration as a reproducibility parameter, without organizing research views by model identity.

## Decision and stopping rules

[Proposal] Any fact loss, permission violation, or duplicate effect is a failure that pauses that path. Include recovery costs. Compare time and total cost only after rules and historical behavior remain acceptable.

[Open] If B requires substantial migration or human explanation, the finding may only be that external knowledge helps, not that regeneration beats repair. No requirement makes all code short-lived; stable deterministic cores may remain long-lived.

Sources: [S0 §VII, §IX and S1](../证据-Evidence/来源摘要-Source-Digest.en.md); background [E02](../证据-Evidence/证据与参考-Evidence-and-References.en.md#e02) concerns merging replicas of specific data types and does not establish arbitrary state replacement.
