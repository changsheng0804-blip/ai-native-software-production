[Home](../README.md) · [中文](证据与参考-Evidence-and-References.zh-CN.md)

Version: v0.1 · Updated: 2026-09-14 · Paired language revision: v0.1

# Evidence and references

## Four epistemic statuses

[Proposal] Use the following throughout. Labels describe the evidence for a specific claim, not the author or tool. Having a source does not establish every claim it makes.

| Chinese | English | Conditions |
|---|---|---|
| 【已确认】 | [Confirmed] | Checkable sources or execution evidence directly support the bounded claim; distinguish source-reported from independently reproduced |
| 【推断】 | [Hypothesis] | An interpretation or testable proposition derived from materials; state assumptions, counterexamples, and tests |
| 【不确定】 | [Open] | Insufficient or conflicting evidence, unavailable reproduction, or untested claims |
| 【建议】 | [Proposal] | Candidate designs, methods, procedures, and next steps; not effectiveness conclusions |

[Proposal] Reassess source claims of verification against underlying evidence. Proposal adoption, publication, agreement among models, and passing tests do not automatically establish an unbounded [Confirmed] claim.

## Project sources and gaps

| ID | Source | Verification scope | Limitation |
|---|---|---|---|
| S0 | User-supplied original discussion | Read; sections, seven prototype reports, and file digest registered | Original attachment not public; prototype code and execution materials unavailable |
| S1 | Subsequent discussions | Read; production-organization focus, five-direction synthesis, repository requirements | Intellectual provenance, not outcome evidence |
| EX-01–07 | Prototypes reported in S0 | [Open] Awaiting reproduction | Not run here; no public reproduction bundle |
| EX-08 | Initial longitudinal comparison protocol | [Proposal] Written, not executed | No data, statistical results, or superiority conclusions |

[Source digest](来源摘要-Source-Digest.en.md) · [Experiment index](../实验-Experiments/实验索引-Experiment-Index.en.md)

## External references checked

Checked on 2026-09-14. Confirmation below is limited to the content inspected. These references establish mechanism background, not H1 or the overall benefits of the three RFCs.

<a id="e01"></a>
### E01: Self-stabilizing systems

Edsger W. Dijkstra, 1974, *Self-stabilizing systems in spite of distributed control*, EWD 426, Communications of the ACM 17(11), 643–644. [Author manuscript transcription, University of Texas archive](https://www.cs.utexas.edu/~EWD/transcriptions/EWD04xx/EWD426.html)

[Confirmed] The manuscript studies reaching and remaining within legitimate states under specified state machines, local moves, and a scheduling model.<br>
[Open] Extending such guarantees to generated implementations, changing requirements, and external business effects requires separate definitions and proofs. Related: Q7.

<a id="e02"></a>
### E02: Mergeable replicated data types

*About CRDTs*, maintained by researchers in the field. [CRDT research resource site](https://crdt.tech/)

[Confirmed] CRDTs handle replica conflicts through defined data structures, update rules, and merge behavior.<br>
[Open] Replica convergence does not establish business correctness or convergence of arbitrary generated programs. Related: RFC-0002, Q10.

<a id="e03"></a>
### E03: Candidate generation with test-based evaluation

*GenProg: Evolutionary Program Repair*. [Research team's project site](https://squareslab.github.io/genprog-code/)

[Confirmed] The project describes searching source-edit candidates, evaluating them with test suites, and iterating.<br>
[Open] The existence of this method establishes neither complete test coverage nor the superiority of regeneration over maintenance. This edition does not adopt the site's historical cost or success figures. Related: Q2.

<a id="e04"></a>
### E04: Transaction isolation and concurrent commitment

PostgreSQL, *13.2 Transaction Isolation*, corresponding to version 18 when inspected. [Official documentation](https://www.postgresql.org/docs/18/transaction-iso.html)

[Confirmed] The documentation distinguishes isolation levels and explains that applications must handle certain serializable-transaction conflicts by retrying.<br>
[Open] Database mechanisms do not automatically cover cross-service messages or other external effects. Related: RFC-0003.

<a id="e05"></a>
### E05: Research discussion venue

GitHub, *GitHub Discussions documentation*. [Official documentation](https://docs.github.com/en/discussions)

[Confirmed] Discussions supports community questions, exchange, and open-ended conversation.<br>
[Proposal] Use discussions for exploration, issues for bounded work, and pull requests for bilingual theory revisions. This is an organizational choice.

## Leads awaiting verification

[Open] The source materials mention the following, but this edition has not verified their primary sources and does not cite them as confirmed facts:

- Correlated failures among independently implemented versions and test-suite overfitting in program repair;
- Exact correspondence between cellular Potts models, differential adhesion, collective robotics, and these prototypes;
- Historical causal interpretations of electrification productivity;
- Live-generation products, disposable software, recent just-in-time construction papers, and performance figures;
- Mathematical mappings among diffusion, control, evolution, and this proposal.

[Proposal] Prefer original papers, author materials, official implementations, and repeatable data. Register the exact title, authors or institution, date, direct URL, linked claim, and supported and unsupported scope. Search snippets alone are insufficient.

## Updating status and correcting errors

[Proposal] A status-changing pull request records old and new statuses, evidence IDs, alternative explanations, and scope. Counterexamples may narrow a confirmed finding or return it to open status; retain history. Without project data, do not state success rates, performance gains, or that a new paradigm has been proven.
