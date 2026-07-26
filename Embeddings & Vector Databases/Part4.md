# 🚀 GenAI Interview Bible 2026
## Volume 3 – Embeddings & Vector Databases

# Question 7 (Part 4)

# Chunking in RAG
## Complete Beginner to Production Guide

> **Difficulty:** ⭐⭐⭐⭐⭐
>
> **Experience Level:** 6+ Years
>
> **Interview Frequency:** ⭐⭐⭐⭐⭐
>
> **Category:** RAG / Chunking / Embeddings / Retrieval / Production AI

---

# 📖 Table of Contents

1. Why Interviewers Ask About Chunking
2. 3-Minute Interview Answer
3. What is Chunking?
4. Why Chunking is Required
5. Chunking Pipeline
6. Characteristics of a Good Chunk
7. Types of Chunking
8. Fixed Chunking
9. Recursive Chunking
10. Semantic Chunking
11. Parent-Child Chunking
12. Document-Based Chunking
13. Metadata-Based Chunking
14. Chunk Size
15. Chunk Overlap
16. Lost in the Middle Problem
17. Production Chunking Pipeline
18. Common Interview Questions
19. Common Mistakes
20. Whiteboard Architecture
21. 30-Second Interview Answer
22. Senior Engineer Tips
23. Best Practices
24. Key Takeaways

---

# 🎯 Why Interviewers Ask This Question

Every Retrieval-Augmented Generation (RAG) application depends on chunking.

Even if you have:

- Best LLM
- Best Embedding Model
- Best Vector Database

Your system will still perform poorly if your chunking strategy is incorrect.

Interviewers ask this question to evaluate whether you understand how documents are prepared before they are stored in a vector database.

---

# ✅ 3-Minute Interview Answer

> Chunking is the process of dividing large documents into smaller, meaningful pieces before generating embeddings. Since LLMs and embedding models have context size limits, entire documents cannot be embedded or retrieved efficiently. Each chunk gets its own embedding and is stored independently in the vector database. During retrieval, only the most relevant chunks are returned. A good chunking strategy improves retrieval accuracy, reduces hallucinations, lowers token costs, and produces better answers.

---

# 📚 What is Chunking?

Imagine you have a document with **500 pages**.

```
Employee Handbook

↓

500 Pages
```

Can we create a single embedding?

Technically yes.

Should we?

**No.**

Instead, we divide the document into many smaller chunks.

Each chunk receives its own embedding.

---

# Why Do We Need Chunking?

Suppose the user asks:

```
What is the maternity leave policy?
```

If the entire handbook is stored as one embedding, the retrieved content might include:

- Company Introduction
- CEO Message
- Payroll Policy
- Travel Policy
- Leave Policy
- Security Guidelines

Most of this information is irrelevant.

Instead:

```
Employee Handbook

↓

Introduction

↓

Chunk 1

--------------------

Leave Policy

↓

Chunk 2

--------------------

Travel Policy

↓

Chunk 3
```

Now only the Leave Policy chunk is retrieved.

---

# Definition

Chunking is the process of splitting a large document into smaller logical units before generating embeddings.

Each chunk becomes:

- Searchable
- Independent
- Embeddable
- Retrievable

---

# Chunking Pipeline

```
PDF

↓

Text Extraction

↓

Cleaning

↓

Chunking

↓

Chunk 1

Chunk 2

Chunk 3

↓

Embedding Model

↓

Vector Database
```

---

# Why Not Store the Entire PDF?

Suppose a document has:

```
1000 Pages
```

Problems with one embedding:

❌ Very large context

❌ Poor retrieval

❌ Higher latency

❌ Higher token cost

❌ Irrelevant information

Instead:

```
Large Document

↓

Split into Chunks

↓

Store Individual Embeddings
```

---

# Characteristics of a Good Chunk

A good chunk should:

✅ Represent one idea

✅ Preserve complete context

✅ Be understandable independently

✅ Stay within embedding model limits

---

### Good Example

```
FastAPI supports dependency injection.

Dependency injection separates business logic from request handling.
```

---

### Bad Example

```
FastAPI supports

--------------------

dependency injection

--------------------

separates business
```

The meaning is lost.

---

# Types of Chunking

There are several chunking strategies.

Each is suitable for different scenarios.

---

# 1. Fixed Chunking

The simplest strategy.

Split after a fixed number of tokens.

Example:

```
1000 Tokens

↓

Chunk 1

↓

1000 Tokens

↓

Chunk 2

↓

1000 Tokens

↓

Chunk 3
```

Advantages:

- Easy
- Fast
- Simple

Disadvantages:

- Breaks sentences
- Breaks paragraphs
- Poor retrieval quality

---

### Example

Original:

```
FastAPI is a modern Python framework.

It supports asynchronous programming.

It automatically generates API documentation.
```

Fixed Chunk:

```
FastAPI is a modern Python

framework. It supports

asynchronous programming...
```

Meaning becomes fragmented.

---

# 2. Recursive Chunking ⭐⭐⭐⭐⭐

Most production systems use Recursive Chunking.

Instead of splitting randomly, it respects document structure.

Priority:

```
Paragraph

↓

Sentence

↓

Comma

↓

Word

↓

Character
```

Only when a paragraph exceeds the limit does it split into sentences.

If needed, it continues splitting into words.

---

### Example

Original:

```
Paragraph

↓

Sentence 1

Sentence 2

Sentence 3
```

Recursive Chunking:

```
Chunk 1

Sentence 1

Sentence 2

-------------------

Chunk 2

Sentence 3
```

Context remains intact.

---

# Why Recursive Chunking is Better

Benefits:

- Preserves meaning
- Better embeddings
- Better retrieval
- Lower hallucinations
- Better context for the LLM

---

# 3. Semantic Chunking ⭐⭐⭐⭐⭐

Semantic Chunking groups content by meaning rather than size.

Example document:

```
Introduction

Architecture

Deployment

Monitoring

Security
```

Semantic Chunking produces:

```
Chunk 1

Introduction

----------------

Chunk 2

Architecture

----------------

Chunk 3

Deployment
```

Each chunk contains one topic.

---

# Advantages

- High retrieval quality
- Better semantic understanding
- More accurate embeddings

Disadvantages:

- Slower
- More computationally expensive
- Requires additional NLP processing

---

# 4. Parent-Child Chunking ⭐⭐⭐⭐⭐

Very popular in enterprise RAG systems.

Idea:

Store:

Small chunks

Retrieve:

Large parent sections

Example:

```
Book

↓

Chapter

↓

Section

↓

Paragraph
```

Store embeddings for paragraphs.

When one paragraph matches,

retrieve the entire section.

---

### Example

Stored:

```
Annual Leave

Paragraph 1

Paragraph 2

Paragraph 3
```

Similarity Search returns:

```
Paragraph 2
```

System sends:

```
Entire Leave Policy Section
```

to the LLM.

This provides richer context.

---

# Why Parent-Child Chunking?

Without parent retrieval:

The LLM receives only one small paragraph.

Important surrounding information is lost.

Parent retrieval solves this problem.

---

# 5. Document-Based Chunking

Split using document structure.

Example:

```
Heading

↓

Subheading

↓

Paragraph
```

Every heading becomes a chunk.

Best suited for:

- Documentation
- User Manuals
- Books
- Standard Operating Procedures

---

# 6. Metadata-Based Chunking

Every chunk stores metadata.

Example:

```
Chunk

↓

Department = HR

Country = India

Version = 2026

Language = English
```

Before similarity search:

Metadata filters remove irrelevant chunks.

This improves:

- Accuracy
- Speed
- Security

---

# Chunk Size

One of the most common interview questions.

There is **no universal perfect chunk size**.

It depends on:

- Document Type
- Embedding Model
- LLM Context Window
- Retrieval Strategy

---

### Typical Production Values

| Content | Chunk Size |
|-----------|------------|
| FAQ | 200–400 Tokens |
| Product Documentation | 400–800 Tokens |
| Technical Manuals | 600–1000 Tokens |
| Books | 800–1200 Tokens |

---

# Chunk Overlap ⭐⭐⭐⭐⭐

Suppose Chunk 1 ends with:

```
Dependency Injection
```

Chunk 2 begins with:

```
improves testing.
```

The sentence is broken.

Chunk overlap solves this.

Example:

```
Chunk 1

Sentence A

Sentence B

Sentence C

--------------------

Chunk 2

Sentence C

Sentence D

Sentence E
```

Sentence C exists in both chunks.

---

# Why Use Chunk Overlap?

Benefits:

- Preserves context
- Prevents broken sentences
- Improves retrieval
- Better LLM responses

Typical overlap:

- 10%–20%

or

- 50–150 Tokens

depending on chunk size.

---

# Lost in the Middle Problem ⭐⭐⭐⭐⭐

Suppose the LLM receives:

```
Chunk A

Chunk B

Chunk C

Chunk D

Chunk E
```

Research shows that LLMs often focus more on:

- Beginning
- End

while paying less attention to the middle.

This is called:

**Lost in the Middle**

---

# Solutions

Production systems use:

- Better Chunking
- Smaller Chunks
- Re-ranking
- Parent Retrieval
- Context Compression

to reduce this problem.

---

# Production Chunking Pipeline

```
PDF

↓

OCR

↓

Text Cleaning

↓

Heading Detection

↓

Recursive Chunking

↓

Chunk Overlap

↓

Metadata

↓

Embedding Model

↓

Vector Database
```

---

# Common Interview Questions

### Why not store one embedding for the whole PDF?

Because retrieval becomes inaccurate and token usage becomes extremely high.

---

### Why not create very small chunks?

Very small chunks lose context.

Example:

```
supports dependency injection
```

Without surrounding sentences, the meaning is incomplete.

---

### Why not create huge chunks?

Large chunks:

- Increase token cost
- Contain irrelevant information
- Reduce retrieval precision

---

### Which chunking strategy is best?

There is no single best strategy.

Most production RAG systems use:

✅ Recursive Chunking + Overlap

Enterprise systems often combine:

- Recursive Chunking
- Parent-Child Retrieval
- Semantic Chunking

---

### Does chunking affect hallucinations?

Yes.

Poor chunking leads to poor retrieval.

Poor retrieval leads to hallucinations.

---

### Can one document generate hundreds of chunks?

Yes.

Large documents often generate hundreds or even thousands of chunks.

---

# ❌ Common Mistakes

### Mistake 1

❌ Bigger chunks always improve accuracy.

✔ Bigger chunks often contain unnecessary information.

---

### Mistake 2

❌ Smaller chunks are always better.

✔ Very small chunks lose context.

---

### Mistake 3

❌ Chunk overlap only duplicates data.

✔ Controlled overlap preserves context and improves retrieval quality.

---

# 🏗 Whiteboard Architecture

```
Large PDF

↓

OCR

↓

Cleaning

↓

Recursive Chunking

↓

Chunk Overlap

↓

Metadata

↓

Embedding Model

↓

Vector Database

↓

Similarity Search

↓

Top-K Chunks

↓

Prompt Builder

↓

LLM

↓

Final Answer
```

---

# ⚡ 30-Second Interview Answer

> Chunking is the process of dividing large documents into smaller, meaningful units before generating embeddings. Since embedding models and LLMs have context limits, documents are split into chunks that can be indexed and searched efficiently. Production systems commonly use Recursive Chunking with overlap because it preserves context and improves retrieval quality. Advanced systems may also use Semantic Chunking or Parent-Child Chunking depending on the document type and business requirements.

---

# ⭐ Senior Engineer Tips

When asked **"How do you design chunking for a production RAG system?"**, explain in this order:

```
Why Chunking

↓

Chunking Pipeline

↓

Fixed Chunking

↓

Recursive Chunking

↓

Semantic Chunking

↓

Parent-Child Chunking

↓

Chunk Size

↓

Chunk Overlap

↓

Metadata

↓

Production Best Practices
```

This sequence demonstrates architectural thinking expected from a Senior GenAI Engineer.

---

# 📌 Production Best Practices

✅ Clean extracted text before chunking.

✅ Preserve document structure (headings, paragraphs, tables).

✅ Use Recursive Chunking as the default strategy.

✅ Apply 10–20% overlap to maintain context.

✅ Store metadata with every chunk.

✅ Tune chunk size based on document type.

✅ Re-rank retrieved chunks before sending them to the LLM.

✅ Continuously evaluate retrieval quality using real user queries.

---

# 🎯 Key Takeaways

- Chunking divides large documents into meaningful pieces.
- Every chunk receives its own embedding.
- Good chunking directly improves retrieval quality.
- Recursive Chunking is the most common production strategy.
- Semantic Chunking groups information by meaning.
- Parent-Child Chunking improves context for enterprise RAG.
- Chunk Overlap preserves context across chunk boundaries.
- Metadata improves filtering and retrieval accuracy.
- Poor chunking increases hallucinations.
- Production RAG systems combine multiple chunking strategies depending on document type and business needs.

---

# 📚 Next Chapter

## Question 7 (Part 5): Advanced Retrieval Techniques

Topics Covered:

- Hybrid Search
- BM25
- Keyword Search
- Metadata Filtering
- Re-ranking
- Cross Encoder
- Query Rewriting
- Multi-Query Retrieval
- Context Compression
- Top-K Optimization
- Azure AI Search Hybrid Retrieval
- Enterprise Retrieval Pipeline
- Production Best Practices
