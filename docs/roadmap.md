# Professional Evolution Plan: Senior Backend → Systems Architect with AI

## 1. Context and motivation

### 1.1. Current situation

- **Current role:** Senior Backend Engineer in critical high-availability systems.
- **Main stack:** Go (Golang), Elixir, microservices, Docker, Cloud.
- **Current AI level:** Absolute beginner.
- **Constraints:**
  - Time: 5–7h / week (weekday evenings + 1 weekend block).
  - Budget: €20–50/month for APIs and tools.

### 1.2. Main motivation

- Avoid becoming a “code monkey” easily replaceable by AI.
- Evolve towards **Staff Engineer / Systems Architect with AI** roles, focusing on:
  - Agent orchestration.
  - Reliability and observability.
  - Internal AI platforms (AI Platform Engineering).
- Become **highly employable** in 1–3 years in sectors such as Fintech, DevTools, SRE/Platforms, etc.

## 2. Vision and objectives

### 2.1. Vision for 1–3 years

Become a profile that:
- Designs and leads the architecture of AI systems in production (not just the models).
- Is a reference in **AI platforms**, **LLM gateways** and **observability/Evals**.
- Can defend complex architectures to CTOs / Directors of Engineering.

### 2.2. Objectives for 6 months (this plan)

1. **Practical knowledge of AI applied to systems:**
   - Understand and know how to use embeddings, RAG and orchestrated agents.
   - Master the use of tools such as LangGraph (Python) at a practical level.

2. **Main project (Portfolio “Staff Thesis”):**
   - Build an **Incident Intelligence / SRE Copilot Platform** with:
     - AI Gateway in Go.
     - Agent orchestrator with LangGraph (Python).
     - Multi-source RAG (logs, metrics, runbooks, code).
     - Automatic evals.
     - Cost and performance metrics.

3. **Foundation for secondary project:**
   - Leave the infrastructure ready so that, in a second phase, you can build:
     - An **AI Cost Controller** (AI FinOps) **or**
     - A more general **AI Internal Developer Platform**.

4. **Professional narrative:**
   - Publish at least 2 technical articles explaining architectures, decisions and results.
   - Have a README and project documentation with Staff Engineer proposal quality.

5. **Re-evaluation framework:**
   - Leave clear criteria so that in 3–6 months you can review:
     - Technical progress.
     - Relevance of the roadmap.
     - Adjustments according to market evolution and your interests.

## 3. Technological strategy

### 3.1. Go + Python duality

- **Python:**
  - “Brain” of the AI system.
  - Use LangChain / LangGraph for agents, RAG and orchestration.
  - Rapid prototypes, integration with AI ecosystem.

- **Go:**
  - Production “infrastructure”.
  - AI Gateway / LLM Proxy: routing, cache, rate limiting, security, metrics.
  - High-performance, low-latency services.

### 3.2. Elixir (later phase)

- **Not a priority in the first 6 months.**
- Ideal use (phase 2 of roadmap): real-time observability and dashboards with Phoenix LiveView for:
  - Viewing agent behaviour live.
  - Monitoring flows and metrics reactively.

## 4. Target skills (competency map)

### 4.1. Core applied AI

1. **Embeddings and RAG**
   - What embeddings are and how they are used for semantic search.
   - Vector DB (Qdrant, Chroma or another).
   - Basic RAG and then advanced RAG (multi-source, re-ranking, agentic RAG).

2. **Agents and orchestration (LangGraph)**
   - Difference between “simple tool calling” and agents with memory and flow.
   - Diagram and build agent graphs with states and transitions.
   - Error handling, timeouts, retries, logging at agent level.

3. **AI Evals and observability**
   - Design test datasets (initially synthetic, then curated).
   - Quality metrics: diagnostic accuracy, completeness, relevance, etc.
   - Integration with observability tools (e.g. Langfuse) for traces and spans.
   - Run evals in CI/CD.

4. **AI Platform Engineering**
   - LLM gateways / multi-provider proxies.
   - Cost control (tokens, estimated cost, budgets).
   - Quotas, rate limiting, multi-tenant.
   - Basic guardrails (output structures, validation).

5. **MCP (Model Context Protocol)**
   - Understand the standard.
   - Implement a simple MCP server that exposes:
     - Incident diagnostic tools.
     - Access to logs, metrics and runbooks.

6. **“Serious” prompt engineering**
   - Design stable, versioned system prompts.
   - Separate prompts into reusable templates.
   - Measure the impact of prompt changes via evals (not by intuition).

***

## 5. Main project: Incident Intelligence Platform (SRE Copilot)

### 5.1. General idea

Build a **platform** (not just a chatbot) that:

- **Ingests and unifies information** from:
  - Logs (e.g. Elastic / Loki / simple files).
  - Metrics (e.g. Prometheus).
  - Runbooks and documentation (Markdown).
  - Relevant code snippets (affected services).

- **When an alert / incident occurs:**
  - Retrieves relevant context (RAG).
  - Orchestrates several specialised agents (log analysis, metrics, code, runbooks).
  - Proposes one or more root cause hypotheses.
  - Suggests mitigation steps and references to documentation.
  - Optionally, generates a “postmortem draft”.

### 5.2. Architectural components

1. **AI Gateway in Go**
   - OpenAI-compatible style API (to use it easily from Python).
   - Features:
     - Routing between providers (OpenAI, Anthropic, etc.).
     - Rate limiting per API key / tenant.
     - Semantic cache for frequent requests.
     - Metrics (Prometheus / OpenTelemetry).
     - Structured logging.

2. **Agent orchestrator (Python + LangGraph)**
   - Specialised agents:
     - Log Analyzer Agent.
     - Metrics Correlator Agent.
     - Code Context Agent.
     - Runbook Suggestion Agent.
   - State graph:
     - Start → Preliminary diagnosis → Additional analysis (if needed) → Synthesis and report.
   - Use the Gateway as backend for all LLM calls.

3. **Multi-source RAG**
   - Index:
     - Summarised/curated logs (not raw).
     - Metrics with context (historical alerts).
     - Runbooks and documentation.
     - Relevant code snippets.
   - RAG:
     - Simple pipeline at first (single index).
     - Then “agentic” RAG: the system decides which source to query for each sub-task.

4. **Evals and observability**
   - Dataset:
     - Collection of “simulated incidents” with:
       - Failure type.
       - Associated logs/metrics.
       - Expected root cause.
       - Good example of analysis.
   - Evals:
     - Compare system output with “expected solution”.
     - Quantitative metrics (percentage correct, step coverage, etc.).
   - Observability:
     - Integration with tool such as Langfuse or similar.
     - Full traces for each incident.

5. **MCP Server**
   - Expose the system as a set of MCP tools:
     - `diagnose_incident(...)`
     - `suggest_runbooks(...)`
     - `get_incident_report(...)`
   - Allow compatible models (Claude, ChatGPT, etc.) to invoke these standardised tools.

***

## 6. Detailed timeline (6 months)

Assuming ~6h average / week (≈24h/month).

### Month 1: Practical fundamentals + basic RAG

**Objectives:**
- Understand embeddings and RAG well.
- Set up a first simple RAG prototype.

**Activities:**
- Follow 1–2 introductory courses/chapters (embeddings, LLMs, RAG, LangChain).
- In Python:
  - Build a basic RAG over a small corpus (e.g. documentation of a service, sample logs).
  - Use a vector DB (Qdrant/Chroma).
- Learn to:
  - Call an LLM via API.
  - Separate prompts into system / user / tool.

**Deliverables:**
- Simple RAG mini-project on GitHub.
- Personal notes with:
  - What you understand about RAG.
  - Open questions.

***

### Month 2: AI Gateway in Go (MVP)

**Objectives:**
- Build the first version of the Gateway that wraps an LLM provider.

**Activities:**
- Design the API:
  - Take inspiration from the OpenAI API (endpoints `/v1/chat/completions`, etc.).
- Implement in Go:
  - Minimal logic for:
    - Receiving requests.
    - Calling the provider (OpenAI or another).
    - Returning response.
  - Structured logging and basic metrics.
- Add:
  - Configuration via environment variables.
  - Basic error / timeout handling.

**Deliverables:**
- Repository `ai-gateway-go` (or similar name) on GitHub.
- README with:
  - Simple architecture diagram.
  - Example of use from `curl` and from a small Python script.

***

### Month 3: Advanced Gateway + first agents

**Objectives:**
- Improve the Gateway.
- Start with agent orchestration.

**Activities (Gateway):**
- Add:
  - Rate limiting per API key.
  - Support for at least 2 providers (e.g. OpenAI + Anthropic or OpenAI + local model via Ollama).
  - Basic Prometheus metrics (latency, errors, tokens, etc.).
  - Simple cache (by hash of prompt+params).

**Activities (Agents):**
- In Python + LangGraph:
  - Create a simple agent that:
    - Receives a question.
    - Calls the Gateway (not the provider directly).
    - Returns a response.
  - Start modelling a single-agent graph (still without complex multi-agent).

**Deliverables:**
- Gateway with basic advanced features.
- First functional agent that consumes the Gateway.

***

### Month 4: Multi-source RAG + Multi-agent orchestration

**Objectives:**
- Connect your RAG with the agent.
- Define the multi-agent structure for the SRE Copilot.

**Activities:**
- Extend the RAG:
  - Ingest:
    - Sample logs.
    - Metrics (even in simplified format).
    - Runbooks in Markdown.
  - Design metadata schema (source type, service, severity, etc.).

- In LangGraph:
  - Define several agents:
    - Log Analyzer.
    - Metrics Analyzer.
    - Runbook Recommender.
  - Build the work graph:
    - Initial node → decides which agents to activate according to incident type.
    - Gather results and synthesise.

**Deliverables:**
- SRE Copilot capable of:
  - Given a “simulated alert” + some data, producing a reasonable analysis.
- Internal documentation (even in Markdown) describing the agent graph.

***

### Month 5: Evals + Observability + MCP

**Objectives:**
- Start treating the platform as a serious system: measure and observe.
- Make it accessible via MCP.

**Activities (Evals):**
- Create a small dataset of simulated incidents with:
  - Description.
  - Input data (logs/metrics).
  - Expected root cause.
  - Example of “ideal” report.
- Implement:
  - Script that runs the SRE Copilot on each incident.
  - Metrics: does it get the root cause right or not? Does it mention key elements?
  - A small automatic report (accuracy percentage, good and bad examples).

**Activities (Observability):**
- Integrate a tracing/observability tool:
  - Capture:
    - Inputs/outputs of each LLM call (through the Gateway).
    - Steps of the agent graph.
  - View at least:
    - Traces per incident.
    - Latencies.

**Activities (MCP):**
- Implement an MCP server that exposes:
  - `diagnose_incident(...)`.
  - `generate_incident_report(...)`.
- Test it with some MCP-compatible client tool (when possible).

**Deliverables:**
- Repeatable eval suite (runnable from command line).
- First results report.
- Minimal operational MCP server.

***

### Month 6: Polish, deployment and narrative

**Objectives:**
- Polish the project so it looks like a “Staff thesis”.
- Tell the story externally.

**Activities (Deployment):**
- Dockerise:
  - Gateway.
  - Agent orchestrator.
  - Vector DB (if necessary).
- Deploy on:
  - Fly.io, Render, Railway, or another cheap platform.
- Add configuration for demo environment (with synthetic data).

**Activities (Technical polish):**
- Review:
  - Logs.
  - Error handling.
  - Basic security (do not expose keys in responses).
- Refine prompts based on eval results.

**Activities (Narrative):**
- Write **2 technical articles** (preferably in English):
  1. “Building an LLM Gateway in Go for Production-Ready AI Systems”.
  2. “From Incidents to Insights: Designing an AI-Driven SRE Copilot with Evals and MCP”.
- Improve the README:
  - Architecture diagram.
  - Explanation of key decisions (ADRs).
  - Eval results (charts, even if simple).
  - Limitations and possible future extensions.

**Deliverables:**
- Deployed platform (even with fake data).
- README + published technical articles.
- List of “future work” (e.g. Elixir LiveView dashboard, AI Cost Controller, etc.).

***

## 7. Intermediate success metrics

To be able to re-evaluate the plan with another AI agent in a few months, define clear indicators now:

1. **Technical progress**
   - Have I built at least 1 functional version of the Gateway?
   - Do I have an RAG that actually uses multiple sources?
   - Do I have a defined and working agent graph?
   - Do I have an eval suite that I can run and whose metrics I understand?

2. **Project quality**
   - Does the system solve synthetic test cases with acceptable quality?
   - Do I understand where it fails and why?
   - Can I explain the architecture trade-offs?

3. **Professional visibility**
   - Do I have at least 1–2 articles published?
   - Does my README look like a serious production project?
   - Have I shared the project with someone and received feedback?

4. **Time management and motivation**
   - Have I maintained the average pace of 5–7h/week?
   - Am I still motivated by the topic or do I need to adjust the scope?

***

## 8. Guide for future re-evaluation with AI

When in 3–6 months you want to review this plan with another AI agent (or with the same model in another version), you can use this document as a basis and ask it things like:

1. **About the market:**
   - “With this project and these skills, what specific types of roles would you recommend I look for now?”
   - “Has anything relevant changed in the ecosystem (MCP, gateways, agent frameworks) that I should incorporate?”

2. **About the project:**
   - “Here is the repository: what architectural weaknesses do you see?”
   - “What refactors or extensions would you prioritise to take it one level closer to a real product?”

3. **About the future roadmap:**
   - “Is it a good time to add an Elixir LiveView dashboard?”
   - “What would have more impact as a next project: an AI Cost Controller or an AI Internal Developer Platform?”

4. **About positioning:**
   - “With this portfolio, how would you write my ‘pitch’ as Staff/Architect in AI for Fintech / DevTools / SRE?”