# Case Studies

> **Note:** All case studies are anonymized to protect client confidentiality. Technical details are real; client names and specific business contexts are abstracted.

---

## Case Study 1: Enterprise RAG System for Financial Services

### Problem
Large banking client needed an internal knowledge assistant to help employees find information across 10,000+ policy documents, compliance guidelines, and internal wikis. Manual search was taking 20-30 minutes per query, and existing keyword search returned too many irrelevant results.

### Business Context
- **Users:** 2,000+ internal employees (compliance, legal, operations)
- **Content:** 10,000+ documents (PDF, Word, SharePoint)
- **Requirements:** GDPR compliance, audit logs, <5s query latency, 95%+ accuracy

### Technical Constraints
- Must run on Azure (client's cloud)
- No data can leave EU region
- Integration with existing Azure AD for auth
- Budget: €50k for infra (6 months)

### Approach
1. **Discovery (2 weeks):** Analyzed document types, user queries, existing systems
2. **Architecture Design (1 week):** Hybrid search (keyword + semantic), Azure OpenAI for LLM, Azure AI Search for vector store, MLflow for prompt tracking
3. **Implementation (8 weeks):** Built ingestion pipeline, deployed RAG backend, created evaluation framework
4. **Testing & Rollout (4 weeks):** User acceptance testing, gradual rollout from 50 → 2,000 users

### Architecture Decisions
- **Vector Database:** Azure AI Search (native Azure integration, GDPR compliance, hybrid search built-in)
- **LLM:** Azure OpenAI GPT-4 with prompt caching (cost vs. accuracy trade-off)
- **Chunking Strategy:** Recursive character splitter with 1000 token chunks, 200 overlap (balanced context vs. precision)
- **Reranking:** Cross-encoder model to refine top-10 results from hybrid search
- **Evaluation:** LLM-as-judge for correctness + human labeling for 500 test queries

### Key Technologies
**Backend:** FastAPI, LangChain, Azure OpenAI, Azure AI Search, Redis (caching)  
**Infrastructure:** AKS (3-node cluster), Terraform, Helm, Azure Application Insights  
**CI/CD:** Azure DevOps, Docker, automated testing with pytest  
**Monitoring:** Application Insights for traces, Prometheus + Grafana for metrics

### Delivery Timeline
- Week 1-2: Discovery & requirements
- Week 3: Architecture design & approval
- Week 4-11: Development (ingestion, RAG backend, evaluation)
- Week 12-15: Testing & rollout
- **Total:** 15 weeks from kickoff to production

### Risk Mitigation
- **Hallucinations:** Implemented citation system (every answer includes source docs) + human-in-the-loop for critical queries
- **Cost Overruns:** Set up prompt caching, token usage monitoring, alerts at 80% budget
- **Data Privacy:** All data encrypted at rest/transit, Azure Private Link, audit logs for all queries

### Measurable Outcomes
- **Query time:** 25 min → 8 seconds (average)
- **User satisfaction:** 87% positive feedback in pilot (50 users)
- **Cost:** €3.20 per 1000 queries (within budget)
- **Accuracy:** 91% correct answers on test set (500 queries)
- **Adoption:** 1,200 active users after 3 months

### Lessons Learned
1. **Chunking matters more than embeddings** – Spent 2 weeks optimizing chunking strategy; improved accuracy by 12%
2. **Evaluation is hard** – LLM-as-judge disagreed with humans 18% of the time; hybrid eval is necessary
3. **Caching saves money** – Prompt caching reduced costs by 40% for repeated queries
4. **Users need citations** – Without source docs, users didn't trust answers (learned in week 1 of pilot)

### Next Steps (if I had more time)
- Multi-modal RAG (process images, tables in PDFs)
- Fine-tuned reranker on domain data
- Agentic layer for multi-hop reasoning (e.g., "Compare policy X and Y")

---

## Case Study 2: Multi-Agent Orchestration Platform

### Problem
Client had multiple AI use cases (document processing, data extraction, chatbot) but no unified way to deploy agents. Each team built custom solutions, leading to duplicated effort and inconsistent quality.

### Business Context
- **Teams:** 5 product teams needing AI capabilities
- **Use cases:** Invoice processing, contract analysis, customer support chatbot, data enrichment
- **Requirements:** Self-service agent deployment, centralized monitoring, cost attribution per team

### Technical Constraints
- Multi-tenant platform (isolated workspaces per team)
- Budget: €10k/month for compute
- Must support custom Python code + LLM calls
- Observability required for debugging agent decisions

### Approach
1. **Platform Design (3 weeks):** YAML-based agent definitions, LangGraph for orchestration, centralized state management
2. **Core Implementation (6 weeks):** Agent registry, execution engine, monitoring dashboard
3. **Self-Service Tooling (2 weeks):** CLI for agent deployment, web UI for monitoring
4. **Onboarding (2 weeks):** Documentation, templates, training sessions

### Architecture Decisions
- **Orchestration:** LangGraph (flexible, observable, Python-native)
- **Deployment:** Kubernetes CronJobs + on-demand triggers via API
- **State Management:** Redis for agent memory, PostgreSQL for audit logs
- **Observability:** LangSmith for agent traces, custom dashboard for cost/usage

### Key Technologies
**Orchestration:** LangGraph, LangChain, Azure OpenAI  
**Backend:** FastAPI, Celery (async tasks), Redis, PostgreSQL  
**Infrastructure:** AKS, Terraform, Helm, Prometheus  
**Frontend:** React dashboard (monitoring only)

### Delivery Timeline
- Week 1-3: Platform architecture & proof-of-concept
- Week 4-9: Core platform development
- Week 10-11: Self-service tooling (CLI, docs)
- Week 12-13: Pilot with 2 teams
- **Total:** 13 weeks

### Risk Mitigation
- **Agent Failures:** Circuit breakers, retry logic, fallback to human
- **Cost Control:** Per-team budgets, auto-pause at threshold, cost alerts
- **Security:** Agent code sandboxing, API rate limits, audit logs

### Measurable Outcomes
- **Time-to-deploy:** 2 weeks → 2 days for new agent use cases
- **Cost visibility:** 100% attribution to teams (previously unknown)
- **Reuse:** 3 agents deployed by 2+ teams (saved ~200 hours of dev time)
- **Reliability:** 99.2% uptime over 3 months

### Lessons Learned
1. **YAML is underrated** – Non-engineers could define simple agents after 1-hour training
2. **Observability is critical** – 60% of support requests were "why did agent do X?"—traces solved this
3. **Self-service requires great docs** – Invested 40 hours in docs; reduced support load by 70%

### Next Steps
- Add A/B testing framework for agent prompts
- Implement agent evaluation suite
- Support other orchestration frameworks (CrewAI, Autogen)

---

## Case Study 3: GPU-Accelerated Deepfake Detection System

### Problem
Cybersecurity client needed real-time deepfake detection for video calls (protect against social engineering attacks). Existing CPU-based model took 45 seconds per frame; needed <1 second.

### Business Context
- **Use case:** Real-time video analysis during enterprise video calls
- **Scale:** 500 concurrent calls, 30 fps
- **Requirements:** <1s latency, 95%+ accuracy, cost-effective

### Technical Constraints
- Must integrate with existing video conferencing platform
- Budget: €15k/month for GPU compute
- Model must be privacy-preserving (no data storage)

### Approach
1. **Model Optimization (2 weeks):** Converted PyTorch model to ONNX, quantized to FP16, optimized with TensorRT
2. **Inference Stack (3 weeks):** Deployed NVIDIA Triton Inference Server on GPU nodes, implemented batching
3. **Integration (2 weeks):** Built video frame extraction service, connected to conferencing API
4. **Load Testing (1 week):** Simulated 500 concurrent calls, tuned batch sizes

### Architecture Decisions
- **Inference Server:** NVIDIA Triton (built for GPUs, dynamic batching, multi-model support)
- **Model Format:** TensorRT (10x faster than native PyTorch)
- **Batching:** Dynamic batching with max 32 frames (balanced latency vs. throughput)
- **GPU:** NVIDIA T4 (cost-effective for inference)

### Key Technologies
**ML Stack:** PyTorch → ONNX → TensorRT, NVIDIA Triton Inference Server  
**Infrastructure:** AKS with GPU node pools, Terraform, Helm  
**Backend:** FastAPI (video frame extraction), gRPC (Triton client)  
**Monitoring:** Prometheus (GPU metrics), Grafana dashboards

### Delivery Timeline
- Week 1-2: Model optimization & benchmarking
- Week 3-5: Triton deployment & integration
- Week 6-7: Load testing & tuning
- Week 8: Production rollout
- **Total:** 8 weeks

### Risk Mitigation
- **GPU Costs:** Auto-scaling GPU nodes (min 1, max 5), cost alerts
- **Model Drift:** Weekly retraining on new deepfake samples
- **Privacy:** Zero data retention, encrypted streams, on-prem deployment option

### Measurable Outcomes
- **Latency:** 45s → 0.8s per frame (10x faster)
- **Throughput:** 500 concurrent calls supported
- **Cost:** €8k/month actual (under budget)
- **Accuracy:** 96% detection rate on test set

### Lessons Learned
1. **TensorRT is magic** – 10x speedup with minimal effort (3 days to convert + optimize)
2. **Batching is key** – Dynamic batching doubled throughput without extra cost
3. **GPU utilization monitoring is critical** – Wasted 30% GPU in first week due to poor batching

### Next Steps
- Multi-modal detection (audio + video)
- Edge deployment for lower latency
- Federated learning for privacy-preserving retraining

---

## How to Use These Case Studies

These examples demonstrate my approach to production AI systems:
1. **Start with the problem**, not the technology
2. **Design for constraints** (cost, compliance, latency)
3. **Measure everything** (accuracy, latency, cost, adoption)
4. **Learn and iterate** (every project teaches something)

If you want to discuss how I'd approach a similar problem for your team, [let's talk](mailto:lrussobertolez@gmail.com).
