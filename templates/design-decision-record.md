# Architecture Decision Record (ADR) Template

> Use this template to document significant architectural decisions. Keep it concise and focused on the "why" behind each choice.

---

## ADR-[NUMBER]: [Short Title of Decision]

**Date:** [YYYY-MM-DD]  
**Status:** [Proposed | Accepted | Deprecated | Superseded]  
**Deciders:** [Names or roles of people who made this decision]  
**Tags:** [e.g., mlops, rag, infrastructure, cost-optimization]

---

### Context

[Describe the situation that requires a decision. What forces are at play? What are the constraints?]

**Questions to answer:**
- What problem are we trying to solve?
- What technical or business constraints exist?
- What's the current state (if any)?
- Why is this decision important now?

**Example:**
"We need to choose a vector database for our production RAG system. The system will serve 500 concurrent users, ingest 10k documents/day, and must comply with GDPR (data in EU). We have a budget of €10k/month for infrastructure. Current state: prototype uses in-memory FAISS, but it doesn't scale."

---

### Decision

[State the decision clearly in 1-2 sentences.]

**Example:**
"We will use **Azure AI Search** as our vector database for the production RAG system."

---

### Alternatives Considered

[List other options you evaluated. For each, briefly explain why you didn't choose it.]

**Format:**
**[Alternative Name]**
- **Pros:** [What's good about it]
- **Cons:** [What's bad about it]
- **Why rejected:** [The deciding factor]

**Example:**

**1. Pinecone**
- **Pros:** Managed service, excellent performance, great DX
- **Cons:** Data stored in US (GDPR concern), €800/month for our scale, vendor lock-in
- **Why rejected:** GDPR compliance requires EU data residency; Pinecone doesn't offer EU-only hosting

**2. Weaviate (self-hosted)**
- **Pros:** Open source, full control, EU deployment possible, hybrid search built-in
- **Cons:** We'd need to manage infrastructure (K8s, backups, scaling), no managed option in Azure
- **Why rejected:** Team lacks time to manage another service; prefer managed solutions

**3. In-memory FAISS**
- **Pros:** Fast, simple, no cost
- **Cons:** No persistence, no multi-instance support, no hybrid search, doesn't scale
- **Why rejected:** Not production-ready for our scale and durability requirements

---

### Consequences

[Describe the outcomes of this decision. Be honest about trade-offs.]

#### **Positive**
- ✅ [Good outcome 1]
- ✅ [Good outcome 2]
- ✅ [Good outcome 3]

**Example:**
- ✅ GDPR compliant (data stays in EU region)
- ✅ Managed service (Azure handles scaling, backups, availability)
- ✅ Hybrid search built-in (keyword + semantic without extra setup)
- ✅ Native Azure integration (AAD auth, Private Link, Terraform support)

#### **Negative**
- ❌ [Trade-off 1]
- ❌ [Trade-off 2]

**Example:**
- ❌ Vendor lock-in to Azure (hard to migrate to other clouds)
- ❌ Cost scales linearly with storage (€500/month for 100GB + queries)
- ❌ Less flexible than Weaviate (custom schemas require workarounds)

#### **Neutral**
- 🟡 [Neutral consequence 1]

**Example:**
- 🟡 Learning curve for Azure AI Search API (1 week for team to ramp up)

---

### Related Decisions

[Link to other ADRs that are connected to this one.]

**Example:**
- **ADR-002: Choice of LLM Provider** (decision to use Azure OpenAI influenced this choice)
- **ADR-005: Infrastructure-as-Code Strategy** (Azure AI Search will be provisioned via Terraform)

---

### Notes

[Any additional context, links to discussions, proof-of-concept results, benchmarks, etc.]

**Example:**
- Ran benchmark: Azure AI Search (120ms p95 latency) vs. Pinecone (80ms p95). Accepted 40ms trade-off for GDPR compliance.
- Team discussion: [Link to Slack thread or meeting notes]
- Proof-of-concept code: [Link to GitHub branch]

---

### Revisit Criteria

[Under what conditions should we reconsider this decision?]

**Example:**
- If query latency exceeds 200ms p95, evaluate Pinecone again
- If Azure AI Search costs exceed €1k/month, consider self-hosted Weaviate
- If we expand to GCP, evaluate Vertex AI Vector Search

---

## Usage Guidelines

### When to Write an ADR
Write an ADR for decisions that:
- Are hard to reverse (e.g., database choice, cloud provider)
- Impact multiple teams or systems
- Involve significant cost or complexity
- Have multiple viable alternatives

### When NOT to Write an ADR
Don't write an ADR for:
- Trivial choices (e.g., naming a variable)
- Decisions that are easily reversible (e.g., library version)
- Personal preferences (e.g., code style)

### ADR Lifecycle
1. **Proposed:** Decision is being considered, feedback welcome
2. **Accepted:** Decision is final, implementation begins
3. **Deprecated:** Decision is no longer relevant (but kept for history)
4. **Superseded:** Replaced by a newer ADR (link to the new one)

### Storage
Store ADRs in `docs/adrs/` folder:
```
docs/
  adrs/
    001-vector-database-choice.md
    002-llm-provider-choice.md
    003-kubernetes-setup.md
```

### Numbering
Use sequential numbers: `001`, `002`, `003`, etc. Never reuse numbers.

---

## Example ADRs

**Real-world examples to inspire you:**

- **ADR-001: Vector Database for RAG System** (see above)
- **ADR-002: Azure OpenAI vs. Self-Hosted LLM** (managed vs. self-hosted trade-off)
- **ADR-003: Kubernetes vs. Serverless for Model Serving** (control vs. simplicity)
- **ADR-004: MLflow vs. Weights & Biases for Experiment Tracking** (cost vs. features)

---

## Further Reading

- [Architecture Decision Records by Michael Nygard](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)
- [ADR GitHub Organization](https://adr.github.io/)
- [When to Write an ADR (Thoughtworks)](https://www.thoughtworks.com/en-us/insights/blog/architecture/architecture-decision-records)

---

## Questions?

If you're documenting a decision and unsure how to structure it, feel free to reach out: [lautarorussobertolez@gmail.com](mailto:lautarorussobertolez@gmail.com)
