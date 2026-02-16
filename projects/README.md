# Projects Index

> Flagship projects that demonstrate my approach to production AI systems. Some are open-source, others are internal tools or client work (anonymized).

---

## Featured Projects

| Project | Problem Solved | Core Stack | Status | Link |
|---------|---------------|------------|--------|------|
| **[Agent Mesh Platform](#agent-mesh-platform)** | Centralized multi-agent orchestration with YAML configs | LangGraph, FastAPI, Redis, AKS | Internal Tool | [Case Study](../docs/02-case-studies.md#case-study-2-multi-agent-orchestration-platform) |
| **[Enterprise RAG System](#enterprise-rag-system)** | Internal knowledge assistant for 10k+ documents | Azure OpenAI, Azure AI Search, LangChain | Client Project | [Case Study](../docs/02-case-studies.md#case-study-1-enterprise-rag-system-for-financial-services) |
| **[GPU Deepfake Detection](#gpu-deepfake-detection)** | Real-time deepfake detection for video calls | NVIDIA Triton, TensorRT, PyTorch | Client Project | [Case Study](../docs/02-case-studies.md#case-study-3-gpu-accelerated-deepfake-detection-system) |
| **[Intelligent CV Generator](#intelligent-cv-generator)** | AI-powered CV builder that adapts to job offers | GPT-4, Azure OpenAI, WeasyPrint | Open Source | [GitHub](https://github.com/lrusso94/intelligent-cv-builder) |
| **[FaceForensics++ Pipeline](#faceforensics-pipeline)** | Deepfake detection training pipeline with MLflow | PyTorch, MLflow, AKS, Terraform | Academic/Internal | [Details](#faceforensics-pipeline) |
| **[MLOps Platform Starter](#mlops-platform-starter)** | End-to-end MLOps platform with CI/CD | MLflow, Kubernetes, GitHub Actions | Planned | [Details](#mlops-platform-starter) |
| **[RAG Evaluation Framework](#rag-evaluation-framework)** | Automated RAG quality assessment | LangChain, Pytest, Azure OpenAI | Planned | [Details](#rag-evaluation-framework) |

---

## Project Details

### Agent Mesh Platform

**Problem:**
Multiple teams building AI agents independently, leading to duplicated effort, inconsistent quality, and no centralized monitoring.

**Solution:**
Built a self-service platform where teams define agents in YAML, deploy via CLI, and monitor via centralized dashboard.

**Key Features:**
- YAML-based agent definitions (no code required for simple agents)
- LangGraph orchestration with sequential, parallel, and hierarchical workflows
- Centralized observability (LangSmith traces, cost attribution per team)
- Self-service deployment (CLI tool + web UI)

**Tech Stack:**
- **Orchestration:** LangGraph, LangChain, Azure OpenAI
- **Backend:** FastAPI, Celery (async tasks), Redis, PostgreSQL
- **Infrastructure:** AKS, Terraform, Helm, Prometheus
- **Frontend:** React dashboard (monitoring only)

**Outcome:**
- Time-to-deploy: 2 weeks → 2 days for new agent use cases
- 3 agents reused by 2+ teams (saved ~200 hours of dev time)
- 99.2% uptime over 3 months

**Learn More:** [Case Study](../docs/02-case-studies.md#case-study-2-multi-agent-orchestration-platform)

---

### Enterprise RAG System

**Problem:**
Major European bank (€200B+ assets, 20,000+ employees) needed internal knowledge assistant to search 10k+ policy documents. Manual search took 20-30 minutes per query.

**Solution:**
Built production RAG system with hybrid search (keyword + semantic), Azure OpenAI, and LLM-as-judge evaluation.

**Key Features:**
- Hybrid search with Azure AI Search (keyword + vector)
- Cross-encoder reranking for top-10 → top-3 refinement
- Citation system (every answer includes source documents)
- Evaluation framework (LLM-as-judge + human labeling)

**Tech Stack:**
- **Backend:** FastAPI, LangChain, Azure OpenAI, Azure AI Search, Redis
- **Infrastructure:** AKS (3-node cluster), Terraform, Helm
- **CI/CD:** Azure DevOps, Docker, pytest
- **Monitoring:** Application Insights, Prometheus, Grafana

**Outcome:**
- Query time: 25 min → 8 seconds
- 91% accuracy on test set (500 queries)
- €3.20 per 1000 queries (cost-effective)
- 1,200 active users after 3 months

**Learn More:** [Case Study](../docs/02-case-studies.md#case-study-1-enterprise-rag-system-for-financial-services)

---

### GPU Deepfake Detection

**Problem:**
Cybersecurity firm (~200 employees, B2B SaaS) needed real-time deepfake detection for video calls to prevent social engineering attacks. Existing CPU model took 45 seconds per frame.

**Solution:**
Optimized PyTorch model to TensorRT, deployed on NVIDIA Triton Inference Server with dynamic batching.

**Key Features:**
- Model quantization (FP32 → FP16) with TensorRT
- NVIDIA Triton dynamic batching (max 32 frames)
- Real-time video frame extraction and inference
- Privacy-preserving (zero data retention)

**Tech Stack:**
- **ML Stack:** PyTorch → ONNX → TensorRT, NVIDIA Triton
- **Infrastructure:** AKS with GPU node pools (NVIDIA T4), Terraform
- **Backend:** FastAPI (frame extraction), gRPC (Triton client)
- **Monitoring:** Prometheus (GPU metrics), Grafana dashboards

**Outcome:**
- Latency: 45s → 0.8s per frame (10x faster)
- 500 concurrent calls supported
- €8k/month actual cost (under €15k budget)
- 96% detection accuracy

**Learn More:** [Case Study](../docs/02-case-studies.md#case-study-3-gpu-accelerated-deepfake-detection-system)

---

### Intelligent CV Generator

**Problem:**
Manual CV tailoring for each job application is time-consuming and inconsistent.

**Solution:**
Built AI-powered CV generator that analyzes job offers, extracts keywords, and generates tailored CVs in the job offer's language.

**Key Features:**
- Automatic language detection (ES/EN/CA/FR/DE)
- Keyword extraction and bolding in CV
- Compatibility scoring (skills match, experience match, culture fit)
- PDF generation with professional styling and AI-generated disclaimer
- Anti-invention rules (strict prompts to prevent fabricating experience)

**Tech Stack:**
- **AI:** Azure OpenAI GPT-4, custom prompts with structured outputs
- **Backend:** Python, FastAPI, WeasyPrint (PDF generation)
- **Data:** Structured JSON profile as single source of truth

**Outcome:**
- Generated 10+ tailored CVs with 80-90% compatibility scores
- Reduced CV preparation time from 2 hours → 5 minutes
- Open-sourced for others to use

**GitHub:** [lrusso94/intelligent-cv-builder](https://github.com/lrusso94/intelligent-cv-builder) *(placeholder—will be public soon)*

---

### FaceForensics++ Pipeline

**Problem:**
Training deepfake detection models requires complex data preprocessing, GPU orchestration, and experiment tracking.

**Solution:**
Built end-to-end training pipeline for FaceForensics++ dataset with MLflow tracking and Kubernetes GPU jobs.

**Key Features:**
- Automated data preprocessing (face extraction, augmentation)
- Kubernetes GPU jobs for distributed training
- MLflow experiment tracking (hyperparameters, metrics, artifacts)
- Model registry with staging → production workflow
- Evaluation framework (accuracy, precision, recall, ROC-AUC)

**Tech Stack:**
- **ML Stack:** PyTorch, Torchvision, MLflow
- **Infrastructure:** AKS with GPU node pools, Terraform, Helm
- **Data:** FaceForensics++ dataset (1M+ frames)
- **Monitoring:** TensorBoard, Prometheus

**Outcome:**
- Trained 5 model variants (ResNet, EfficientNet, ViT)
- 94% accuracy on test set
- Experiment tracking reduced debugging time by 50%

**Status:** Academic project / Internal tool (not public)

---

### MLOps Platform Starter

**Problem:**
Setting up MLOps infrastructure (experiment tracking, model registry, CI/CD, monitoring) from scratch takes weeks.

**Solution:**
Open-source starter template with Terraform modules for end-to-end MLOps platform on Kubernetes.

**Planned Features:**
- **Experiment Tracking:** MLflow with PostgreSQL backend, Azure Blob Storage for artifacts
- **Model Registry:** MLflow model registry with staging/production stages
- **CI/CD:** GitHub Actions for model training, testing, deployment
- **Model Serving:** FastAPI + Docker + Kubernetes with auto-scaling
- **Monitoring:** Prometheus + Grafana for metrics, Application Insights for traces
- **Infrastructure-as-Code:** Terraform modules for AKS, Azure Storage, networking

**Tech Stack:**
- **MLOps:** MLflow, Kubernetes, Docker, GitHub Actions
- **Infrastructure:** Terraform, Helm, Azure (AKS, Blob Storage, Application Insights)
- **Monitoring:** Prometheus, Grafana, Azure Monitor

**Status:** 🚧 **Planned** (target: Q2 2025)

**Why This Matters:**
- Reduces MLOps setup time from weeks to hours
- Provides opinionated best practices (not a blank canvas)
- Multi-cloud ready (Azure first, GCP/AWS modules later)

---

### RAG Evaluation Framework

**Problem:**
Evaluating RAG systems is hard—no standardized metrics, LLM-as-judge is inconsistent, human labeling is slow.

**Solution:**
Open-source evaluation framework with multiple metrics (correctness, relevance, faithfulness, latency) and automated testing.

**Planned Features:**
- **Metrics:**
  - Correctness: LLM-as-judge + human labeling
  - Relevance: Retrieval precision@K, recall@K
  - Faithfulness: Answer grounded in retrieved docs?
  - Latency: p50, p95, p99 for retrieval + generation
  - Cost: Tokens per query, monthly budget tracking
- **Test Sets:** Curated Q&A pairs with expected answers
- **CI/CD Integration:** Run evaluation on every PR (no regressions)
- **Dashboards:** Track metrics over time (detect drift)

**Tech Stack:**
- **Evaluation:** LangChain, Azure OpenAI, Pytest
- **Metrics Storage:** PostgreSQL, Prometheus
- **Dashboards:** Grafana, Streamlit
- **CI/CD:** GitHub Actions

**Status:** 🚧 **Planned** (target: Q2 2025)

**Why This Matters:**
- RAG systems degrade over time without evaluation
- Manual testing doesn't scale beyond 10 queries
- Need automated, continuous evaluation for production

---

## Future Projects (Ideas)

These are projects I'd love to build if I had more time:

1. **Multi-Cloud MLOps Platform** – Portable MLOps infrastructure (Azure, GCP, AWS) with unified API
2. **Agentic Workflow Studio** – Visual editor for LangGraph workflows (drag-and-drop agent design)
3. **Cost Optimization Toolkit** – Automated token usage analysis, prompt caching, model selection for LLMs
4. **Federated Learning Framework** – Privacy-preserving model training across distributed data sources
5. **AI Governance Dashboard** – Centralized monitoring for AI systems (cost, compliance, performance, drift)

**Interested in collaborating?** Reach out: [lrussobertolez@gmail.com](mailto:lrussobertolez@gmail.com)

---

## How to Navigate This Portfolio

- **For Recruiters:** Start with [Featured Projects](#featured-projects) table (quick overview)
- **For Engineers:** Read [Case Studies](../docs/02-case-studies.md) for deep dives
- **For Architects:** Check [Architecture Notes](../docs/03-architecture-notes.md) for design patterns
- **For Hiring Managers:** Read [Signal & Scope](../docs/04-signal-and-scope.md) to understand what I do/don't do

---

## Want to See Code?

Most projects are client work (not public), but I'm working on open-sourcing the Intelligent CV Generator and MLOps Platform Starter.

**GitHub (coming soon):** [github.com/lrusso94](https://github.com/lrusso94)

In the meantime, if you want to discuss any project in detail, [let's talk](mailto:lrussobertolez@gmail.com).
