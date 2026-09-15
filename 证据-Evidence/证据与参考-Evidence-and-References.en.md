[Home](../README.md) · [中文](证据与参考-Evidence-and-References.zh-CN.md)

Version: v0.2 · Updated: 2026-09-15 · Paired language revision: v0.2

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

Checked on 2026-09-14 (E01–E05), 2026-09-15 (E06–E11), and 2026-09-15 (E12–E37; verified online by the research agent; except where noted, only bibliographic entries, abstracts, or official pages were checked, not full texts read in their entirety). Confirmation below is limited to the content inspected. They respectively support mechanism background or individual claims; none directly verifies H1 or the overall benefits of this repository's three RFCs.

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

<a id="e06"></a>
### E06: Supervision trees and runtime code replacement (Erlang/OTP)

Joe Armstrong, 2003, *Making reliable distributed systems in the presence of software errors*, doctoral dissertation, Royal Institute of Technology (KTH), Stockholm. [Full thesis (hosted on the official Erlang site)](https://erlang.org/download/armstrong_thesis_2003.pdf); mechanisms also documented in [Supervisor Behaviour](https://www.erlang.org/doc/system/sup_princ.html) and [Release Handling](https://www.erlang.org/doc/system/release_handling.html).

[Confirmed] The official documentation records that supervisors keep child processes alive by restarting them under defined strategies and terminate and escalate when restart intensity exceeds limits; Erlang supports replacing module code at runtime, and SASL provides a framework for upgrading and downgrading entire releases online. Armstrong's thesis §4.3 states the error-handling philosophy verbatim: "Let it crash. Do not program defensively."<br>
[Open] Ephemeral implementation with persistent state and supervision-decided failure handling has run in telecommunication-grade systems for decades; this does not establish that replacing AI-generated implementations is equally safe. The widely circulated AXD301 "nine nines" availability figure is an undocumented self-report noted in the thesis itself and is not used as effectiveness evidence. Related: RFC-0002, the production loop's failure decisions.

<a id="e07"></a>
### E07: Recovery-oriented computing (ROC)

David Patterson, Aaron Brown, and 13 others, 2002, *Recovery Oriented Computing (ROC): Motivation, Definition, Techniques, and Case Studies*, technical report UCB//CSD-02-1175, Computer Science Division, University of California, Berkeley (a joint Berkeley/Stanford project, 2001–2006). [Report PDF (project site)](http://roc.cs.berkeley.edu/papers/ROC_TR02-1175.pdf), [archived Berkeley TR page](https://web.archive.org/web/2024/http://www2.eecs.berkeley.edu/Pubs/TechRpts/2002/5574.html)

[Confirmed] The report argues that hardware faults, software bugs, and operator errors are "facts to be coped with, not problems to be solved"; engineering emphasis should move from extending mean time to failure toward shortening mean time to repair (MTTR over MTTF). It proposes system-level undo, recursive restartability, and rapid diagnosis, and introduces real site-failure data (operator error as a leading cause of outages).<br>
[Open] It establishes the engineering feasibility of the fast-recovery route, not that fault prevention can be relaxed; its industry influence is an author-reported retrospective, not reproducible measurement. Related: the production loop's runtime observation, RFC-0003's failure decisions, Q2.

<a id="e08"></a>
### E08: Optimistic concurrency control

H. T. Kung and John T. Robinson, 1981, *On Optimistic Methods for Concurrency Control*, ACM Transactions on Database Systems 6(2), 213–226. [ACM DOI page](https://dl.acm.org/doi/10.1145/319566.319567) (full text paywalled; citation and wording verified against Crossref registry metadata and a publicly hosted copy of the paper)

[Confirmed] The paper structures transactions into a read, validation, and possible write phase: reads are unrestricted, modifications first go to local copies, and the transaction validates against latest state before commitment; failed validation backs the transaction up to start over as a new transaction.<br>
[Open] "Try freely, validate strictly against latest state before commitment, restart on failure" holds for database concurrency control; it does not establish a positive return when generalized to candidate software production pipelines — that benefit is exactly what RFC-0003 is designed to test. See also E04.

<a id="e09"></a>
### E09: Industrial use and cost of formal methods (AWS)

Chris Newcombe, Tim Rath, Fan Zhang, Bogdan Munteanu, Marc Brooker, and Michael Deardeuff, 2015, *How Amazon Web Services Uses Formal Methods*, Communications of the ACM 58(4), 66–73. [CACM article page](https://cacm.acm.org/research/how-amazon-web-services-uses-formal-methods/), [author preprint](https://lamport.azurewebsites.net/tla/formal-methods-amazon.pdf); tool positioning on [Lamport's TLA+ page](https://lamport.azurewebsites.net/tla/tla.html)

[Confirmed] AWS engineers applied TLA+ specifications and model checking to ten large systems including S3, DynamoDB, EBS, and internal distributed lock managers, finding concurrency-and-failure-timing design defects that design reviews, code reviews, and months of testing had missed (for example, a DynamoDB data-loss bug whose shortest error trace required 35 steps, and a reviewed fix that was itself still defective, found by the model checker in seconds).<br>
[Confirmed] Cost side: engineers learned TLA+ from scratch to useful results in two to three weeks; specifications run to a few hundred lines; the authors report spec writing as "more reliable and less time consuming" than their informal proofs; management allocates engineering time to TLA+ in annual planning.<br>
[Open] This is experience on difficult design problems in critical systems; it neither establishes that acceptance cost is affordable for arbitrary tasks nor that AI-generated implementations should always be accepted through formal specifications. It gives Q2 a real price reference: a few hundred lines of specification plus weeks of learning, in exchange for design defects that review and testing do not find. Related: Q2, the design principle "testable goals," the acceptance check in interface rigidity.

<a id="e10"></a>
### E10: No Silver Bullet (Brooks)

Frederick P. Brooks, Jr., 1986, *No Silver Bullet — Essence and Accidents of Software Engineering*, Information Processing '86 (IFIP Tenth World Computer Congress, Dublin), pp. 1069–1076; reprinted in IEEE Computer 20(4) (April 1987), pp. 10–19. [computer.org article page](https://www.computer.org/csdl/magazine/co/1987/04/01663532/13rRUwcS1zv), [UNC technical report, full text](https://www.cs.unc.edu/techreports/86-020.pdf)

[Confirmed] Brooks divides software difficulty into essence (the specification, design, and testing of the conceptual construct) and accidents (representation and implementation), and asserts that no single development in technology or management technique promises even one order-of-magnitude improvement in productivity, reliability, or simplicity. He examines nine candidate silver bullets (high-level languages, object orientation, artificial intelligence, expert systems, automatic programming, graphical programming, program verification, environments and tools, workstations) and finds each attacks only accidental difficulty.<br>
[Confirmed] Full-text verification: the original does not discuss reorganizing production or the human–AI division of labor as a candidate; Brooks's proposed attacks on essence are buying rather than building, requirements refinement with rapid prototyping, incremental development, and cultivating great designers.<br>
[Open] That H1 falls outside the dimension Brooks argued does not mean Brooks would endorse H1 — the essence he identifies substantially overlaps this repository's four costs (decomposition, verification, composition, knowledge continuity). The two form a testable opposition: if those costs do not fall under reorganization, Brooks wins; if they fall substantially, H1 holds within its stated scope. Related: H1, the core thesis.

<a id="e11"></a>
### E11: The delayed payoff of electrification (David)

Paul A. David, 1990, *The Dynamo and the Computer: An Historical Perspective on the Modern Productivity Paradox*, American Economic Review 80(2) (Papers and Proceedings), 355–361, Department of Economics, Stanford University. [IDEAS record](https://ideas.repec.org/a/aea/aecrev/v80y1990i2p355-61.html), [full-text scan](http://digamo.free.fr/david90.pdf); longer 1989 working-paper version at [Warwick TWERP 339](https://warwick.ac.uk/fac/soc/economics/research/workingpapers/1989-1994/twerp339.pdf)

[Confirmed] David argues that factory electrification diffused slowly (electric motors accounted for under 5 percent of factory mechanical drive in 1899); early electrification replaced steam engines with electric motors as prime movers while leaving "the intra-plant power transmission system based on line shafts and belt drives essentially unchanged"; manufacturing productivity gains did not appear until the early 1920s, roughly four decades after the first central power stations; the gains came from redesigning factories around "unit drive" (an individual electric motor per machine), including single-story layouts and flexible machine placement, and about half of the 1919–29 acceleration in manufacturing productivity is statistically accounted for by growth in electric motor capacity.<br>
[Open] This interpretation is a canonical case in the general-purpose-technology literature, not a settled conclusion: Field (2003) argues 1929–41 was the most technologically progressive decade and shifts the center of gravity to transport and distribution; Crafts (2002) questions reading the multi-decade lag as an inevitability for ICT/AI; David himself cautions that "computers are not dynamos." The analogy frames the question; it does not answer it. Related: the README's central analogy, the core thesis's point of departure.

<a id="e12"></a>
### E12: Copilot randomized controlled experiment (lab task)

Sida Peng, Eirini Kalliamvakou, Peter Cihon, Mert Demirer (GitHub/Microsoft), 2023, *The Impact of AI on Developer Productivity: Evidence from GitHub Copilot*. [arXiv:2302.06590](https://arxiv.org/abs/2302.06590), [GitHub Blog summary](https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/)

[Confirmed] In a randomized controlled experiment, developers using Copilot completed the same HTTP-server task 55.8% faster, with no significant difference in completion rates between groups; the experiment only measured "writing done", not correctness and review cost.<br>
[Open] Single-task laboratory evidence cannot be generalized to overall productivity; it supports "generation-side speedup" but does not measure "delivery-side gains". Related: D1, Q2.

<a id="e13"></a>
### E13: Field randomized controlled experiments at three large companies

Kevin Zheyuan Cui, Mert Demirer, Sonia Jaffe, Leon Musolff, Sida Peng, Tobias Salz, 2024 (SSRN) → 2025, *The Effects of Generative AI on High-Skilled Work*. [NBER w34851](https://www.nber.org/system/files/working_papers/w34851/revisions/w34851.rev1.pdf), [Microsoft Research page](https://www.microsoft.com/en-us/research/publication/the-effects-of-generative-ai-on-high-skilled-work-evidence-from-three-field-experiments-with-software-developers/)

[Confirmed] Per the official abstract: pooling the three experiments with 4,867 developers, tasks completed +26.08% (SE 10.3%); developers with less experience showed higher adoption and gains; the metric is completions/PR counts, not quality and defect rates.<br>
[Open] Per-entry numbers in the full text were not directly verified because of SSRN anti-scraping; each experiment is individually noisy. Related: D1.

<a id="e14"></a>
### E14: NAV IT two-year longitudinal case

Viktoria Stray et al. (SINTEF/NAV IT, Norway), 2025–2026, *Developer Productivity With and Without GitHub Copilot*, HICSS-59. [arXiv:2509.20353](https://arxiv.org/abs/2509.20353)

[Confirmed] 703 repositories, 26,317 commits, 25 Copilot users versus 14 non-users: commit activity showed no statistically significant change after adopting Copilot, while perceived productivity rose.<br>
[Open] Single organization, commit volume as a proxy metric; shows that "perceived faster" and "output metrics" can decouple. Note: this case's direction does not fully match "faster generation → more awaiting verification"; it supports "perception–output decoupling" and does not directly support the verification bottleneck. Related: D1, D8.

<a id="e15"></a>
### E15: DORA 2025 State of AI-assisted Software Development

Google Cloud led, 2025. [dora.dev report page](https://dora.dev/dora-report-2025/), [ThoughtWorks summary](https://www.thoughtworks.com/en-us/insights/reports/the-2025-dora-report)

[Confirmed] Official conclusions: AI is an "amplifier" that amplifies an organization's existing strengths and weaknesses; individual efficiency and delivery speed gains coexist with rising system instability; the highest returns come from changing the underlying organizational systems rather than the tools themselves.<br>
[Open] Survey self-report data, correlational not causal; the third-party-reported 90% daily-usage figure was not verified against the original. Related: the README analogy, H1.

<a id="e16"></a>
### E16: Writing code vs. shipping code (NBER weak-link hypothesis)

Mert Demirer, Leon Musolff, Liyuan Yang, May 2026 (revised September), *Writing Code vs. Shipping Code: Productivity Effects Across Generations of AI Coding Tools*, NBER Working Paper 35275. [NBER page](https://www.nber.org/papers/w35275)

[Confirmed] (within its measurement scope) matched event study of 500,000+ GitHub developers: autocomplete, interactive agents, and autonomous agents raised commit volume +30% / +180% / +240% respectively, but project count only +80% and actual releases only +30%; the authors propose the "weak-link hypothesis": AI gains are attenuated by human-chain bottlenecks (review, integration, release); the human–AI substitution elasticity is only 0.23 (strong complementarity).<br>
[Open] Observational study of GitHub telemetry and market data; it quantifies "generation-end gains ≠ delivery-end gains" and is currently the strongest external quantitative support for this repository's "verification is the bottleneck". It also reports that across four software markets "the number of new applications surged while total usage did not grow", which is consistent with the "extra commits are low-value output" explanation — the decay gap is compatible with at least three explanations (low-value output, demand-side saturation, stricter review standards) and should not be read only as "verification is the hold-up". Related: D1, Q2, H1.

<a id="e17"></a>
### E17: Quality stock of generated code (commercial scan research group)

GitClear, 2025, *AI Copilot Code Quality: 2025 Look Back*. [Report page](https://www.gitclear.com/ai_assistant_code_quality_2025_research); similar: Veracode 2025 GenAI Code Security Report (45% of AI-generated code failed basic security tests, updated to 28–30% in spring 2026, [blog](https://www.veracode.com/blog/spring-2026-genai-code-security/)), Escape 2025 (5,600+ vibe-coded apps with 2,000+ vulnerabilities, [methodology](https://escape.tech/blog/methodology-how-we-discovered-vulnerabilities-apps-built-with-vibe-coding/)), Cloud Security Alliance 2026 (about 10% of 1,645 Lovable apps had vulnerable endpoints, [research note](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/))

[Confirmed] GitClear descriptive statistics over 211M lines of changes: duplicated code blocks roughly quadrupled; copy-paste lines rose from 8.3% to 12.3% (2021 → 2024); refactored lines fell from 25% to below 10%.<br>
[Open] Descriptive statistics from a commercial analytics company; methodology not peer-reviewed and causality unclear; the specific figures of the sub-sources (Veracode 45%/28–30%, Escape 2,000+ vulnerabilities, CSA about 10%) were not each independently verified; they can only show "the defect stock on the generation side is rising", not precise attribution. Related: D1, D6.

<a id="e18"></a>
### E18: METR long-task time horizons

Thomas Kwa et al. (METR), 2025 (NeurIPS 2025; v4 2026-07), *Measuring AI Ability to Complete Long Software Tasks*. [arXiv:2503.14499](https://arxiv.org/abs/2503.14499), [continuously updated page](https://metr.org/time-horizons/)

[Confirmed] "50% task-completion time horizon" method and measurements: Claude 3.7 Sonnet around 50 minutes in early 2025; roughly doubling every 7 months since 2019; the May 2026 FAQ gives GPT-5 about 2 hours 17 minutes; the paper explicitly warns about extrapolation risk.<br>
[Open] The task set consists of self-contained, well-defined, automatically scored "clean" tasks; agent performance drops sharply under holistic/human scoring; measurements beyond 16-hour tasks are unreliable. It distinguishes "rising capability" from "production trustworthiness" and does not solve the verification problem. Related: D1.

<a id="e19"></a>
### E19: OpenAI retires SWE-bench Verified

OpenAI, 2026-02-23, *Why SWE-bench Verified no longer measures frontier coding capabilities*. [Official page](https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/)

[Confirmed] Official audit of 138 tasks where models consistently fail: 59.4% of the test cases are themselves defective and reject functionally correct solutions; frontier models can reproduce human golden patches verbatim (training contamination); scores rose only 74.9% → 80.9% in the last six months; OpenAI retired the benchmark and recommends SWE-bench Pro.<br>
[Open] A stakeholder statement; SWE-bench Pro itself has drawn criticism ([LessWrong](https://www.lesswrong.com/posts/nAMhbz5sfpcynjPP5/swe-bench-pro-is-even-worse)). "About 60% of human-reviewed ground-truth tests are still defective" is strong supporting evidence for Q2's "who verifies the validators". Related: Q2, D1.

<a id="e20"></a>
### E20: Anthropic context engineering

Anthropic engineering blog, 2025-09-29, *Effective context engineering for AI agents*. [Link](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

[Confirmed] Official argument: context is a finite resource; more tokens bring "context rot", lowering model recall accuracy; attention budgets are consumed; engineering focus shifts from prompt engineering to context engineering (MCP, tools, history selection, iterative refinement).<br>
[Open] Not mutually exclusive with the "verification bottleneck"; its remedy direction is "feeding the right context" and it does not discuss production-organization reorganization. Related: D4, recorded as a competing view.

<a id="e21"></a>
### E21: Specification-driven development (industry and academia)

Den Delimarsky (GitHub), 2025-09, *Spec-driven development with AI*. [Blog](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/), [Spec Kit](https://github.com/github/spec-kit); Deepak Babu Piskala, 2026-01, *Spec-Driven Development: From Code to Contract in the Age of AI Coding Assistants*. [arXiv:2602.00180](https://arxiv.org/abs/2602.00180)

[Confirmed] GitHub: specs are "living, executable assets" and a shared source of truth; Specify → Plan → Tasks four phases, each phase may not enter the next before full verification. The academic version proposes a spec-first / spec-anchored / spec-as-source three-level strictness scale and a decision framework for "when SDD is not worth it".<br>
[Open] Process proposals, not effectiveness evidence; both assume spec writing itself is cheap and retain "humans read specs, humans do acceptance" at the center — more conservative than "kernel + periphery". Related: D8, acceptance-check-style interface, Q2.

<a id="e22"></a>
### E22: TDD benchmark (tests as specification)

Yi Cui et al., 2025-05, *Tests as Prompt: A Test-Driven-Development Benchmark for LLM Code Generation* (WebApp1K / TDD-Bench). [arXiv:2505.09027](https://arxiv.org/abs/2505.09027)

[Confirmed] 1,000 TDD tasks across 20 domains, 19 frontier models: instruction following and in-context learning matter more to success than general coding ability; instruction loss in long prompts is one of the main performance bottlenecks.<br>
[Open] The benchmark only tests "generate code once tests are given", not "who writes the tests and whether they are written correctly" — precisely the core gap of Q2. Related: D8, Q2.

<a id="e23"></a>
### E23: A systematic rebuttal to "ephemeral software / disposable implementation"

Andreas Kirsch (blackhc), 2026-03-18, *The Flawed Ephemeral Software Hypothesis*. [Link](https://www.blackhc.net/essays/future_of_software/)

[Confirmed] The essay concedes "generation became cheap" but asserts the bottleneck shifts to verification, integration, UX/edge cases (an Amdahl's-law analogy); it argues the future is malleable rather than ephemeral and that code remains the source of truth; it records supporting archives (Karpathy vibe coding, Vercel Rauch ephemeral apps, a16z Acharya [Disposable Software](https://a16z.com/disposable-software/), Tunguz [Ephemeral Software](https://tomtunguz.com/ephemeral-software), Replit Masad et al.) and rebuttal pillars (edge cases can only be exposed by production; state and integration surfaces make regeneration risk silent data corruption; interface-stability expectations make every regeneration introduce variance; it cites Brooks "grow, not build" and Spolsky's rewrite lessons).<br>
[Open] A long-form personal argument, not empirical.<br>
[Proposal] Its core dilemma must be answered head-on: constrained regeneration (read old code, diffs, logs, tests) → it is no longer ephemeral software; unconstrained → every regeneration round resets accumulated boundary knowledge. Related: RFC-0002, Q4.

<a id="e24"></a>
### E24: The improvement school (Kent Beck)

Kent Beck, from 2026-04, *Genie Tarpit* series (and *Nobody Wants Agents*). [tidyfirst.substack.com/p/genie-tarpit](https://tidyfirst.substack.com/p/genie-tarpit)

[Confirmed] Beck argues AI generates "plausible-looking but broken code" and complexity accumulates faster than humans can manage; the leverage is not better prompts but where the team sits on the "working features / changeable code" two axes; the remedy is outcome-oriented (describe what you want, let the system decide how), but he explicitly does not advocate overturning the existing engineering organization.<br>
[Open] Essay-style writing, personal judgment; represents the "incremental absorption" route. Related: H1 (should be made one of EX-08's control groups).

<a id="e25"></a>
### E25: AI assistants and insecure code (Stanford)

Neil Perry, Megha Srivastava, Deepak Kumar, Dan Boneh (Stanford), 2022 (arXiv)/CCS 2023, *Do Users Write More Insecure Code with AI Assistants?*. [arXiv:2211.03622](https://arxiv.org/abs/2211.03622)

[Confirmed] Experiment with 47 participants: participants with an AI assistant (Codex) wrote significantly more insecure code while being more confident they had written secure code — self-assessment of AI output systematically decouples from objective results.<br>
[Open] CTF/security-style small tasks, 2022 models, controlled experiment. Related: D1, D2, D3.

<a id="e26"></a>
### E26: Copilot code security assessment (NYU)

Hammond Pearce et al. (NYU), 2021 (arXiv)/IEEE S&P 2022, *Asleep at the Keyboard?*. [arXiv:2108.09293](https://arxiv.org/abs/2108.09293)

[Confirmed] 89 high-risk scenarios, 1,689 Copilot-generated programs, about 40% contained exploitable vulnerabilities.<br>
[Open] Scenarios constructed against CWE Top-25, function-level code, early models; "contains vulnerabilities" ≠ "entirely unusable"; real-world impact depends on human review filtering. Related: D1.

<a id="e27"></a>
### E27: SWE-Bench+ (inflated benchmarks)

Reem Aleithan, Haoran Xue et al. (York University), 2024, *SWE-Bench+: Enhanced Coding Benchmark for LLMs*. [arXiv:2410.06992](https://arxiv.org/abs/2410.06992)

[Confirmed] Manual case-by-case review of SWE-Agent+GPT-4 successful patches: 32.67% were "answer leakage" (issue text/comments directly gave the solution) and 31.08% passed by exploiting weak test cases; after removal, the resolution rate fell from 12.47% to 3.97%.<br>
[Open] Single agent+model combination, human annotation; shows "benchmark-reported resolution rates are inflated", indirectly supporting "verification is insufficient". Related: Q2, D1.

<a id="e28"></a>
### E28: Are SWE-bench "solved" patches actually correct

You Wang, Michael Pradel, Zhongxin Liu (University of Stuttgart), 2025, *Are "Solved Issues" in SWE-bench Really Solved Correctly?*, ISSTA 2025. [arXiv:2503.15223](https://arxiv.org/abs/2503.15223)

[Confirmed] Differential testing of three SOTA tools' patches on SWE-bench Verified: 7.8% counted as "correct" fail the developer test suite; 29.6% of "reasonable patches" behave differently from human ground truth (28.6% of those confirmed wrong); reported resolution rates are overestimated by 6.2 percentage points.<br>
[Open] Limited to SWE-bench Verified's verification mechanism; the most direct quantitative evidence that "benchmark pass ≠ correct". Related: Q2.

<a id="e29"></a>
### E29: Defect-detection ability of LLM-generated unit tests

Lin Yang et al. (Tianjin University/Huawei et al.), 2024, *On the Evaluation of Large Language Models in Unit Test Generation*. [arXiv:2406.18181](https://arxiv.org/abs/2406.18181)

[Confirmed] 17 Java projects, 5 open-source LLMs + GPT-4: LLM-generated unit tests have limited defect-detection ability, primarily because the tests' own validity is low (many tests fail to compile/pass or have invalid assertions).<br>
[Open] Unit-test granularity, Java projects; shows "using LLMs to generate validators" cannot be taken for granted and confirms "verification itself needs verification". Related: Q2.

<a id="e30"></a>
### E30: Error correlation in LLMs (cross-model)

Elliot Kim, Avi Garg, Kenny Peng, Nikhil Garg (Cornell et al.), 2025, *Correlated Errors in Large Language Models*. [arXiv:2506.07962](https://arxiv.org/abs/2506.07962)

[Confirmed] Empirical study of 350+ LLMs: when two models err simultaneously, about 60% of the time they err in the same place; larger, stronger models have highly correlated errors even across architectures/vendors.<br>
[Open] The evaluation targets reasoning/text tasks rather than code; error correlation is aggregate statistics and does not mean every specific problem is common-cause. Related: D5, Q6.

<a id="e31"></a>
### E31: Failure independence in LLM-generated code (code scenario)

Rodrigo Pato Nogueira, Karthik Pattabiraman, Marco Vieira, João R. Campos (UBC et al.), 2026 (arXiv preprint), *A Systematic Methodology for Evaluating Failure Independence in LLM-Generated Code*. [arXiv:2607.02808](https://arxiv.org/abs/2607.02808)

[Confirmed] 224 problems × 12 models × 5 languages: repeated implementations of the same model are structurally highly similar; under an N-version programming framework, three/five-version integration reliability gains are only 0.43/0.44 of what the independence assumption makes achievable, dropping below 0.3 for same-model ensembles; manual failure analysis shows "different failure modes often share the same root cause".<br>
[Open] 2026-07 preprint, no peer review yet; majority-voting/ensemble scenarios. It turns "common-cause failure" into a quantifiable failure-independence metric. Related: D5, Q6.

<a id="e32"></a>
### E32: Self-consistency (the boundary of multi-candidate gains)

Xuezhi Wang et al. (Google Research), 2022 (arXiv)/ICLR 2023, *Self-Consistency Improves Chain of Thought Reasoning in Language Models*. [arXiv:2203.11171](https://arxiv.org/abs/2203.11171)

[Confirmed] Sampling multiple reasoning paths + majority voting significantly improves accuracy on GSM8K and similar tasks; classic pass@k results (Codex: HumanEval pass@1≈28% → pass@100≈72%) likewise show that sampling has real gains.<br>
[Open] Reasoning tasks rather than code; majority voting presupposes "the majority agrees with the correct answer and sample errors do not fully overlap" — when all samples share the same bias/the same vague specification, voting amplifies the same error. It delimits, rather than denies, "multiple candidates are useless". Related: D5.

<a id="e33"></a>
### E33: Is self-repair a silver bullet

Theo X. Olausson et al. (MIT/ETH), 2023 (arXiv)/ICLR 2024, *Is Self-Repair a Silver Bullet for Code Generation?*. [arXiv:2306.09896](https://arxiv.org/abs/2306.09896)

[Confirmed] Self-repair gains are capped by the model's own feedback ability: effective with strong external feedback (real tests), almost no gain with model-generated feedback; under a fixed budget, "diverse initial candidates" beat "repeatedly repairing the same candidate".<br>
[Open] MBPP/HumanEval-style function-level tasks, GPT-3.5/4 era. Related: D5, D6.

<a id="e34"></a>
### E34: Chain-of-thought explanations can be unfaithful

Miles Turpin et al. (Anthropic/MIT), 2023 (arXiv)/NeurIPS 2023, *Language Models Don't Always Say What They Think*. [arXiv:2305.04388](https://arxiv.org/abs/2305.04388)

[Confirmed] By introducing biased leading questions, models can be made to systematically change their answers while their CoT explanations still fabricate a self-consistent but wrong rationale — explanations decouple from the actual reasoning process, and the more fluent, the more misleading.<br>
[Open] Text reasoning tasks (GSM8K etc.); it demonstrates "inducible unfaithfulness", not a claim that explanations are always unfaithful. It directly destroys the argument that "explanations can serve as correctness evidence". Related: D2, separate generation from acceptance.

<a id="e35"></a>
### E35: LLM-generated code comments are inaccurate

Sungmin Kang, Louis Milliken, Shin Yoo (KAIST), 2024, *Identifying Inaccurate Descriptions in LLM-generated Code Comments via Test Execution*. [arXiv:2406.14836](https://arxiv.org/abs/2406.14836)

[Confirmed] Evaluating Java comments generated by 3 LLMs: even the best model had about one-fifth (≈20%) of comments containing verifiably inaccurate statements; existing "comment–code consistency detection" techniques show no statistically significant effect at identifying inaccurate comments; the authors advocate "documentation testing" — generate tests from documentation and run them, using external execution evidence to validate documentation.<br>
[Open] Java, comment-level; "inaccurate" judged by verifiable statements; another 2026 study ([ACM 3786175](https://dl.acm.org/doi/10.1145/3786175.3788344)) reports that under expert scoring 58.8% of AI comments match human-written quality — the two do not contradict (quality perception vs. factual accuracy), but suggest this repository's claim should focus on "factual accuracy/consistency with behavior". Related: D2 (two skins).

<a id="e36"></a>
### E36: Models cannot self-correct

Jie Huang et al. (DeepMind), 2023 (arXiv)/ICLR 2024, *Large Language Models Cannot Self-Correct Reasoning Yet*. [arXiv:2310.01798](https://arxiv.org/abs/2310.01798)

[Confirmed] Without external feedback, asking models to self-check and self-correct does not improve accuracy and can lower it — "self-assessment" is not verification.<br>
[Open] Reasoning tasks. Related: D2, D3.

<a id="e37"></a>
### E37: The "end of code review" argument (position paper)

Martin Monperrus, 2026, *The End of Code Review: Coding Agents Supersede Human Inspection*. [arXiv:2606.13175](https://arxiv.org/abs/2606.13175)

[Confirmed] The paper argues "human review throughput does not grow with AI output; the bottleneck and productivity gains scale proportionally".<br>
[Open] This is an argumentative position paper rather than a measurement study, and must be attributed as such when cited; only the bibliographic record was confirmed by search, without reading the full text. Related: D1.

## Leads awaiting verification

[Open] The following appear in the source materials; this edition has not completed primary-source verification or has only partial coverage:

- Common-failure research on different implementations: partially covered (E30, E31), but field data from real team workflows is missing;
- Test-suite overfitting in automated repair: no direct study yet; defects in test suites themselves already have supporting evidence (E19, E27, E28);
- Exact correspondence between cellular Potts models, differential adhesion, collective robotics, and these prototypes;
- The debate and archives on live-generation products and disposable software are covered (E23), but empirical performance figures remain unverified;
- Mathematical mappings among diffusion, control, evolution, and this proposal.

[Open] The lead "historical causal interpretations of electrification productivity" from the original list was verified on 2026-09-15 and moved to checked references ([E11](#e11)); its causal interpretation remains a contested research conclusion, not settled fact.

[Proposal] Prefer original papers, author materials, official implementations, and repeatable data. Register the exact title, authors or institution, date, direct URL, linked claim, and supported and unsupported scope. Search snippets alone are insufficient.

## Updating status and correcting errors

[Proposal] A status-changing pull request records old and new statuses, evidence IDs, alternative explanations, and scope. Counterexamples may narrow a confirmed finding or return it to open status; retain history. Without project data, do not state success rates, performance gains, or that a new paradigm has been proven.
