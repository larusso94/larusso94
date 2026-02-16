# Architecture Notes

> Architectural patterns and design principles I follow when building production AI systems.

---

## 1. RAG in Production Architecture

```mermaid
graph TD
    A[User Query] --> B[Query Preprocessor]
    B --> C{Routing Layer}
    C -->|Semantic Search| D[Embedding Model]
    C -->|Keyword Search| E[BM25 Index]
    D --> F[Vector Database]
    E --> F
    F --> G[Hybrid Search Results]
    G --> H[Reranker Model]
    H --> I[Top-K Documents]
    I --> J[Context Builder]
    J --> K[LLM with Prompt]
    K --> L[Response Generator]
    L --> M[Citation Formatter]
    M --> N[User Response]
    
    K --> O[Evaluation Pipeline]
    O --> P[Correctness Judge]
    O --> Q[Latency Monitor]
    O --> R[Cost Tracker]
    
    S[Document Ingestion] --> T[Chunking Strategy]
    T --> U[Embedding Generation]
    U --> F
    S --> V[Keyword Indexing]
    V --> E
    
    W[Monitoring] --> F
    W --> K
    W --> O
    W --> X[Observability Dashboard]
    
    style K fill:#3498db,stroke:#2c3e50,stroke-width:2px,color:#fff
    style F fill:#e74c3c,stroke:#c0392b,stroke-width:2px,color:#fff
    style O fill:#2ecc71,stroke:#27ae60,stroke-width:2px,color:#fff
```

### Key Components

**Ingestion Pipeline:**
- **Chunking Strategy:** Recursive character splitter with semantic boundaries (paragraphs, sentences)
- **Embedding Model:** OpenAI `text-embedding-3-small` (cost-effective) or domain-specific fine-tuned model
- **Vector Database:** Azure AI Search, Pinecone, or Weaviate (choice depends on cloud, scale, features)
- **Keyword Index:** BM25 for exact matches (technical terms, IDs, dates)

**Retrieval Layer:**
- **Hybrid Search:** 70% semantic + 30% keyword (tuned per use case)
- **Reranker:** Cross-encoder model (e.g., `ms-marco-MiniLM`) for top-10 → top-3 refinement
- **Query Routing:** Simple queries → keyword, complex queries → semantic, hybrid for everything else

**Generation Layer:**
- **LLM:** Azure OpenAI GPT-4 or GPT-3.5 (cost vs. quality trade-off)
- **Prompt Engineering:** System prompt with role, retrieved context, citations requirement, guardrails
- **Caching:** Prompt caching for repeated queries (40% cost reduction in practice)

**Evaluation Pipeline:**
- **Correctness:** LLM-as-judge + human labeling for critical queries
- **Latency:** p50, p95, p99 tracking with alerts
- **Cost:** Token usage per query, monthly budget tracking
- **Retrieval Quality:** Recall@K, precision@K, NDCG

**Observability:**
- **Traces:** LangSmith or Application Insights for request flow
- **Metrics:** Prometheus for latency, cost, error rates
- **Logs:** Audit logs for compliance, query logs for debugging

### Design Principles
1. **Hybrid beats pure semantic** – Keyword search catches exact matches that embeddings miss
2. **Reranking is worth the latency** – 100ms reranking improves accuracy by 15%+
3. **Citations are non-negotiable** – Users don't trust answers without sources
4. **Evaluation is continuous** – Accuracy degrades over time; monitor and retrain

---

## 2. Agentic Workflow System Architecture

```mermaid
graph TD
    A[User Request] --> B[Agent Orchestrator]
    B --> C{Workflow Type}
    C -->|Sequential| D[Sequential Executor]
    C -->|Parallel| E[Parallel Executor]
    C -->|Hierarchical| F[Hierarchical Coordinator]
    
    D --> G[Agent 1: Task Planner]
    G --> H[Agent 2: Tool Executor]
    H --> I[Agent 3: Result Validator]
    I --> J[Final Output]
    
    E --> K[Agent Pool]
    K --> L[Agent A]
    K --> M[Agent B]
    K --> N[Agent C]
    L --> O[Result Aggregator]
    M --> O
    N --> O
    O --> J
    
    F --> P[Coordinator Agent]
    P --> Q[Sub-Agent 1]
    P --> R[Sub-Agent 2]
    Q --> S[Tool Call]
    R --> S
    S --> P
    P --> J
    
    T[Shared State Manager] --> B
    T --> D
    T --> E
    T --> F
    
    U[Tool Registry] --> S
    U --> H
    U --> V[External APIs]
    U --> W[Database Queries]
    U --> X[LLM Calls]
    
    Y[Observability Layer] --> B
    Y --> T
    Y --> U
    Y --> Z[Agent Trace Dashboard]
    
    AA[Governance Layer] --> B
    AA --> AB[Permission Manager]
    AA --> AC[Resource Limiter]
    AA --> AD[Failure Handler]
    
    style B fill:#3498db,stroke:#2c3e50,stroke-width:2px,color:#fff
    style T fill:#e74c3c,stroke:#c0392b,stroke-width:2px,color:#fff
    style Y fill:#2ecc71,stroke:#27ae60,stroke-width:2px,color:#fff
```

### Key Components

**Orchestration Layer:**
- **Workflow Engine:** LangGraph for state management and control flow
- **Execution Modes:** Sequential (chain of thought), Parallel (independent tasks), Hierarchical (manager-worker)
- **State Management:** Redis for shared memory, PostgreSQL for persistent state

**Agent Pool:**
- **Agent Types:** Task Planner, Tool Executor, Validator, Coordinator
- **Agent Registry:** YAML definitions with capabilities, permissions, resource limits
- **Dynamic Loading:** Agents loaded on-demand from registry

**Tool Layer:**
- **Tool Registry:** Centralized catalog of available tools (APIs, databases, LLMs, custom code)
- **Tool Calling:** Function calling with input validation and output parsing
- **Error Handling:** Retry logic, fallbacks, circuit breakers

**Governance:**
- **Permissions:** Agent-specific access controls (which tools, which data)
- **Resource Limits:** Max tokens per agent, max execution time, max cost
- **Failure Handling:** Graceful degradation, human-in-the-loop escalation

**Observability:**
- **Traces:** LangSmith for agent decision logs, tool calls, state transitions
- **Metrics:** Agent success rate, latency, cost per workflow
- **Dashboards:** Real-time monitoring of active workflows, bottlenecks, failures

### Design Principles
1. **State is king** – Explicit state management prevents agent confusion
2. **Tools over prompts** – Well-defined tools beat "just ask the LLM to do it"
3. **Observe everything** – Agents are black boxes; traces make them debuggable
4. **Fail gracefully** – Agents will fail; plan for retries, fallbacks, human escalation

---

## 3. MLOps Platform Architecture

```mermaid
graph TD
    A[Data Scientist] --> B[Experiment Tracking]
    B --> C[MLflow Server]
    C --> D[Experiment Logs]
    C --> E[Model Artifacts]
    
    A --> F[Model Development]
    F --> G[Jupyter Notebooks]
    F --> H[Local Training]
    H --> C
    
    I[ML Pipeline] --> J[Training Job]
    J --> K[AKS Training Pods]
    K --> L[GPU Node Pool]
    K --> M[CPU Node Pool]
    J --> C
    
    C --> N[Model Registry]
    N --> O{Model Version}
    O -->|Staging| P[Staging Environment]
    O -->|Production| Q[Production Environment]
    
    P --> R[Model Serving - Staging]
    R --> S[Test API]
    
    Q --> T[Model Serving - Prod]
    T --> U[Load Balancer]
    U --> V[Inference Pod 1]
    U --> W[Inference Pod 2]
    U --> X[Inference Pod 3]
    
    Y[CI/CD Pipeline] --> Z[GitHub Actions]
    Z --> AA[Build Docker Image]
    AA --> AB[Run Tests]
    AB --> AC[Deploy to Staging]
    AC --> AD[Automated Validation]
    AD --> AE[Deploy to Prod]
    
    AF[Monitoring Layer] --> AG[Prometheus]
    AG --> AH[Model Drift Detection]
    AG --> AI[Performance Metrics]
    AG --> AJ[Resource Usage]
    AG --> AK[Grafana Dashboard]
    
    AL[Infrastructure] --> AM[Terraform]
    AM --> AN[AKS Cluster]
    AM --> AO[Storage Accounts]
    AM --> AP[Networking]
    AM --> AQ[IAM Roles]
    
    style C fill:#3498db,stroke:#2c3e50,stroke-width:2px,color:#fff
    style N fill:#e74c3c,stroke:#c0392b,stroke-width:2px,color:#fff
    style T fill:#2ecc71,stroke:#27ae60,stroke-width:2px,color:#fff
    style AF fill:#f39c12,stroke:#e67e22,stroke-width:2px,color:#fff
```

### Key Components

**Experiment Tracking:**
- **MLflow Server:** Centralized tracking for experiments, parameters, metrics, artifacts
- **Integration:** Python SDK for logging, UI for browsing experiments
- **Storage:** Azure Blob Storage for artifacts, PostgreSQL for metadata

**Model Registry:**
- **Versioning:** Semantic versioning (v1.0.0, v1.1.0, etc.)
- **Stages:** Development → Staging → Production
- **Metadata:** Model lineage, training data, hyperparameters, performance metrics

**Training Infrastructure:**
- **Kubernetes Jobs:** On-demand training pods with GPU/CPU resource requests
- **GPU Node Pool:** NVIDIA T4/V100 for deep learning training
- **CPU Node Pool:** Standard VMs for preprocessing and feature engineering
- **Auto-scaling:** Scale up during training, scale down when idle

**Model Serving:**
- **Deployment:** Docker containers with model artifacts, FastAPI for REST API
- **Scaling:** Horizontal pod autoscaling based on request rate
- **Load Balancing:** NGINX Ingress with sticky sessions for stateful models
- **Versioning:** Blue-green deployments for zero-downtime updates

**CI/CD Pipeline:**
- **Trigger:** Git push to `main` branch
- **Steps:** Lint → Unit Tests → Build Docker Image → Deploy to Staging → Validation Tests → Deploy to Production
- **Rollback:** Automatic rollback if validation fails
- **Notifications:** Slack alerts for deployments and failures

**Monitoring:**
- **Model Drift:** Statistical tests on input distributions (KS test, PSI)
- **Performance:** Latency (p50, p95, p99), throughput (requests/sec), error rate
- **Resource Usage:** CPU, memory, GPU utilization per pod
- **Alerts:** PagerDuty integration for critical issues

**Infrastructure-as-Code:**
- **Terraform:** Provision AKS cluster, storage accounts, networking, IAM
- **Helm Charts:** Deploy MLflow, Prometheus, Grafana, model serving
- **GitOps:** All infrastructure changes via Git PRs

### Design Principles
1. **Everything is code** – Models, infrastructure, pipelines all version-controlled
2. **Automate validation** – No manual testing; automated tests gate production
3. **Monitor everything** – Drift, performance, cost—all tracked in real-time
4. **Make rollbacks trivial** – Production issues happen; fast rollback saves the day

---

## Common Patterns Across Architectures

### 1. **Observability First**
Every system has traces, metrics, and logs. Debugging production AI is impossible without observability.

### 2. **Infrastructure-as-Code**
All infrastructure provisioned via Terraform/Helm. No manual changes to production.

### 3. **Cost Visibility**
Every component tracks cost (LLM tokens, GPU hours, storage). Monthly budgets with alerts.

### 4. **Graceful Degradation**
Systems degrade gracefully under load or failure. Fallbacks, retries, circuit breakers.

### 5. **Security by Default**
Auth, encryption, audit logs, least-privilege IAM. Security is not an afterthought.

---

## Want to Discuss Architecture?

These diagrams are starting points. Real systems are messier, with trade-offs specific to your use case. If you want to dive deeper into any of these patterns, [let's talk](mailto:lrussobertolez@gmail.com).
