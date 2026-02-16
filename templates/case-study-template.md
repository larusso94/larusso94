# Case Study Template

> Use this template to document production AI projects in a structured way. Anonymize client details, but keep technical facts accurate.

---

## [Project Name]

### Problem
[1-2 sentences describing the business problem. What was broken? What pain did users/client experience?]

**Example:** "Large banking client needed an internal knowledge assistant to help employees find information across 10,000+ policy documents. Manual search was taking 20-30 minutes per query."

---

### Business Context
**Users:** [Who will use this system? How many?]  
**Content/Data:** [What data sources? What format? How much?]  
**Requirements:** [Key business requirements—latency, accuracy, compliance, cost, etc.]

**Example:**
- **Users:** 2,000+ internal employees (compliance, legal, operations)
- **Content:** 10,000+ documents (PDF, Word, SharePoint)
- **Requirements:** GDPR compliance, audit logs, <5s query latency, 95%+ accuracy

---

### Technical Constraints
[List hard constraints that shaped the solution. Cloud provider, budget, integration requirements, security/compliance needs.]

**Example:**
- Must run on Azure (client's cloud)
- No data can leave EU region
- Integration with existing Azure AD for auth
- Budget: €50k for infra (6 months)

---

### Approach
[High-level timeline and phases. Keep it brief—3-5 bullet points.]

**Example:**
1. **Discovery (2 weeks):** Analyzed document types, user queries, existing systems
2. **Architecture Design (1 week):** Hybrid search, Azure OpenAI, Azure AI Search
3. **Implementation (8 weeks):** Built ingestion pipeline, deployed RAG backend, evaluation framework
4. **Testing & Rollout (4 weeks):** UAT, gradual rollout from 50 → 2,000 users

---

### Architecture Decisions
[Key technical decisions with rationale. Format: **Decision:** Explanation (trade-off)]

**Example:**
- **Vector Database:** Azure AI Search (native Azure integration, GDPR compliance, hybrid search built-in)
- **LLM:** Azure OpenAI GPT-4 with prompt caching (cost vs. accuracy trade-off)
- **Chunking Strategy:** Recursive character splitter with 1000 token chunks, 200 overlap (balanced context vs. precision)
- **Reranking:** Cross-encoder model to refine top-10 results from hybrid search
- **Evaluation:** LLM-as-judge for correctness + human labeling for 500 test queries

---

### Key Technologies
**Backend:** [FastAPI, Flask, etc.]  
**AI/ML Stack:** [LangChain, LangGraph, Azure OpenAI, vector DB, etc.]  
**Infrastructure:** [Kubernetes, Terraform, cloud services]  
**CI/CD:** [GitHub Actions, Azure DevOps, etc.]  
**Monitoring:** [Prometheus, Grafana, Application Insights, etc.]

**Example:**
**Backend:** FastAPI, LangChain, Azure OpenAI, Azure AI Search, Redis (caching)  
**Infrastructure:** AKS (3-node cluster), Terraform, Helm, Azure Application Insights  
**CI/CD:** Azure DevOps, Docker, automated testing with pytest  
**Monitoring:** Application Insights for traces, Prometheus + Grafana for metrics

---

### Delivery Timeline
[Brief week-by-week or month-by-month timeline. Total duration at the end.]

**Example:**
- Week 1-2: Discovery & requirements
- Week 3: Architecture design & approval
- Week 4-11: Development (ingestion, RAG backend, evaluation)
- Week 12-15: Testing & rollout
- **Total:** 15 weeks from kickoff to production

---

### Risk Mitigation
[What could go wrong? How did you prevent or handle it?]

**Example:**
- **Hallucinations:** Implemented citation system (every answer includes source docs) + human-in-the-loop for critical queries
- **Cost Overruns:** Set up prompt caching, token usage monitoring, alerts at 80% budget
- **Data Privacy:** All data encrypted at rest/transit, Azure Private Link, audit logs for all queries

---

### Measurable Outcomes
[Quantifiable results. Before/after metrics, user satisfaction, cost, adoption.]

**Example:**
- **Query time:** 25 min → 8 seconds (average)
- **User satisfaction:** 87% positive feedback in pilot (50 users)
- **Cost:** €3.20 per 1000 queries (within budget)
- **Accuracy:** 91% correct answers on test set (500 queries)
- **Adoption:** 1,200 active users after 3 months

---

### Lessons Learned
[3-5 bullet points. What worked? What didn't? What would you do differently?]

**Example:**
1. **Chunking matters more than embeddings** – Spent 2 weeks optimizing chunking strategy; improved accuracy by 12%
2. **Evaluation is hard** – LLM-as-judge disagreed with humans 18% of the time; hybrid eval is necessary
3. **Caching saves money** – Prompt caching reduced costs by 40% for repeated queries
4. **Users need citations** – Without source docs, users didn't trust answers (learned in week 1 of pilot)

---

### Next Steps (Optional)
[If you had more time, what would you add? What's on the roadmap?]

**Example:**
- Multi-modal RAG (process images, tables in PDFs)
- Fine-tuned reranker on domain data
- Agentic layer for multi-hop reasoning (e.g., "Compare policy X and Y")

---

## Usage Tips

1. **Anonymize client details** – Replace company names with "Large banking client", "Energy tech startup", etc.
2. **Keep technical facts accurate** – Don't inflate numbers or invent features
3. **Focus on decisions and trade-offs** – Explain *why* you chose X over Y
4. **Use metrics** – Numbers are more convincing than adjectives ("10x faster" > "much faster")
5. **Be honest about lessons learned** – Mistakes make you credible; pretending everything was perfect doesn't

---

## Example Case Studies

See [docs/02-case-studies.md](../docs/02-case-studies.md) for three full examples using this template.
