# 🚀 GenAI Interview Bible 2026
## Volume 3 – Embeddings & Vector Databases

# Question 7 (Part 3)

# Vector Databases
## Complete Guide to pgvector, Pinecone, Qdrant, Milvus, Weaviate & Azure AI Search

> **Difficulty:** ⭐⭐⭐⭐⭐
>
> **Experience Level:** 6+ Years
>
> **Interview Frequency:** ⭐⭐⭐⭐⭐
>
> **Category:** Vector Databases / RAG / Semantic Search / Production Architecture

---

# 📖 Table of Contents

1. Why Interviewers Ask This Question
2. 3-Minute Interview Answer
3. What is a Vector Database?
4. Traditional Database vs Vector Database
5. Why Not Use a Normal SQL Database?
6. How a Vector Database Works
7. What Does a Vector Database Store?
8. Metadata
9. Why Metadata is Important
10. pgvector
11. HNSW & IVFFlat Indexes
12. Pinecone
13. Qdrant
14. Milvus
15. Weaviate
16. Azure AI Search
17. Vector Database Comparison
18. Which Vector Database Should You Choose?
19. Production Architecture
20. Common Interview Questions
21. Common Mistakes
22. Whiteboard Diagram
23. 30-Second Interview Answer
24. Senior Engineer Tips
25. Key Takeaways

---

# 🎯 Why Interviewers Ask This Question

Once an interviewer confirms that you understand:

- LLMs
- Embeddings
- Similarity Search

the next logical question is:

> **"Where are embeddings stored and how are they searched?"**

The expected answer is **Vector Database**.

Interviewers also evaluate whether you understand:

- Why SQL databases are not enough for semantic search
- Why vector indexes are needed
- Different vector database options
- Trade-offs between pgvector, Pinecone, Qdrant, Milvus, Weaviate, and Azure AI Search
- Which database you would choose for different production scenarios

---

# ✅ 3-Minute Interview Answer

> A Vector Database is a database designed to store, index, and search vector embeddings efficiently. Unlike traditional databases that perform exact keyword matching, vector databases perform semantic similarity search using algorithms such as HNSW or IVFFlat. In a RAG application, document chunks are converted into embeddings and stored inside a vector database. When a user asks a question, the query is converted into an embedding, compared with stored vectors, and the most relevant document chunks are retrieved before sending them to the LLM.

---

# 🤔 What is a Vector Database?

A Vector Database is optimized for storing and searching high-dimensional vectors.

Instead of storing only text or numbers, it stores:

- Embedding Vector
- Original Text
- Metadata
- Document ID
- Chunk ID
- Similarity Index

Instead of asking:

```sql
SELECT * FROM documents
WHERE title = 'FastAPI';
```

A Vector Database answers:

> **"Which documents are semantically most similar to this query?"**

---

# 🗄 Traditional Database vs Vector Database

## Traditional SQL Database

Example Table

| ID | Product |
|----|----------|
| 1 | Car |
| 2 | Bike |
| 3 | Laptop |

Query

```sql
SELECT *
FROM products
WHERE product = 'Car';
```

Only exact matches are returned.

---

## Vector Database

The same data is stored as vectors.

Example

```
Car

↓

[0.14, 0.82, -0.45, ...]
```

If the user searches:

```
Automobile
```

The database retrieves:

```
Car
```

because both vectors are semantically similar.

---

# ❓ Why Not Use a Normal SQL Database?

Technically, embeddings can be stored in a SQL table.

Example:

| ID | Text | Embedding |
|----|------|-----------|

However, SQL databases were designed for:

- Exact matching
- Sorting
- Filtering
- Joins
- Transactions

They were **not designed** for:

- High-dimensional vector comparison
- Approximate Nearest Neighbor Search
- Cosine Similarity
- HNSW Graph Traversal

Searching millions of vectors one by one would be too slow.

---

# ⚙ How a Vector Database Works

### Indexing Phase

```
PDF

↓

Text Extraction

↓

Chunking

↓

Embedding Model

↓

Embedding Vector

↓

Vector Database

↓

Create Index
```

---

### Retrieval Phase

```
User Question

↓

Embedding Model

↓

Query Vector

↓

Similarity Search

↓

Top-K Chunks

↓

LLM

↓

Answer
```

---

# 📦 What Does a Vector Database Store?

A typical record contains:

```
Document ID

Embedding Vector

Original Text

Metadata

Chunk Number

Source

Timestamp
```

Example

```json
{
  "id": 101,
  "text": "FastAPI is a modern Python web framework.",
  "embedding": [0.18, -0.91, 0.42, ...],
  "metadata": {
    "source": "FastAPI.pdf",
    "page": 12,
    "department": "Engineering"
  }
}
```

---

# 🏷 What is Metadata?

Metadata is additional information stored along with the embedding.

Examples include:

- Document Name
- Author
- Department
- Version
- Country
- Language
- Creation Date
- Security Level

Metadata allows filtering before similarity search.

Example:

```
Department = HR

Country = India

Version = Latest
```

Only matching documents are searched.

---

# ⭐ Why Metadata is Important

Suppose a company has documents from:

- HR
- Finance
- Engineering

An HR employee searches:

```
Leave Policy
```

Without metadata,

Engineering documents are also searched.

With metadata filtering:

```
Department = HR
```

Only HR documents participate in similarity search.

Benefits:

- Faster Search
- Better Accuracy
- Lower Cost
- Improved Security

---

# 🐘 What is pgvector?

pgvector is an extension for PostgreSQL.

It allows PostgreSQL to store vector embeddings.

Without pgvector, PostgreSQL supports:

- Text
- Numbers
- Dates
- JSON

With pgvector, it also supports:

- Vector Embeddings

---

# Example Table

```sql
CREATE TABLE documents (

id SERIAL PRIMARY KEY,

content TEXT,

embedding VECTOR(1536)

);
```

The number **1536** represents the embedding dimension.

---

# Why Companies Use pgvector

Many organizations already use PostgreSQL.

Instead of introducing another database,

they simply install pgvector.

Advantages:

- Existing PostgreSQL Knowledge
- ACID Transactions
- SQL Queries
- Metadata Filtering
- Lower Operational Cost
- Easy Backup & Restore

---

# 📚 pgvector Index Types

pgvector supports:

## HNSW

Best for:

- Fast Search
- High Recall
- Production Systems

Example

```sql
CREATE INDEX idx_embedding

ON documents

USING hnsw (embedding vector_cosine_ops);
```

---

## IVFFlat

Groups vectors into clusters.

Advantages:

- Faster Index Creation
- Lower Memory Usage

Disadvantages:

- Slightly lower retrieval accuracy compared to HNSW.

---

# ☁ What is Pinecone?

Pinecone is a fully managed cloud-native Vector Database.

You do not manage:

- Servers
- Scaling
- Replication
- Backups
- Infrastructure

Everything is handled by Pinecone.

Advantages:

- Easy API
- Automatic Scaling
- High Availability
- Production Ready

Disadvantages:

- Paid Service
- Vendor Lock-in
- Less Infrastructure Control

---

# 🟢 What is Qdrant?

Qdrant is an open-source Vector Database.

Features:

- HNSW
- REST API
- gRPC
- Metadata Filtering
- Docker Support
- High Performance

Advantages:

- Free
- Open Source
- Excellent Filtering
- Easy Deployment

Suitable for organizations wanting complete control over their infrastructure.

---

# 🔵 What is Milvus?

Milvus is designed for massive vector datasets.

Suitable for:

- Billions of vectors
- Recommendation Systems
- AI Search
- Image Search
- Enterprise AI

Features:

- Distributed Architecture
- GPU Acceleration
- Multiple Index Types
- Horizontal Scaling

---

# 🟣 What is Weaviate?

Weaviate is another popular open-source Vector Database.

Features:

- REST API
- GraphQL
- Hybrid Search
- Multi-Tenant Support
- Built-in AI Modules

Suitable for AI-native applications.

---

# 🔷 What is Azure AI Search?

Azure AI Search is Microsoft's managed enterprise search service.

It supports:

- Full-text Search
- Semantic Search
- Vector Search
- Hybrid Search
- Metadata Filtering
- AI Skillsets

It integrates seamlessly with:

- Azure OpenAI
- Azure Blob Storage
- Azure Functions
- Azure AI Foundry

This makes it a strong choice for Azure-based enterprise applications.

---

# 📊 Vector Database Comparison

| Feature | pgvector | Pinecone | Qdrant | Milvus | Weaviate | Azure AI Search |
|----------|----------|-----------|---------|---------|------------|----------------|
| Open Source | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| Managed Cloud | ❌ | ✅ | Optional | Optional | Optional | ✅ |
| PostgreSQL Based | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Metadata Filtering | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| HNSW | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Hybrid Search | Limited | ✅ | ✅ | ✅ | ✅ | ✅ |
| Best For | Existing PostgreSQL Apps | SaaS | Open Source | Enterprise Scale | AI Applications | Azure Enterprise |

---

# 🎯 Which Vector Database Should You Choose?

### Small Projects

✅ pgvector

---

### Existing PostgreSQL Applications

✅ pgvector

---

### Startup

✅ Pinecone

---

### Open Source Projects

✅ Qdrant

---

### Billion-Scale AI Systems

✅ Milvus

---

### Azure Enterprise Applications

✅ Azure AI Search

---

# 🏗 Production Architecture

```
                User
                  │
                  ▼
             FastAPI API
                  │
                  ▼
          Authentication
                  │
                  ▼
          Query Rewriting
                  │
                  ▼
         Embedding Model
                  │
                  ▼
      Azure AI Search / pgvector
                  │
                  ▼
        Similarity Search
                  │
                  ▼
           Top-K Chunks
                  │
                  ▼
          Prompt Builder
                  │
                  ▼
          Azure OpenAI LLM
                  │
                  ▼
            Final Answer
```

---

# 💬 Common Interview Questions

### Can PostgreSQL become a Vector Database?

Yes.

By installing the **pgvector** extension.

---

### Can pgvector replace Pinecone?

For many small and medium-sized production systems, yes.

For globally distributed or extremely large workloads, managed vector databases may provide operational advantages.

---

### Why not MongoDB?

MongoDB also supports vector search in recent versions.

However, PostgreSQL with pgvector or dedicated vector databases are often preferred depending on architecture, operational requirements, and ecosystem.

---

### What is stored besides embeddings?

- Original Text
- Metadata
- Source Document
- Chunk ID
- Security Information

---

### Why store original text?

Embeddings are only mathematical representations.

The LLM needs the original document text to generate answers.

---

### Can one document have multiple embeddings?

Yes.

Documents are split into chunks.

Each chunk receives its own embedding.

---

# ❌ Common Mistakes

### Mistake 1

❌ Vector Databases store only vectors.

✔ They also store metadata, original text, document references, and indexes.

---

### Mistake 2

❌ Vector Databases replace SQL databases.

✔ They usually complement SQL databases.

---

### Mistake 3

❌ pgvector is a separate database.

✔ pgvector is an extension for PostgreSQL.

---

# 🖊 Whiteboard Architecture

```
Documents

↓

Chunking

↓

Embedding Model

↓

Embedding Vectors

↓

pgvector / Pinecone / Qdrant

↓

HNSW Index

↓

Similarity Search

↓

Top-K

↓

Prompt Builder

↓

LLM

↓

Answer
```

---

# ⚡ 30-Second Interview Answer

> A Vector Database stores embeddings and performs semantic similarity search. Unlike traditional databases that use exact keyword matching, vector databases retrieve documents based on meaning using indexing algorithms such as HNSW or IVFFlat. Popular solutions include pgvector for PostgreSQL applications, Pinecone as a managed cloud service, Qdrant and Weaviate as open-source options, Milvus for massive AI workloads, and Azure AI Search for enterprise applications built on Azure.

---

# ⭐ Senior Engineer Tips

When answering questions about Vector Databases, always explain in this order:

```
Why Vector Databases

↓

Embeddings

↓

Metadata

↓

Indexes

↓

HNSW

↓

pgvector

↓

Cloud Vector Databases

↓

Production Architecture

↓

Trade-offs

↓

Choosing the Right Database
```

Senior interviewers are looking not only for technical knowledge but also for your ability to make the right architectural decisions.

---

# 📌 Key Takeaways

- Vector Databases store embeddings for semantic search.
- They support high-dimensional vector indexing and retrieval.
- Metadata filtering improves accuracy and performance.
- pgvector extends PostgreSQL with vector capabilities.
- HNSW and IVFFlat are the most common indexing algorithms.
- Pinecone is a fully managed cloud Vector Database.
- Qdrant and Weaviate are popular open-source options.
- Milvus is designed for large-scale AI applications.
- Azure AI Search provides integrated vector, semantic, and hybrid search within the Azure ecosystem.
- Choosing the right Vector Database depends on scale, infrastructure, cloud platform, and operational requirements.

---

# 📚 Next Chapter

➡ **Question 7 (Part 4): Chunking Strategies in RAG**

Topics Covered:

- What is Chunking?
- Why Chunking is Required
- Fixed Chunking
- Recursive Chunking
- Semantic Chunking
- Parent-Child Chunking
- Chunk Overlap
- Chunk Size
- Lost in the Middle Problem
- Metadata-Based Chunking
- Production Chunking Strategies
- 50+ Senior-Level Interview Questions
