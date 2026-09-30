# Enterprise AI OS [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> **The operating system for enterprise AI — build it, run it, and keep it under control.** A curated
> map of the whole AI estate: the models, agents, orchestration, memory, knowledge, and data an
> enterprise *runs* — and the security, identity, access control, observability, and governance that
> keep it *under control* — for an era of increasingly autonomous AI.

Think of it like an operating system. An OS **runs** processes, manages **memory**, handles
**identity and access**, brokers **I/O**, and **monitors and protects** everything on the machine.
Enterprise AI needs the same — but across fleets of models, agents, tools, and knowledge, at company
scale. This list is that OS, mapped in two halves: **Build** (what it runs) and **Control** (how it
stays governed).

Building an agent gets easier every month. Running **fleets** of them — LLMs, multi-agent
orchestrators, MCP tools, A2A networks, shared memory and second brains, knowledge graphs and
databases — and keeping them **protected, access-controlled, identified, monitored, tracked, and
governed** at enterprise scale is the hard, unsolved part. As models move toward superintelligence,
that control problem is *the* problem. Every entry below has a one-line note on why it's
here — a curated map, not a dump.

**Maintained by [Lijith V M](https://github.com/Lijithvmv)** — I build enterprise AI systems and the
governance around them. Contributions welcome ([CONTRIBUTING](CONTRIBUTING.md)).

---

## Contents
**Part I — Build: the agentic stack**
[LLMs & serving](#llms--serving) ·
[Agent frameworks & harnesses](#agent-frameworks--harnesses) ·
[Multi-agent orchestration](#multi-agent-orchestration) ·
[Protocols: MCP, A2A & AG-UI](#protocols-mcp-a2a--ag-ui) ·
[RAG, GraphRAG & retrieval](#rag-graphrag--retrieval) ·
[Knowledge graphs & ontologies](#knowledge-graphs--ontologies) ·
[Memory, second brain & enterprise memory](#memory-second-brain--enterprise-memory) ·
[Databases & vector stores](#databases--vector-stores) ·
[Coding agents, code & infra](#coding-agents-code--infra)

**Part II — Control: the trust plane**
[Standards & frameworks](#standards--frameworks) ·
[Threats & attacks](#threats--attacks) ·
[Guardrails & protection](#guardrails--protection) ·
[Access control: RBAC & ABAC](#access-control-rbac--abac) ·
[Identity: human & non-human](#identity-human--non-human) ·
[AI gateways & policy enforcement](#ai-gateways--policy-enforcement) ·
[Evaluation, judges & verification](#evaluation-judges--verification) ·
[Observability, monitoring & tracing](#observability-monitoring--tracing) ·
[Audit, provenance & supply chain](#audit-provenance--supply-chain) ·
[Data protection & privacy](#data-protection--privacy) ·
[Reading & talks](#reading--talks)

---

# Part I — Build: the agentic stack

## LLMs & serving
- [vLLM](https://github.com/vllm-project/vllm) — high-throughput LLM serving; the default for self-hosting.
- [Ollama](https://github.com/ollama/ollama) — run open models locally; the on-ramp for local/offline agents.
- [LiteLLM](https://github.com/BerriAI/litellm) — one API across 100+ model providers (also a gateway/proxy — see control plane).

## Agent frameworks & harnesses
- [LangGraph](https://github.com/langchain-ai/langgraph) — graph-based agent orchestration with state, checkpoints, and human-in-the-loop.
- [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) — a lightweight, code-first agent runtime (handoffs, guardrails, sessions).
- [CrewAI](https://github.com/crewAIInc/crewAI) — role-based multi-agent crews.
- [Microsoft AutoGen](https://github.com/microsoft/autogen) — conversation-driven multi-agent orchestration.
- [Google ADK](https://github.com/google/adk-python) — Agent Development Kit: code-first agents with eval and deploy.
- [LlamaIndex](https://github.com/run-llama/llama_index) — data framework + agent workflows over your data.
- [Newton](https://github.com/Lijithvmv/newton) — a fully-local coding/project agent; a study in *harness* engineering for small models.
- [open-dots](https://github.com/Anil-matcha/open-dots) — a self-hosted agent **workspace** (open alternative to OpenAI Dots / Meta Muse / Grok): Next.js + FastAPI, local-first storage, and a **deny-by-default action gateway with approval workflows** — a rare example of the control thesis baked into an end-user app. *(MIT · 4.8k★.)*

## Multi-agent orchestration
- [Model orchestration patterns](https://www.anthropic.com/engineering/building-effective-agents) — Anthropic's "building effective agents": when to use workflows vs agents (essential reading before you orchestrate).
- [OpenAI Swarm / Agents handoffs](https://github.com/openai/swarm) — minimal patterns for routing and specialist handoffs.
- *(Orchestrator = the layer that decides what runs next: branches, retries, handoffs, shared state. Keep it explicit and inspectable.)*

## Protocols: MCP, A2A & AG-UI
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) — the standard for connecting agents to tools/data; read its **authorization** model before exposing tools.
- [A2A (Agent2Agent) protocol](https://a2aproject.github.io/A2A/) — inter-agent communication; the backbone (and trust boundary) of multi-agent networks.
- [AG-UI protocol](https://github.com/ag-ui-protocol/ag-ui) — the **agent↔UI** layer: event-based streaming (31 event types, transport-agnostic) so any surface renders an agent's tokens, tool calls, reasoning, and shared state in real time. **1.0 (Sept 2026)**; native in LangChain, Claude Agent SDK, CrewAI, Pydantic AI. Completes the trio — **MCP** (agent↔tools) · **A2A** (agent↔agent) · **AG-UI** (agent↔user).

- [Microsoft GraphRAG](https://github.com/microsoft/graphrag) — community-hierarchy GraphRAG (global + local search); powerful for corpus-wide synthesis but token-heavy (~77× naive RAG).
- [LightRAG](https://github.com/HKUDS/LightRAG) — flat entity-relation GraphRAG; cheaper to index and *update* than community hierarchies.
- [HippoRAG](https://github.com/OSU-NLP-Group/HippoRAG) — memory-inspired: OpenIE triples + Personalized PageRank for efficient **multi-hop** retrieval in one graph op.
- [RAPTOR](https://github.com/parthsarthi03/raptor) — recursive embedding-cluster summaries into a hierarchical tree (abstraction levels, no explicit entities).
- [Haystack](https://github.com/deepset-ai/haystack) — production RAG/search pipelines.
- [RAGAS](https://github.com/explodinggradients/ragas) — evaluation for RAG (also in [eval](#evaluation-judges--verification)).
- **[GraphRAG vs Vector RAG — comparison](https://aipractitioner.substack.com/p/graphrag-vs-vector-rag-better-retrieval)** — the decision rubric: real gaps are often <8%; **graphs augment, don't replace, vectors**. Start vector for simple facts; add a graph for multi-hop and corpus synthesis.
- *Note:* similarity is not meaning — pair retrieval with an ontology/authority layer for correctness (see [knowledge graphs](#knowledge-graphs--ontologies)).

## Knowledge graphs & ontologies
- [Neo4j](https://neo4j.com/) — the mainstream property-graph database; the backbone for control/evidence graphs.
- [Graphiti](https://github.com/getzep/graphiti) — build real-time, temporally-aware knowledge graphs for agents.
- [Automating KG population with an LLM](https://machinelearningmastery.com/automating-knowledge-graph-population-extracting-entities-and-triples-from-unstructured-text-with-an-llm/) — the practical *populate-the-graph* how-to: extract entities + triples as **SPOC quads** (subject-predicate-object-**context/provenance**) from unstructured text with a local LLM (JSON mode, temp 0, normalize, human-verify).
- **Ontology / semantic layer** — the business-meaning layer that says what your terms mean and which source is authoritative; what RAG alone can't give you.

## Memory, second brain & enterprise memory
- [Mem0](https://github.com/mem0ai/mem0) — a memory layer for agents (extraction, storage, retrieval of long-term facts).
- [Letta (formerly MemGPT)](https://github.com/letta-ai/letta) — agents with self-editing long-term memory.
- [Zep](https://github.com/getzep/zep) — a memory server for agents with temporal knowledge graphs.
- [cognee](https://github.com/topoteretes/cognee) — memory as a knowledge graph + vector store ("second brain" for agents).
- **Enterprise memory** — shared, governed, auditable memory across teams and agents; treat it as a *protected asset* (poisoning + access control matter).

## Databases & vector stores
- [pgvector](https://github.com/pgvector/pgvector) — vectors in PostgreSQL; keep vectors next to your governed relational data.
- [Qdrant](https://github.com/qdrant/qdrant) · [Milvus](https://github.com/milvus-io/milvus) · [Weaviate](https://github.com/weaviate/weaviate) · [Chroma](https://github.com/chroma-core/chroma) — dedicated vector databases at different scales.

## Coding agents, code & infra
- [Aider](https://github.com/Aider-AI/aider) — AI pair programming in the terminal.
- [OpenHands](https://github.com/All-Hands-AI/OpenHands) — an autonomous software-engineering agent platform.
- *(Coding agents have real blast radius on a dev machine and in CI — see [guardrails](#guardrails--protection) and [access control](#access-control-rbac--abac).)*

---

# Part II — Control: the trust plane

## Standards & frameworks
- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/) — the canonical risk taxonomy. Start here.
- [OWASP AISVS](https://github.com/OWASP/AISVS) — turns the risk list into testable, verifiable requirements across assurance levels.
- [OWASP GenAI / Agentic Security Initiative](https://genai.owasp.org/initiatives/) — agentic threats, mitigations, multi-agent threat modeling.
- [MITRE ATLAS](https://atlas.mitre.org/) — adversary tactics & techniques for ML systems (the ATT&CK of AI).
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) — + its Generative AI Profile (NIST AI 600-1).
- [ISO/IEC 42001](https://www.iso.org/standard/81230.html) — the AI management-system standard ("ISO 27001 for AI").

## Threats & attacks
- **Direct vs indirect prompt injection** — indirect (instructions hidden in retrieved content/tool output) is the core agent threat; it scales with every tool you connect.
- **Jailbreaking, prompt/system-prompt extraction, many-shot, GCG suffixes, Crescendo** — the modern technique set (see [Papers/reading](#reading--talks)); note a system prompt is *not* a secret.
- **Tool poisoning / MCP trust abuse · exfiltration via tool calls · memory & RAG poisoning · confused-deputy** — the agentic action-abuse surface.

## Guardrails & protection
- [GuardLayer](https://github.com/Lijithvmv/Guard-Layer) — layered input/output/tool-call security: prompt-injection defense, egress policy, session taint, tamper-evident audit log. Zero-dependency core.
- [NVIDIA OpenShell](https://github.com/NVIDIA/OpenShell) — the safe **runtime** for agent fleets: **kernel-enforced** per-agent sandbox, every network egress passes a policy check, **credentials never reach the agent**, and **formally-verified policy changes** (a prover flags risky new access for human review). Containment at the kernel. *(Rust · Apache-2.0 · 12k★.)*
- [shield-kya](https://github.com/The-Pixel-Boys/shield-kya) — a local **MCP "Know Your Agent" gate**: **Allow / Review / Deny** on every tool call, **receipts** on a live dashboard, and certification against an *Agent Trust Baseline*; PreToolUse hooks across many agent hosts.
- [NVIDIA NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) — programmable guardrails (Colang) for LLM apps.
- [Guardrails AI](https://github.com/guardrails-ai/guardrails) — validators and structured-output enforcement.
- [LLM Guard](https://github.com/protectai/llm-guard) — input/output scanners (injection, PII, toxicity).
- [Rebuff](https://github.com/protectai/rebuff) — multi-layered prompt-injection detection.
- [Lakera Gandalf](https://gandalf.lakera.ai/) — the classic gamified injection challenge; builds intuition fast.

## Access control: RBAC & ABAC
- [Open Policy Agent (OPA)](https://github.com/open-policy-agent/opa) — policy-as-code (Rego); the standard for fine-grained authorization.
- [Cedar](https://github.com/cedar-policy/cedar) — AWS's authorization policy language (RBAC + ABAC).
- [OpenFGA](https://github.com/openfga/openfga) — relationship-based access control (Google Zanzibar-style) for fine-grained permissions.
- *(For agents: authorize the **action**, not just the service — allow / ask-for-approval / deny per call.)*

## Identity: human & non-human
- [SPIFFE / SPIRE](https://github.com/spiffe/spire) — workload identity: short-lived, verifiable identities for services and agents.
- **Non-human identity (NHI) for agents** — scope agents with least-privilege machine identities; distinguish **U2M** (agent acts for a user, permissions carry through) from **M2M** (agent acts as itself).
- **Token vending / short-lived credentials** — never give an agent a standing, long-lived key.
- [NIST NCCoE — Agentic AI Identity & Authorization](https://pages.nist.gov/nccoe-ai-identity/summary-of-comments.html) — the authoritative reference (600+ public comments): **trust anchors (persistent) vs ephemeral credentials (task-scoped)**, **task-scoped zero-trust authz** (decide at execution, not login), cryptographic **intent "flight plans"**, **deterministic — not LLM — authorization**, and delegation that stays cryptographically traceable to the human/org principal.
- **The identity standards stack** — WIMSE · SPIFFE/SPIRE (workload id) · OAuth2 token-exchange / RAR (delegation + intent) · Cedar / OPA / NGAC (authz) · W3C VC/DID (cross-domain trust) · DPoP / mTLS (sender constraint) · OpenID AuthZEN (authz decisions) · SCITT (provenance).

## AI gateways & policy enforcement
- [Portkey AI Gateway](https://github.com/Portkey-AI/gateway) — an open-source gateway: routing, guardrails, budgets, observability across providers.
- [LiteLLM Proxy](https://github.com/BerriAI/litellm) — a self-hostable gateway with keys, budgets, and rate limits per team/agent.
- **The control-plane pattern** — one governed endpoint where every request is authenticated, authorized (identity → policy), budgeted, guardrailed, and logged. *Who* (identity) × *what* (policy) × *how much* (budget), enforced in one place.

## Evaluation, judges & verification
- [Microsoft PyRIT](https://github.com/Azure/PyRIT) — red-teaming toolkit for generative AI.
- [garak](https://github.com/NVIDIA/garak) — LLM vulnerability scanner ("nmap for LLMs").
- [promptfoo](https://github.com/promptfoo/promptfoo) — eval + red-team harness for prompts, models, and RAG.
- [DeepEval](https://github.com/confident-ai/deepeval) — unit-test-style LLM evaluation.
- [RAGAS](https://github.com/explodinggradients/ragas) — RAG-specific evaluation metrics.
- [Giskard](https://github.com/Giskard-AI/giskard) — testing & scanning for ML/LLM systems.
- **LLM-as-judge / verifier ("jev")** — a separate model or deterministic check that grades output; the loop should complete on *external evidence*, not the model's say-so.

## Observability, monitoring & tracing
- [Langfuse](https://github.com/langfuse/langfuse) — open-source LLM observability, tracing, and evals.
- [Arize Phoenix](https://github.com/Arize-ai/phoenix) — tracing and evaluation for LLM/agent apps.
- [OpenLLMetry](https://github.com/traceloop/openllmetry) — OpenTelemetry-based instrumentation for LLM apps.
- [FastAPI + OpenTelemetry](https://fastapi.tiangolo.com/advanced/opentelemetry/) — built-in OTel traces/metrics/logs for FastAPI services (set the OTLP endpoint; it instruments requests, dependencies, and exceptions) — the wiring for API/agent observability.
- **OpenTelemetry GenAI semantic conventions** — log enough to *reconstruct a decision*: tool calls, arguments, model version, decision path.

## Audit, provenance & supply chain
- [Sigstore model-transparency](https://github.com/sigstore/model-transparency) — sign and verify ML models (provenance/integrity).
- [safetensors](https://github.com/huggingface/safetensors) — safe model serialization (pickle executes code on load — avoid it).
- **AI-BOM** — inventory every model, dataset, tool, and MCP server with its provenance. Tamper-evident audit trails for non-deterministic systems.

## Data protection & privacy
- [Microsoft Presidio](https://github.com/microsoft/presidio) — PII detection and de-identification for text and images.
- **DLP for GenAI** — stop sensitive data from reaching the model or leaving in a response; classify at ingestion; keep secrets out of the context window.

## Reading & talks
- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — the reference on agent/workflow design.
- [Simon Willison — prompt injection series](https://simonwillison.net/tags/prompt-injection/) — the clearest running commentary (jailbreak ≠ injection; the dual-LLM pattern).
- [Embrace The Red (Johann Rehberger)](https://embracethered.com/blog/) — offense-first write-ups of real agent/LLM exploits.
- [Greshake et al. — indirect prompt injection](https://arxiv.org/abs/2302.12173) · [Zou et al. — GCG](https://arxiv.org/abs/2307.15043) — foundational attack papers.
- [GitHub — the Agentic Engineering System](https://github.com/resources/insights/agentic-engineering-system) — an operating model for org-wide agent adoption: Governance + Shared Knowledge + Customer Value; Define → Deliver → Detect; Director / Performer / Assessor.
- [Anthropic — GLM-5.3 & the spread of advanced cyber capabilities](https://www.anthropic.com/research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities) — open-weight models can be cheaply stripped of safeguards (refusal 95% → 6% via abliteration, ~$1,200); the case for putting safety in the **runtime**, not only the model.

---

*A maintained seed — curated from practitioner research and grown weekly. This is a map of a fast-
moving field; open a PR to add what matters and fix what's stale.*
