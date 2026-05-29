# Awesome Operational Grounding [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of research, tools, and standards for **Automated Operational Grounding Construction (AOGC)** — using LLMs to build and maintain the structured layer that connects enterprise schemas, constraints, actions, policies, and versions to agent behavior.

Companion to the survey *Scaling Enterprise Agent Deployment: A Survey of LLM-Based Operational Grounding Construction* (Bai et al., 2026). The survey codes **32 core LLM construction methods**, **5 supporting validators/representations**, and **1 adjacent enterprise-agent architecture** across five functional dimensions and three autonomy tiers.

## Contents

- [What is operational grounding?](#what-is-operational-grounding)
- [Survey & nearby surveys](#survey--nearby-surveys)
- [Autonomy tiers](#autonomy-tiers)
- [Core methods — Tier 1 (subtask tools)](#core-methods--tier-1-subtask-tools)
- [Core methods — Tier 2 (pipeline engines)](#core-methods--tier-2-pipeline-engines)
- [Core methods — Tier 3 (construction agents)](#core-methods--tier-3-construction-agents)
- [Supporting representations & validators](#supporting-representations--validators)
- [Adjacent enterprise architectures](#adjacent-enterprise-architectures)
- [Schema-level extraction (extended D1 corpus)](#schema-level-extraction-extended-d1-corpus)
- [Action, process & tool construction (extended D3 corpus)](#action-process--tool-construction-extended-d3-corpus)
- [Governance & compliance (extended D4 corpus)](#governance--compliance-extended-d4-corpus)
- [Maintenance & evolution (extended D5 corpus)](#maintenance--evolution-extended-d5-corpus)
- [Agent benchmarks (downstream evaluation)](#agent-benchmarks-downstream-evaluation)
- [Standards & formal foundations](#standards--formal-foundations)
- [Enterprise context](#enterprise-context)
- [Related awesome lists](#related-awesome-lists)
- [Contributing](#contributing)

## What is operational grounding?

Enterprise LLM agents need more than a vocabulary. They need a linked **operational grounding layer** \(\mathcal{O}=\langle V,C,A,G,M\rangle\):

| Dim. | Layer | Role | Typical artifacts |
|------|-------|------|-------------------|
| **D1** | \(V\) Vocabulary | Entity and relationship structure for interpreting state | OWL/RDFS, taxonomies, DB/API type mappings |
| **D2** | \(C\) Constraints | Valid states, derivations, violation checks | SHACL/ShEx, OWL axioms, business rules |
| **D3** | \(A\) Actions | Callable operations and process dynamics | PDDL, BPMN, OpenAPI, tool contracts |
| **D4** | \(G\) Governance | Normative control over actions and data | RBAC/ABAC, privacy vocabularies, policy rules |
| **D5** | \(M\) Maintenance | Change, provenance, consistency over time | Ontology versioning, RDF deltas, temporal KGs |

**AOGC** is LLM-based construction, validation, or maintenance of these artifacts from heterogeneous enterprise sources (schemas, API docs, workflows, policies, release notes). Success is measured by cross-artifact fidelity and downstream agent behavior, not standalone extraction accuracy.

## Survey & nearby surveys

- *Scaling Enterprise Agent Deployment: A Survey of LLM-Based Operational Grounding Construction* (Bai et al., 2026) — Defines AOGC, the five-dimension framework, three-tier autonomy taxonomy, coded evidence map (32 core methods), and realism-gap analysis. **Primary reference for this list.**
- [LLMs for Ontology Engineering: A Landscape of Tasks and Benchmarking Challenges](https://ceur-ws.org/Vol-3953/) (Garijo et al., 2024) — Ontology-engineering task landscape; broader than enterprise agent grounding ([paper PDF](https://ceur-ws.org/Vol-3953/364.pdf)).
- [Large Language Models for Ontology Engineering: A Systematic Literature Review](https://content.iospress.com/articles/semantic-web/sw240001) (Li et al., 2025) — Systematic review of LLM ontology engineering.
- [LLM-Empowered Knowledge Graph Construction: A Survey](https://arxiv.org/abs/2510.20345) (Bian, 2025) — KG construction survey; instance population focus rather than schema-level grounding.
- [LLMs4OL: Large Language Models for Ontology Learning](https://link.springer.com/chapter/10.1007/978-3-031-47243-4_25) (Babaei Giglou et al., 2023) — Benchmark suite for isolated ontology-learning subtasks. **D1** · **T1** · benchmark
- [From Automation to Autonomy: A Survey on LLMs in Scientific Discovery](https://aclanthology.org/2025.emnlp-main.895/) (Zheng et al., 2025) — Autonomy framing adapted in the AOGC survey.

## Autonomy tiers

| Tier | LLM role | Human role | Status in coded corpus |
|------|----------|------------|------------------------|
| **T1** Subtask tool | One predefined extraction, translation, or validation step | Selects inputs, integrates output | 7 core methods |
| **T2** Pipeline engine | Fixed multi-step construction + external checking | Defines scope, accepts/rejects artifact | 25 core methods |
| **T3** Construction agent | Plans strategy, identifies missing artifacts, maintains linked layer | Sets goals, acceptance testing | **0 core methods** (open problem) |

## Core methods — Tier 1 (subtask tools)

### D1 — Vocabulary & schema structure

- [LLMs4OL](https://link.springer.com/chapter/10.1007/978-3-031-47243-4_25) — Controlled benchmark for term typing, taxonomy edges, and relation extraction ([code](https://github.com/HamedBabaei/LLMs4OL)). **D1** · **T1** · benchmark

### D2 — Constraints & rules

- [NL-to-OWL Axioms (Ontology Engineering with LLMs)](https://arxiv.org/abs/2307.16699) (Mateiu & Groza, 2023) — Translates bounded natural language into OWL/DL axioms with logical validation. **D2** · **T1** · method
- [OntoAxiom](https://arxiv.org/abs/2512.05594) (Bakker et al., 2025) — Benchmark for axiom identification over existing ontologies ([code](https://gitlab.com/ontologylearning/axiomidentification)). **D2** · **T1** · benchmark
- [Declare Constraint Extraction](https://doi.org/10.1016/j.dss.2026.114627) (Park et al., 2026) — Extracts declarative process constraints from NL descriptions ([code](https://github.com/gyunamister/nl2declare)). **D2 D3 D4** · **T1** · benchmark
- [Business as Rulesual (BREX/ExIde)](https://arxiv.org/abs/2505.18542) (Yang et al., 2025) — Benchmark and framework for business rule flow modeling ([code](https://github.com/oYoungCo/Business-as-Rulesual)). **D2 D3 D4** · **T1** · benchmark

### D3 — Actions & processes

- [PAGED](https://aclanthology.org/2024.acl-long.583/) (Du et al., 2024) — Benchmark for procedural graph extraction from documents ([code](https://github.com/SCUNLP/PAGED)). **D1 D2 D3** · **T1** · benchmark

### D5 — Maintenance

- [When Facts Expire](https://github.com/SoulardThibaut/WhenFactExpire) (Soulard et al., 2025) — Benchmarks temporal validity in knowledge graphs (CIKM 2025). **D1 D5** · **T1** · benchmark

## Core methods — Tier 2 (pipeline engines)

### D1 — Ontology & vocabulary construction

- [NeOn-GPT](https://link.springer.com/chapter/10.1007/978-3-031-47243-4_2) (Fathallah et al., 2024) — LLM pipeline for ontology learning with reasoner and OOPS! feedback ([code](https://github.com/andreamust/NEON-GPT)). **D1 D2 D5** · **T2** · system
- [Ontogenia](https://link.springer.com/chapter/10.1007/978-3-031-94575-5_18) (Lippolis et al., 2025) — End-to-end ontology generation with pitfall detection and expert review ([code](https://github.com/dersuchendee/Onto-Generation)). **D1 D2** · **T2** · system
- [OntoGenix](https://doi.org/10.1016/j.ipm.2024.103876) (Val-Calvo et al., 2024) — Dataset-driven ontology engineering with LLM assistance and expert evaluation ([code](https://github.com/tecnomod-um/OntoGenix)). **D1 D2 D5** · **T2** · system
- [AutoSchemaKG](https://arxiv.org/abs/2505.23628) (Bai et al., 2025) — Autonomous KG construction with dynamic schema induction from web-scale corpora; builds ATLAS family of graphs ([code](https://github.com/HKUST-KnowComp/AutoSchemaKG)). **D1** · **T2** · system
- [Intention KG (IGC-RC)](https://aclanthology.org/2026.eacl-long.21/) (Bai et al., 2026) — Constructs relational intention graphs from behavioral session data for intention prediction and recommendation ([code](https://github.com/HKUST-KnowComp/RelationalIntentionGraph)). **D1 D3** · **T2** · system
- [AutoGraph-R1](https://arxiv.org/abs/2510.15339) (Tsang et al., 2025) — RL-optimizes KG construction for downstream RAG/QA performance with task-aware reward functions ([code](https://github.com/HKUST-KnowComp/AutoGraph-R1)). **D1** · **T2** · method
- [Capability Ontologies with LLMs](https://arxiv.org/abs/2404.17524) (Vieira da Silva et al., 2024) — Generates capability ontologies with OWL/SHACL validation ([code](https://github.com/CaSkade-Automation/LLM4Cap)). **D1 D2 D3** · **T2** · method

### D2 — Constraints, shapes & KG rules

- [ShEx Schema Generation for Large KGs](https://aclanthology.org/2025.findings-emnlp.671/) (Zhang et al., 2025) — LLM-generated ShEx schemas over large knowledge graphs ([code](https://github.com/King-s-Knowledge-Graph-Lab/shapespresso)). **D2** · **T2** · method
- [AutomationML + SHACL Validation](https://arxiv.org/abs/2506.10678) (Westermann et al., 2025) — Validates textual constraints against AutomationML via LLMs and SHACL execution ([code](https://github.com/hsu-aut/aml-shacl)). **D2 D4** · **T2** · method
- [SHACL Repair with LLMs](https://arxiv.org/abs/2507.22419) (Lin et al., 2025) — Systematic KG repair driven by SHACL violation reports (no public code found). **D2 D5** · **T2** · method
- [ChatRule](https://arxiv.org/abs/2309.01538) (Luo et al., 2023) — Mines logical KG rules with LLMs for downstream reasoning ([code](https://github.com/RManLuo/ChatRule)). **D2** · **T2** · method

### D3 — Planning, workflows & API contracts

- [Generalized Planning in PDDL Domains with LLMs](https://ojs.aaai.org/index.php/AAAI/article/view/30006) (Silver et al., 2024) — LLM-assisted PDDL domain debugging and task solving ([code](https://github.com/tomsilver/llm-genplan)). **D2 D3** · **T2** · method
- [World-Model PDDL Construction](https://arxiv.org/abs/2305.14909) (Guan et al., 2023) — Constructs PDDL world models from NL for model-based planning ([code](https://github.com/GuanSuns/LLMs-World-Models-for-Planning)). **D2 D3** · **T2** · system
- [NL2Plan](https://arxiv.org/abs/2405.04215) (Gestrin et al., 2024) — Robust LLM-driven planning from minimal text with planner validation ([code](https://github.com/mrlab-ai/NL2Plan)). **D2 D3** · **T2** · system
- [Planning-Domain Generation](https://ojs.aaai.org/index.php/ICAPS/article/view/31502) (Oswald et al., 2024) — LLMs as PDDL domain generators with plan-set comparison ([code](https://github.com/IBM/NL2PDDL)). **D2 D3** · **T2** · benchmark
- [Consistent PDDL Generation](https://arxiv.org/abs/2404.07751) (Smirnov et al., 2024) — Generates internally consistent PDDL domains with consistency checks ([artifacts](https://github.com/HRI-EU/pddl-domains)). **D2 D3** · **T2** · method
- [Process-Model Benchmark (LLM BPM)](https://link.springer.com/article/10.1007/s10270-025-01318-w) (Kourani et al., 2025) — Framework and benchmark for LLM business process modeling with conformance testing ([code](https://github.com/humam-kourani/EvaluatingLLMsProcessModeling)). **D2 D3** · **T2** · benchmark
- [BPMNGen](https://link.springer.com/article/10.1007/s12599-025-00983-x) (Hörner et al., 2026) — Generates BPMN 2.0 models from NL process descriptions with quality assessment. **D3** · **T2** · system
- [text2flow](https://aclanthology.org/2026.findings-eacl.158/) (Ying et al., 2026) — Multi-agent procedural graph extraction with structural and logical refinement via simulation. **D2 D3** · **T2** · system
- [SOPStruct](https://arxiv.org/abs/2504.00029) (Garg et al., 2025) — Structured plan representation of procedures with PDDL soundness checks. **D2 D3** · **T2** · system
- [OASBuilder](https://aclanthology.org/2025.acl-industry.18/) (Lazar et al., 2025) — Generates OpenAPI specifications from online API documentation. **D2 D3** · **T2** · system

### D4 — Governance & compliance

- [PrivComp-KG](https://arxiv.org/abs/2404.19744) (Garza et al., 2024) — KG + LLM pipeline for privacy policy compliance verification. **D2 D4** · **T2** · system
- [ComplianceNLP](https://arxiv.org/abs/2604.23585) (Guo et al., 2026) — KG-augmented RAG for multi-framework regulatory gap detection ([code](https://github.com/bettyguo/ComplianceNLP)). **D2 D4 D5** · **T2** · system
- [RAGulating Compliance](https://arxiv.org/abs/2508.09893) (Agarwal et al., 2025) — Multi-agent KG for regulatory QA. **D2 D4** · **T2** · system

### D5 — Maintenance & temporal reasoning

- [TimeR⁴](https://aclanthology.org/2024.emnlp-main.394/) (Qian et al., 2024) — Time-aware RAG for temporal KG question answering ([code](https://github.com/qianxinying/TimeR4)). **D1 D5** · **T2** · method

## Core methods — Tier 3 (construction agents)

No coded core method yet autonomously chooses missing D1–D5 construction and maintenance actions across heterogeneous enterprise sources. This remains the primary open target for AOGC research.

**Early adjacent signals** (not counted as core Tier 3):

- [End-to-End PDDL Planning with Dynamic Agents](https://arxiv.org/abs/2512.09629) (La Malfa et al., 2025) — Agentic PDDL construction with verifier feedback.
- [ContextCov](https://arxiv.org/abs/2603.00822) (Sharma, 2026) — Derives executable constraints from agent instruction files.
- [Ontology-to-Tools Compilation](https://arxiv.org/abs/2602.03439) (Zhou et al., 2026) — Compiles ontologies into enforceable semantic constraints for LLM agents.

## Supporting representations & validators

These works define target languages, validators, or infrastructure that AOGC pipelines compile into or check against. Marked **S** in the survey evidence map.

- [Compiling SHACL into SQL](https://link.springer.com/chapter/10.1007/978-3-031-71834-7_28) (Jakubowski & Van den Bussche, 2024) — Makes SHACL constraints executable at database scale ([code](https://github.com/MaximeJakubowski/shaclsql-supplementary)). **D2** · validator
- [Data Privacy Vocabulary (DPV) v2](https://w3id.org/dpv) (Pandit et al., 2024) — Privacy vocabulary for policy-oriented constraint targets. **D2 D4** · representation
- [Explainable DPV/SHACL Validation](https://link.springer.com/chapter/10.1007/978-3-032-25156-5_21) (Hernandez & Pandit, 2026) — Human-in-the-loop validation of data sharing agreements (ESWC 2026). **D2 D4** · method
- [KGHeartBeat](https://github.com/isislab-unisa/KGHeartBeat) (Pellegrino et al., 2025) — KG quality assessment and diagnostic signals ([web app](https://kgheartbeat.di.unisa.it)). **D2 D5** · tool
- [OntoEditor](https://github.com/ahemaid/OntoEditor) (Hemid et al., 2024) — Distributed version control for collaborative ontology development. **D2 D5** · tool
- [Jelly-Patch](https://github.com/Jelly-RDF/jelly-jvm) (Sowinski et al., 2025) — Fast RDF delta format for recording graph changes. **D5** · representation

## Adjacent enterprise architectures

Marked **A** in the survey — inform the Tier 3 target but do not autonomously construct linked D1–D5 artifacts from domain sources.

- [FAOS](https://arxiv.org/abs/2604.00555) (Luong Tuan & Sanyal, 2026) — Ontology-constrained neurosymbolic architecture for domain-grounded enterprise agents; couples runtime grounding to agent tasks. **D1–D5** · adjacent

## Schema-level extraction (extended D1 corpus)

Tier-1 building blocks cited in the survey for entity, relation, and schema-conditioned extraction. Most are **T1** subtask tools.

- [ChatIE](https://arxiv.org/abs/2302.10205) (Wei et al., 2023) — Zero-shot IE via conversational prompting. **D1** · **T1**
- [Large Language Models as Clinical IE](https://aclanthology.org/2022.emnlp-main.130/) (Agrawal et al., 2022) — Few-shot schema-level extraction in clinical domains. **D1** · **T1**
- [Aligning Instruction Tasks for Zero-Shot RE](https://aclanthology.org/2023.findings-acl.50/) (Zhang et al., 2023) — Instruction alignment unlocks zero-shot relation extraction. **D1** · **T1**
- [GPT-RE](https://aclanthology.org/2023.emnlp-main.214/) (Wan et al., 2023) — In-context learning for relation extraction. **D1** · **T1**
- [InstructUIE](https://arxiv.org/abs/2304.08085) (Wang et al., 2023) — Multi-task instruction tuning for unified information extraction ([code](https://github.com/BeyonderXX/InstructUIE)). **D1** · **T1**
- [IEPile](https://aclanthology.org/2024.acl-short.13/) (Gui et al., 2024) — Large-scale schema-conditioned IE corpus. **D1** · benchmark
- [UniversalNER](https://openreview.net/forum?id=r65xfUb76p) (Zhou et al., 2024) — Targeted distillation for open NER. **D1** · **T1**
- [GoLLIE](https://openreview.net/forum?id=Y3wpuxd7u9) (Sainz et al., 2024) — Annotation guidelines improve zero-shot IE ([code](https://github.com/hitz-zentroa/GoLLIE)). **D1** · **T1**
- [CodeIE](https://aclanthology.org/2023.acl-long.855/) (Li et al., 2023) — Code LMs as few-shot extractors. **D1** · **T1**
- [CodeKGC](https://doi.org/10.1145/3641850) (Bi et al., 2024) — Code LM for generative KG schema construction ([code](https://github.com/zjunlp/DeepKE/tree/main/example/llm/CodeKGC)). **D1** · **T1**
- [Zero/Few-Shot KG Triplet Extraction](https://aclanthology.org/2024.kallm-1.2/) (Papaluca et al., 2024) — LLM triplet extraction with minimal supervision. **D1** · **T1**
- [Ontology-Guided KG Construction from Short Texts](https://aclanthology.org/2024.kallm-1.8/) (van Cauter & Yakovets, 2024) — Schema-guided construction from maintenance texts. **D1** · **T1**
- [Fine-Tuning for Triple Extraction](https://aclanthology.org/2024.kallm-1.12/) (Zhang et al., 2024) — Data augmentation for triple extraction. **D1** · **T1**
- [PLRTE](https://doi.org/10.1016/j.jbi.2024.104738) (Zheng et al., 2024) — Progressive learning for biomedical relation triplet extraction. **D1** · **T1**

## Action, process & tool construction (extended D3 corpus)

Additional D3-relevant work beyond the 32 core coded rows.

- [Exploring ChatGPT for Event Extraction](https://arxiv.org/abs/2303.03836) (Gao et al., 2023) — Feasibility study for event extraction with LLMs. **D3** · **T1**
- [Human Evaluation of Procedural KG Extraction](https://arxiv.org/abs/2412.03589) (Carriero et al., 2024) — Procedural KG extraction from text with human evaluation. **D3** · **T1**
- [Precondition and Effect Knowledge (World Models)](https://aclanthology.org/2025.coling-main.503/) (Xie et al., 2025) — LLMs as world models with precondition/effect structure. **D3** · **T1**
- [LLM+P](https://arxiv.org/abs/2304.11477) (Liu et al., 2023) — Combines LLMs with classical planners for optimal planning. **D3** · **T2**
- [Process Modeling with LLMs](https://arxiv.org/abs/2403.07541) (Kourani et al., 2024) — LLM-based business process model generation. **D3** · **T2**
- [LLM-Based BPM Generation from Text](https://aclanthology.org/2025.findings-ijcnlp.31/) (Li et al., 2025) — Text-to-business-process-model pipeline. **D3** · **T2**
- [Large Language Models for BPM Tasks](https://arxiv.org/abs/2307.09923) (Grohs et al., 2024) — LLMs on business process management tasks. **D3** · **T1**
- [SpeCrawler](https://arxiv.org/abs/2402.11625) (Lazar et al., 2024) — OpenAPI generation from API documentation. **D3** · **T2**
- [ToolFactory](https://arxiv.org/abs/2501.16945) (Ni et al., 2025) — Automates tool generation from REST API documentation ([code](https://github.com/coolkillercat/ToolFactory-review)). **D3** · **T2**
- [Doc2Agent](https://arxiv.org/abs/2506.19998) (Ni et al., 2025) — Scalable tool-using agent generation from API docs ([code](https://github.com/coolkillercat/Doc2Agent)). **D3** · **T2**
- [Gorilla](https://arxiv.org/abs/2305.15334) (Patil et al., 2024) — LLM connected with massive APIs for tool use ([code](https://github.com/ShishirPatil/gorilla)). **D3** · **T1**
- [Toolformer](https://papers.nips.cc/paper_files/paper/2023/hash/d842425e4bf79ba039352da0f658a906-Abstract-Conference.html) (Schick et al., 2023) — Self-supervised tool-use learning. **D3** · foundation
- [ReAct](https://openreview.net/forum?id=WE_vluYUL-X) (Yao et al., 2023) — Synergizes reasoning and acting in language models. **D3** · foundation

## Governance & compliance (extended D4 corpus)

- [KG Ecosystem Life Cycles](https://www.vldb.org/pvldb/vol18/p1390-geisler.pdf) (Geisler et al., 2025) — Managing KG ecosystems from genesis to maturity (PVLDB 2025 vision paper). **D4 D5** · adjacent
- [Semantic Technologies for Global Governance](https://link.springer.com/chapter/10.1007/978-3-031-94578-6_7) (Nuzzolese et al., 2025) — Hybrid AI for tracking WHO resolutions. **D4** · adjacent

## Maintenance & evolution (extended D5 corpus)

- [Continual Few-Shot KGC](https://doi.org/10.1145/3627673.3679734) (Li et al., 2024) — Learning from novel knowledge over time ([code](https://github.com/cfkgc-paper/CFKGC-paper)). **D5** · adjacent
- [SAGE: Scale-Aware Gradual KG Evolution](https://arxiv.org/abs/2508.11347) (Li et al., 2025) — Continual KG embedding under scale change (KDD 2025). **D5** · adjacent
- [UniEdit](https://arxiv.org/abs/2503.07372) (Chen et al., 2025) — Unified knowledge editing benchmark for LLMs. **D5** · benchmark
- [Retrieval-Enhanced Knowledge Editing](https://arxiv.org/abs/2403.19631) (Shi et al., 2024) — Multi-hop QA via retrieval-enhanced editing (CIKM 2024) ([code](https://github.com/sycny/RAE)). **D5** · method
- [LLM-Guided Dynamic Adaptation for Temporal KG Reasoning](https://proceedings.neurips.cc/paper_files/paper/2024/file/8b3c966fb5b4d2e12391e6291e634da0-Paper-Conference.pdf) (Hu et al., 2024) — Temporal KG reasoning with dynamic adaptation (NeurIPS 2024). **D5** · method
- [Chain-of-History Reasoning](https://aclanthology.org/2024.findings-acl.372/) (Xia et al., 2024) — History-aware temporal KG forecasting. **D5** · method
- [Quality Without Borders](https://ceur-ws.org/Vol-4085/paper21.pdf) (Tuozzo, 2025) — Modular unified KG quality assessment (ISWC 2025 doctoral consortium). **D5** · method

**Agentic maintenance analogues** (skill/workflow evolution, not full AOGC):

- [Voyager](https://arxiv.org/abs/2305.16291) (Wang et al., 2024) — Open-ended embodied agent with skill library ([code](https://github.com/MineDojo/Voyager)). **D5** · analogue
- [SEW: Self-Evolving Agentic Workflows](https://arxiv.org/abs/2505.18646) (Liu et al., 2025) — Self-evolving workflows for code generation. **D5** · analogue
- [SkillForge](https://arxiv.org/abs/2604.08618) (Liu et al., 2026) — Domain-specific self-evolving agent skills. **D5** · analogue
- [CoEvoSkills](https://arxiv.org/abs/2604.01687) (Zhang et al., 2026) — Co-evolutionary verification for agent skills. **D5** · analogue
- [Frontier-Eng](https://arxiv.org/abs/2604.12290) (Chi et al., 2026) — Self-evolving agents on real-world engineering tasks. **D5** · benchmark

## Agent benchmarks (downstream evaluation)

These evaluate agent behavior assuming grounding is already supplied — complementary to AOGC construction research.

- [SWE-bench](https://openreview.net/forum?id=VTF8yNQM66) (Jimenez et al., 2024) — Real-world GitHub issue resolution ([code](https://github.com/SWE-bench/SWE-bench)).
- [WebArena](https://arxiv.org/abs/2307.13854) (Zhou et al., 2024) — Realistic web environment for autonomous agents ([code](https://github.com/web-arena-x/webarena)).
- [GAIA](https://openreview.net/forum?id=fibxvahvs3) (Mialon et al., 2024) — General AI assistant benchmark.
- [AgentBench](https://arxiv.org/abs/2308.03688) (Liu et al., 2023) — Multi-environment agent evaluation.
- [τ-bench](https://arxiv.org/abs/2406.12045) (Yao et al., 2024) — Tool-agent-user interaction in real-world domains.

## Standards & formal foundations

Target representation languages and classical foundations referenced by the survey framework.

- [OWL 2 Structural Specification](https://www.w3.org/TR/2012/REC-owl2-syntax-20121211/) (W3C, 2012) — **D1**
- [SHACL](https://www.w3.org/TR/shacl/) (W3C, 2017) — **D2**
- [JSON Schema Validation](https://json-schema.org/draft/2020-12/json-schema-validation) (Wright et al., 2022) — **D2**
- [SWRL](https://www.w3.org/submissions/2004/SUBM-SWRL-20040521/) (Horrocks et al., 2004) — **D2**
- [PDDL](https://planning.wiki/_citedpapers/pddl1998.pdf) (McDermott et al., 1998) — **D3**
- [HTN / UMCP](https://www.cs.umd.edu/~nau/papers/erol1994umcp.pdf) (Erol et al., 1994) — **D3**
- [BPMN 2.0](https://www.omg.org/spec/BPMN/2.0.2/About-BPMN) (OMG, 2014) — **D3**
- [OWL-S](https://www.w3.org/Submission/OWL-S/) (Martin et al., 2004) — **D3**
- [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.1.html) (OpenAPI Initiative, 2024) — **D3**
- [Knowledge Engineering: Principles and Methods](https://doi.org/10.1016/S0169-023X(97)00056-6) (Studer et al., 1998) — Classical ontology engineering foundations.
- [A Translation Approach to Portable Ontology Specifications](https://doi.org/10.1006/knac.1993.1008) (Gruber, 1993) — Foundational ontology definition.
- [Formal Ontology and Information Systems](https://doi.org/10.3233/978-1-58603-933-8-3-15) (Guarino, 1998) — Formal ontology in IS.

## Enterprise context

Industry signals and protocols motivating operational grounding construction.

- [Model Context Protocol (MCP)](https://spec.modelcontextprotocol.io/specification/2024-11-05/) (Anthropic, 2024) — Standardizes LLM connections to data, tools, and authorization-sensitive capabilities.
- [OpenAI Forward Deployed Engineering](https://openai.com/business/the-openai-deployment-company/) (OpenAI, 2026) — Enterprise AI delivery pattern embedding engineers with users.
- [Anthropic Enterprise AI Services](https://www.anthropic.com/news/enterprise-ai-services-company) (Anthropic, 2026) — Enterprise AI deployment company announcement.
- [ServiceNow × Accenture FDE Program](https://newsroom.accenture.com/news/2026/servicenow-and-accenture-launch-forward-deployed-engineering-program-to-scale-agentic-ai-across-the-enterprise) (2026) — Forward-deployed engineering for agentic AI at scale.
- [Palantir SEC Form 10-K (FDE pattern)](https://www.sec.gov/Archives/edgar/data/1321655/000119312521060650/d65934d10k.htm) (Palantir, 2021) — Embedded engineers surfacing product needs from field deployments.

## Related awesome lists

- [Awesome Knowledge Graph](https://github.com/shaoxiongji/awesome-knowledge-graph) — General KG resources.
- [Awesome Semantic Web](https://github.com/semantalytics/awesome-semantic-web) — Semantic Web and ontology engineering resources.
- [Awesome LLM Agents](https://github.com/kaushikb11/awesome-llm-agents) — LLM agent systems and tooling.
- [Awesome MCP Servers](https://github.com/punkpeye/awesome-mcp-servers) — MCP server implementations.

## Contributing

Contributions welcome! Please read [contributing.md](contributing.md) before opening a pull request.

**In scope:** LLM-based construction, validation, or maintenance of schema-level grounding artifacts (D1–D5); benchmarks and validators directly supporting AOGC; adjacent enterprise grounding architectures.

**Out of scope:** Pure instance-level KG population, ontology usage without construction, general LLM surveys unrelated to grounding layers.

---

Maintained by [HKBU KnowComp](https://github.com/HKBU-KnowComp). If you use this list in research, please cite the AOGC survey (Bai et al., 2026).
