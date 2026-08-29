# 🚀 GenAI System Design Interview Questions — 2026

A practical system-design preparation guide for **Senior / 6+ Years GenAI Engineer interviews**.

This list focuses on **scenario-based system design questions** rather than isolated topics.
In real interviews, one broad architecture question can test multiple concepts such as RAG, vector databases, hybrid search, reranking, agents, security, scalability, evaluation, observability, latency, and cost optimization.

---

# 📚 Table of Contents

* [How to Use This Guide](#-how-to-use-this-guide)
* [Tier 1 — Must Prepare](#-tier-1--must-prepare)
* [Tier 2 — Agents](#-tier-2--agents)
* [Tier 3 — LLM Application Platform](#-tier-3--llm-application-platform)
* [Tier 4 — Production and LLMOps](#-tier-4--production-and-llmops)
* [Tier 5 — Advanced](#-tier-5--advanced)
* [Top 10 Priority Questions](#-top-10-priority-questions)
* [What Interviewers Evaluate](#-what-interviewers-evaluate)
* [Senior-Level Answer Framework](#-senior-level-answer-framework)

---

# 🎯 How to Use This Guide

Do **not** memorize these as 20 independent questions.

Instead, treat them as **20 master scenarios**.

For example, an interviewer may ask:

> "Design an enterprise RAG system for 10 million documents."

Then follow-up questions may cover:

* Hybrid search
* BM25
* Vector search
* Reranking
* Chunking
* Metadata filtering
* RBAC
* Multi-tenancy
* Caching
* Scaling
* Evaluation
* Observability
* Cost optimization

Therefore, one system-design question can test **5–10 different GenAI concepts**.

---

# 🔥 Tier 1 — Must Prepare

## 1. Enterprise-Scale RAG

### Interview Question

> **Design a production-grade RAG system for an enterprise with 10M+ documents, supporting 50K concurrent users.**

### Topics to Cover

* Document ingestion
* PDF/document parsing
* OCR
* Layout extraction
* Chunking
* Embeddings
* Vector database
* Metadata storage
* Hybrid search
* Reranking
* Prompt construction
* LLM integration
* Streaming
* Caching
* Horizontal scaling
* Database scaling
* Cost optimization
* Evaluation
* Observability
* Disaster recovery

### Expected Architecture

```text
                    Users
                      |
                      v
                API Gateway
                      |
                      v
             Authentication
                      |
                      v
                Chat Service
                      |
             +--------+--------+
             |                 |
             v                 v
        Query Rewrite      Cache
             |
             v
      Hybrid Retrieval
       /            \
      v              v
   BM25          Vector Search
      \              /
       \            /
          v      v
          Reranker
             |
             v
       Context Builder
             |
             v
            LLM
             |
             v
        Guardrails
             |
             v
         Streaming
             |
             v
            User
```

---

# 2. Secure Multi-Tenant RAG

### Interview Question

> **Design a multi-tenant enterprise RAG platform where users can only retrieve documents they are authorized to access.**

### Topics to Cover

* Multi-tenancy
* Tenant isolation
* RBAC
* ACL
* Document-level permissions
* Metadata filtering
* Pre-filtering vs post-filtering
* PostgreSQL Row-Level Security
* Vector DB filtering
* Encryption
* Audit logs
* Data leakage prevention
* Authentication
* Authorization

### Key Question

> How do you guarantee that Tenant A can never retrieve Tenant B's documents?

---

# 3. High-Precision Enterprise Search

### Interview Question

> **Design a search/RAG system combining keyword search, semantic search, and reranking to achieve high retrieval precision.**

### Architecture

```text
                User Query
                    |
          +---------+---------+
          |                   |
          v                   v
       BM25             Vector Search
          |                   |
          +---------+---------+
                    |
                    v
                   RRF
                    |
                    v
                 Top-K
                    |
                    v
              Cross Encoder
                    |
                    v
                  Top-N
                    |
                    v
                   LLM
```

### Topics to Cover

* BM25
* Dense embeddings
* Hybrid search
* Reciprocal Rank Fusion
* Reranking
* Cross-encoder
* ColBERT
* Contextual compression
* Lost-in-the-middle

---

# 4. Real-Time Document Ingestion

### Interview Question

> **Design a document ingestion platform that processes thousands of document uploads, updates, and deletions per minute while keeping search available.**

### Topics to Cover

* Object storage
* Event-driven architecture
* Kafka / SQS
* Async workers
* OCR
* Parsing
* Chunking
* Embedding generation
* Idempotency
* Retries
* Dead-letter queues
* Versioning
* Re-indexing
* Deletion
* Tombstones
* Eventual consistency

### Architecture

```text
Upload
   |
   v
Object Storage
   |
   v
Message Queue
   |
   v
Document Workers
   |
   +----> OCR
   |
   +----> Parser
   |
   +----> Chunker
   |
   +----> Embedding
   |
   v
Vector Database
```

---

# 5. Complex / Long-Document Q&A

### Interview Question

> **Design a system where users upload a 500-page financial report and ask questions requiring reasoning across multiple distant sections.**

### Topics to Cover

* Hierarchical chunking
* Parent-child chunks
* Metadata
* Query decomposition
* Multi-hop retrieval
* Long-context models
* Reranking
* Context-window management
* Aggregation
* Agentic retrieval

---

# 🤖 Tier 2 — Agents

# 6. Production AI Agent

### Interview Question

> **Design an autonomous AI agent that understands a task, selects tools, executes actions, observes results, and recovers from failures.**

### Topics to Cover

* Planning
* Tool calling
* State management
* Memory
* Tool authorization
* Retry
* Timeout
* Error handling
* Infinite-loop prevention
* Human-in-the-loop
* Idempotency

### Architecture

```text
User
 |
 v
Agent
 |
 v
Planner
 |
 v
Tool Selection
 |
 v
Tool Execution
 |
 v
Observation
 |
 +--------> Next Action
 |
 v
Final Response
```

---

# 7. LangGraph Stateful Agent

### Interview Question

> **Design a coding agent using graph-based orchestration that reads a codebase, modifies code, runs tests, and iteratively fixes failures.**

### Architecture

```text
START
  |
  v
Understand Task
  |
  v
Plan
  |
  v
Tool Call
  |
  v
Execute
  |
  v
Run Tests
  |
  +------ PASS ------> END
  |
 FAILURE
  |
  v
Analyze Error
  |
  v
Fix Code
  |
  +------------------> Run Tests
```

### Topics to Cover

* Stateful workflows
* Graph orchestration
* Cyclic workflows
* Checkpoints
* Persistence
* Human approval
* Tool execution
* Retry
* Infinite-loop prevention
* State serialization

---

# 8. Multi-Agent Customer Support

### Interview Question

> **Design a multi-agent customer-support system with specialized billing, technical, and shipping agents coordinated by a supervisor.**

### Architecture

```text
                     User
                       |
                       v
                 Supervisor
                 /    |     \
                /     |      \
               v      v       v
           Billing  Technical Shipping
            Agent     Agent     Agent
               \       |       /
                \      |      /
                 v     v     v
                  Response
```

### Topics to Cover

* Supervisor pattern
* Agent routing
* Shared state
* Context handoff
* Tool authorization
* Inter-agent communication
* Failure handling

---

# 9. Long-Term Agent Memory

### Interview Question

> **Design an AI assistant that remembers useful information about a user across months of conversations without storing or retrieving irrelevant information.**

### Topics to Cover

* Short-term memory
* Long-term memory
* Episodic memory
* Semantic memory
* Memory extraction
* Importance scoring
* Memory consolidation
* Vector storage
* Memory retrieval
* Memory deletion
* Privacy

---

# ⚡ Tier 3 — LLM Application Platform

# 10. Enterprise LLM Gateway

### Interview Question

> **Design an LLM Gateway supporting Azure OpenAI, OpenAI, and Anthropic with automatic model routing, fallback, retries, token tracking, and cost monitoring.**

### Architecture

```text
                    Client
                      |
                      v
                 API Gateway
                      |
                      v
                 LLM Gateway
                      |
          +-----------+-----------+
          |           |           |
          v           v           v
     Azure OpenAI   OpenAI    Anthropic
          |           |           |
          +-----------+-----------+
                      |
                      v
                   Response
```

### Topics to Cover

* Provider abstraction
* Model routing
* Fallback
* Retries
* Timeout
* Circuit breaker
* Token tracking
* Cost tracking
* Rate limiting
* Streaming
* API normalization

---

# 11. Million-User Streaming AI Chat

### Interview Question

> **Design a ChatGPT-like streaming application supporting 1M+ users with low latency and controlled infrastructure cost.**

### Topics to Cover

* SSE
* WebSockets
* FastAPI
* Stateless services
* Redis
* PostgreSQL
* Connection management
* Horizontal scaling
* Streaming
* Rate limiting
* API Gateway
* Load balancing
* CDN

### Architecture

```text
Users
  |
  v
CDN / Load Balancer
  |
  v
API Gateway
  |
  v
Chat Service
  |
  +------ Redis
  |
  +------ PostgreSQL
  |
  +------ LLM Gateway
              |
              v
             LLM
              |
              v
          Streaming
              |
              v
             User
```

---

# 12. Low-Latency LLM Application

### Interview Question

> **Design an LLM application where response latency must remain below a strict SLA while maintaining answer quality.**

### Latency Components

```text
Total Latency
     |
     +-- Network
     +-- Retrieval
     +-- Reranking
     +-- Prompt Processing
     +-- LLM TTFT
     +-- Token Generation
```

### Topics to Cover

* Streaming
* TTFT
* TPOT
* Caching
* Smaller models
* Model routing
* Parallel retrieval
* Prompt optimization
* Batching
* Speculative decoding

---

# 13. Semantic LLM Caching

### Interview Question

> **Design a caching system that prevents unnecessary LLM calls while ensuring cached responses are not semantically incorrect or stale.**

### Topics to Cover

* Exact-match cache
* Semantic cache
* Embeddings
* Similarity threshold
* Redis
* TTL
* Cache invalidation
* Document-version based invalidation
* Context-aware caching

---

# 14. Distributed AI Rate Limiter

### Interview Question

> **Design a distributed rate limiter for an AI API that enforces RPM and TPM quotas across thousands of customers.**

### Topics to Cover

* Token bucket
* Sliding window
* Redis
* Atomic operations
* Distributed counters
* RPM
* TPM
* Race conditions
* Per-user limits
* Per-tenant limits
* Global limits

---

# 🛡️ Tier 4 — Production & LLMOps

# 15. GenAI Evaluation Platform

### Interview Question

> **Design a production evaluation platform that continuously measures the quality, correctness, faithfulness, and safety of a RAG/Agent application.**

### Architecture

```text
Production Requests
        |
        v
     Logging
        |
        v
 Evaluation Dataset
        |
        v
 Automated Evaluation
        |
        v
 LLM-as-a-Judge
        |
        v
     Metrics
        |
        v
 Regression Detection
        |
        v
 Dashboard / Alerts
```

### Topics to Cover

* Golden datasets
* Offline evaluation
* Online evaluation
* LLM-as-a-judge
* Faithfulness
* Relevance
* Groundedness
* Hallucination
* Regression testing
* Dataset drift

---

# 16. GenAI Observability Platform

### Interview Question

> **Design an observability system that traces every step of an agentic RAG request and identifies latency, errors, and token costs.**

### Example Trace

```text
Request
  |
  v
Query Rewrite
  |
  v
Retriever
  |
  v
Reranker
  |
  v
LLM
  |
  v
Tool
  |
  v
LLM
  |
  v
Response
```

### Metrics

* TTFT
* TPOT
* End-to-end latency
* Token usage
* Cost
* Retrieval scores
* Error rate
* Tool calls
* Model usage
* Prompt version
* Cache hit rate

---

# 17. LLM Guardrails & Prompt Injection Defense

### Interview Question

> **Design a production guardrail layer protecting an enterprise AI application against prompt injection, jailbreaks, PII leakage, and unsafe outputs.**

### Topics to Cover

* Input validation
* Prompt injection detection
* Jailbreak detection
* Output validation
* PII detection
* Content moderation
* Tool permissions
* Sandboxing
* Policy enforcement
* Human escalation
* Audit logging

### Architecture

```text
User Input
    |
    v
Input Guardrails
    |
    v
Prompt Injection Detection
    |
    v
Agent / RAG / LLM
    |
    v
Output Guardrails
    |
    v
PII / Safety Check
    |
    v
Response
```

---

# 18. Prompt Management Platform

### Interview Question

> **Design an enterprise prompt-management system supporting prompt versioning, testing, A/B experiments, deployment, and rollback without redeploying application code.**

### Topics to Cover

* Prompt registry
* Version control
* Prompt templates
* Variables
* Environments
* A/B testing
* Canary deployment
* Rollback
* Prompt evaluation
* Telemetry
* KPI correlation

---

# 🧠 Tier 5 — Advanced / Company Dependent

# 19. LLM Inference Platform

### Interview Question

> **Design a high-performance LLM serving infrastructure capable of handling thousands of concurrent generation requests while minimizing GPU memory usage and latency.**

### Topics to Cover

* KV Cache
* PagedAttention
* Continuous batching
* GPU utilization
* Tensor parallelism
* Quantization
* Speculative decoding
* vLLM
* GPU scheduling
* Model serving
* Autoscaling

> **Priority:** Very high for ML Infrastructure / Model Serving roles, but lower for application-focused GenAI Engineer roles.

---

# 20. Fine-Tuning / Distillation Platform

### Interview Question

> **Design a pipeline that uses production data from an expensive frontier model to fine-tune a smaller model while maintaining acceptable quality at a fraction of the cost.**

### Topics to Cover

* Data collection
* Data sanitization
* Data filtering
* Synthetic data
* Instruction tuning
* LoRA
* QLoRA
* Fine-tuning
* Evaluation
* Regression testing
* Model registry
* Deployment
* Monitoring
* Cost comparison

---

# ⭐ Top 10 Priority Questions

If you have limited preparation time, focus on these first:

```text
1. Enterprise RAG
2. Secure Multi-Tenant RAG
3. Hybrid Search + Reranking
4. Real-Time Document Ingestion
5. Production AI Agent
6. LangGraph Stateful Agent
7. Enterprise LLM Gateway
8. 1M+ User Streaming AI Chat
9. GenAI Evaluation Platform
10. GenAI Observability
```

---

# 🎯 What Interviewers Evaluate

When you answer a system-design question, interviewers are generally evaluating more than whether you know RAG or LangChain.

## 1. Requirements

Can you clarify:

* Number of users
* Number of documents
* Request volume
* Latency requirements
* Availability requirements
* Data size
* Security requirements
* Cost constraints

---

## 2. Architecture

Can you design:

* APIs
* Services
* Databases
* Queues
* Storage
* LLM layer
* Vector database
* Cache
* Authentication
* Monitoring

---

## 3. Scalability

Explain:

* Horizontal scaling
* Load balancing
* Database scaling
* Vector DB scaling
* Partitioning
* Sharding
* Async processing
* Queues
* Caching

---

## 4. Reliability

Discuss:

* Retries
* Timeouts
* Circuit breakers
* Dead-letter queues
* Idempotency
* Failover
* Graceful degradation
* Disaster recovery

---

## 5. Security

Discuss:

* Authentication
* Authorization
* RBAC
* Tenant isolation
* Encryption
* PII
* Prompt injection
* Audit logs
* Secrets management

---

## 6. GenAI-Specific Concerns

Always consider:

* Hallucination
* RAG quality
* Retrieval precision
* Context window
* Prompt quality
* Token usage
* Model selection
* Model fallback
* Evaluation
* Guardrails

---

## 7. Cost

Discuss:

```text
LLM Cost
+
Embedding Cost
+
Vector DB
+
Database
+
Compute
+
Storage
+
Network
+
Observability
```

Then explain how you would reduce cost.

---

## 8. Observability

Monitor:

* Latency
* TTFT
* TPOT
* Token usage
* Cost
* Error rate
* Retrieval quality
* LLM quality
* Cache hit rate
* Queue depth
* GPU utilization

---

# 🏆 Senior-Level System Design Answer Framework

For almost every GenAI system-design question, follow this sequence:

```text
1. Clarify Requirements
          ↓
2. Estimate Scale
          ↓
3. Define APIs
          ↓
4. High-Level Architecture
          ↓
5. Explain Data Flow
          ↓
6. Database Design
          ↓
7. RAG / Agent / LLM Architecture
          ↓
8. Scalability
          ↓
9. Reliability
          ↓
10. Security
          ↓
11. Evaluation
          ↓
12. Observability
          ↓
13. Cost Optimization
          ↓
14. Bottlenecks & Trade-offs
```

---

# 💡 Golden Rule for Senior Interviews

Don't answer:

> "I will use LangChain, PostgreSQL, Redis and OpenAI."

Instead answer:

> **"Given these requirements, I would choose X because of Y, and the trade-off is Z."**

For example:

> "I would use hybrid retrieval rather than relying only on dense retrieval because enterprise documents often contain exact identifiers, product codes, error codes, and legal terminology where lexical matching performs better. I would then use a reranker to improve precision before passing the final context to the LLM."

That demonstrates **architecture thinking**, not just tool knowledge.

---

# 🚀 Final Preparation Strategy

### Phase 1 — Master Architecture

Study:

```text
RAG
Agents
LLM Gateway
Streaming
Evaluation
Observability
Security
Scaling
```

### Phase 2 — Practice the Top 10

For each question, practice explaining:

```text
Requirements
→ Architecture
→ Data Flow
→ Storage
→ APIs
→ Scaling
→ Security
→ Reliability
→ Evaluation
→ Monitoring
→ Cost
```

### Phase 3 — Practice Follow-Ups

For every design, expect:

> "What if traffic becomes 10x?"

> "What if the vector DB goes down?"

> "How do you prevent data leakage?"

> "How do you reduce cost?"

> "How do you measure RAG quality?"

> "How do you handle hallucination?"

> "Why PostgreSQL/pgvector instead of a dedicated vector DB?"

> "Why Kafka?"

> "Why Redis?"

> "Why SSE instead of WebSockets?"

> "What happens if the LLM provider goes down?"

> "How would you deploy this on AWS?"

---

# 📌 Target

If you can confidently design these **20 scenarios** and handle the follow-up questions, you will cover a large portion of the **Senior GenAI System Design** skill set:

```text
                SENIOR GENAI
                SYSTEM DESIGN
                      |
       +--------------+--------------+
       |              |              |
       v              v              v
      RAG           Agents       LLM Platform
       |              |              |
       v              v              v
   Retrieval       State          Gateway
   Security        Tools          Routing
   Scaling         Memory         Streaming
       |              |              |
       +--------------+--------------+
                      |
                      v
                Production
                      |
       +--------------+--------------+
       |              |              |
       v              v              v
    Security       Evaluation    Observability
       |              |              |
       +--------------+--------------+
                      |
                      v
              Scale + Reliability
                      |
                      v
                Cost Optimization
```

**This is the master GenAI System Design checklist to keep in your GitHub interview-preparation repository.**
