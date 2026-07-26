# 🚀 GenAI Interview Bible 2026
# Volume 6 – RAG Fundamentals

# Question 11

# What is Chunking in RAG? (Production Level)
## Complete Beginner to Senior Guide

> **Difficulty:** ⭐⭐⭐⭐⭐
>
> **Experience Level:** 6+ Years
>
> **Interview Frequency:** ⭐⭐⭐⭐⭐
>
> **Category:** RAG / Vector Database / Information Retrieval

---

# 📖 Table of Contents

1. Why Interviewers Ask This Question
2. What is Chunking?
3. Why Do We Need Chunking?
4. What Happens Without Chunking?
5. How Chunking Works
6. Chunking Pipeline
7. Types of Chunking
8. Fixed Size Chunking
9. Recursive Chunking
10. Semantic Chunking
11. Document Aware Chunking
12. Parent Child Chunking
13. Sliding Window Chunking
14. Chunk Overlap
15. Chunk Size Selection
16. Metadata in Chunking
17. Production Chunking Pipeline
18. Real Production Example
19. Common Interview Questions
20. Whiteboard Architecture
21. 30-Second Interview Answer
22. Senior Engineer Tips
23. Production Best Practices
24. Key Takeaways

---

# 🎯 Why Interviewers Ask This Question

Chunking is one of the **most important topics in RAG**.

Many beginners know:

```
Document

↓

Embedding

↓

Vector DB
```

But they don't know **why we split documents before creating embeddings.**

A senior GenAI engineer should understand:

- Why chunking is required
- Different chunking strategies
- When to use each strategy
- Production best practices
- Common mistakes

---

# 📚 What is Chunking?

Chunking means **dividing a large document into smaller meaningful pieces before creating embeddings.**

Simple Definition

> Chunking is the process of splitting a large document into smaller sections so that each section can be embedded, stored, retrieved, and understood efficiently.

---

# Real Life Analogy

Imagine a 600-page book.

Question

```
Where is Newton's First Law explained?
```

Would you hand over the entire 600-page book?

No.

You would open the chapter related to Physics.

That chapter is like a chunk.

Instead of reading everything,

you retrieve only the relevant part.

---

# Why Do We Need Chunking?

Suppose you have a PDF.

```
Company Policy

800 Pages
```

Can we send all 800 pages to an LLM?

No.

Problems:

- Token limit exceeded
- Higher cost
- Slower response
- More hallucinations
- Poor retrieval accuracy

Chunking solves all these problems.

---

# What Happens Without Chunking?

Suppose a document contains:

```
Employee Handbook

500 Pages
```

User asks:

```
How many leaves can employees take?
```

Without chunking

```
Entire PDF

↓

Embedding

↓

Vector Search
```

Problems

- Huge embedding
- Poor semantic representation
- Slow search
- Irrelevant retrieval

---

# With Chunking

```
500 Pages

↓

Split into

300 Chunks

↓

300 Embeddings

↓

Vector Database
```

Now,

only the relevant chunk is retrieved.

This improves speed and accuracy.

---

# High-Level Chunking Pipeline

```
PDF

↓

Text Extraction

↓

Cleaning

↓

Chunking

↓

Embedding

↓

Vector Database
```

Every production RAG system follows a pipeline similar to this.

---

# Example

Document

```
Python Guide

Page 1

Introduction

...

Page 80

Functions

...

Page 200

Decorators

...

Page 500

Async Programming
```

Chunking creates:

```
Chunk 1

Introduction
```

```
Chunk 2

Variables
```

```
Chunk 3

Functions
```

```
Chunk 4

Decorators
```

```
Chunk 5

Async Programming
```

Each chunk gets its own embedding.

---

# Why Smaller Chunks Work Better

Suppose a chunk contains only:

```
Python Decorators
```

Embedding becomes highly focused.

If it also contains:

- SQL
- Docker
- Kubernetes
- Azure
- React

the embedding becomes less specific.

Smaller, coherent chunks improve semantic retrieval.

---

# Types of Chunking

There is no single best strategy.

Common approaches include:

- Fixed Size Chunking
- Recursive Chunking
- Semantic Chunking
- Document Aware Chunking
- Parent Child Chunking
- Sliding Window Chunking

Let's understand each.

---

# 1. Fixed Size Chunking

The simplest approach.

Split after a fixed number of tokens or characters.

Example

```
Document

↓

500 Tokens

↓

Chunk 1
```

```
Next 500 Tokens

↓

Chunk 2
```

Advantages

- Simple
- Fast
- Easy to implement

Disadvantages

- May split sentences
- May lose context

---

# Example

```
Machine learning is becoming increasingly important because...
```

If the split happens here,

the sentence becomes incomplete.

This hurts retrieval quality.

---

# 2. Recursive Chunking

One of the most popular production approaches.

Instead of splitting blindly,

the system tries natural boundaries.

Typical order:

```
Paragraph

↓

Sentence

↓

Line

↓

Word
```

It first attempts to split by paragraph.

If the paragraph is too large,

it splits by sentence.

If still too large,

it splits by smaller units.

This preserves readability.

---

# Example

Instead of

```
Paragraph ends in the middle...
```

Recursive chunking keeps complete paragraphs whenever possible.

Much better semantic quality.

---

# 3. Semantic Chunking

One of the smartest chunking methods.

Instead of splitting by size,

it splits based on **meaning**.

Example

Document

```
Introduction

↓

Python Basics

↓

Functions

↓

Decorators

↓

Async

↓

Conclusion
```

Semantic chunking creates chunks around topic changes.

Benefits

- Better retrieval
- Better embeddings
- Higher answer quality

Trade-off

- More computationally expensive

---

# Example

Wrong Chunk

```
Python Variables

+

Kubernetes Pods

+

Azure Storage
```

Correct Semantic Chunk

```
Python Variables
```

Next Chunk

```
Python Functions
```

Each chunk discusses one topic.

---

# 4. Document Aware Chunking

Some documents have structure.

Example

```
Title

↓

Heading

↓

Subheading

↓

Paragraph

↓

Table
```

Instead of ignoring structure,

the chunker preserves it.

Example

```
Chapter 3

↓

Networking

↓

VPC

↓

Subnets
```

The hierarchy is retained.

Very common for PDFs and technical documentation.

---

# 5. Parent Child Chunking

A production technique used by many enterprise RAG systems.

Parent Chunk

```
Complete Chapter
```

Child Chunks

```
Topic 1

Topic 2

Topic 3
```

Search happens on child chunks.

When a child is selected,

the parent is also retrieved.

Benefits

- Better context
- More complete answers
- Lower hallucination

---

# Example

Parent

```
Docker Guide
```

Children

```
Containers
```

```
Volumes
```

```
Networking
```

User asks

```
Explain Docker Networking
```

System retrieves:

Child

```
Networking
```

Plus Parent

```
Docker Guide
```

Now the LLM receives detailed context.

---

# 6. Sliding Window Chunking

A very common interview topic.

Instead of creating completely separate chunks,

adjacent chunks overlap.

Example

```
Chunk 1

1-500 Tokens
```

```
Chunk 2

450-950 Tokens
```

Notice

```
450-500
```

appears in both chunks.

This overlap preserves context.

---

# Why Overlap is Important

Suppose a sentence starts here:

```
Token 480
```

and ends here:

```
Token 520
```

Without overlap,

the sentence gets split.

With overlap,

the sentence appears in both chunks.

This significantly improves retrieval quality.

---

# Chunk Overlap

Typical overlap values

```
50 Tokens

100 Tokens

150 Tokens
```

Common production values depend on:

- Document type
- Average paragraph length
- Embedding model
- LLM context window

Too much overlap wastes storage.

Too little overlap loses context.

---

# Choosing Chunk Size

There is **no universal chunk size**.

It depends on:

- Document type
- LLM context window
- Embedding model
- Use case

Examples

Technical Documentation

```
400–800 Tokens
```

FAQ

```
100–300 Tokens
```

Legal Documents

```
700–1200 Tokens
```

Research Papers

```
600–1000 Tokens
```

---

# Why Not Create Very Large Chunks?

Example

```
5000 Tokens
```

Problems

- Weak embeddings
- Multiple unrelated topics
- Lower retrieval precision
- Higher token cost

---

# Why Not Create Very Small Chunks?

Example

```
20 Tokens
```

Problems

- Missing context
- Incomplete answers
- Too many vectors
- Increased storage

Finding the right balance is important.

---

# Metadata in Chunking

Each chunk usually stores metadata.

Example

```json
{
  "document": "Python Guide",
  "chapter": "Decorators",
  "page": 142,
  "chunk_id": 87,
  "author": "John",
  "version": "v2"
}
```

Metadata enables filtering.

Example

```
Retrieve only

Version = v2

Department = HR

Language = English
```

---

# Production Chunking Pipeline

```
PDF

↓

OCR (if needed)

↓

Text Extraction

↓

Cleaning

↓

Remove Headers/Footers

↓

Chunking

↓

Metadata Generation

↓

Embedding Model

↓

Vector Database
```

---

# Real Production Example

Suppose a company has:

```
Employee Handbook

250 Pages
```

Pipeline

```
PDF

↓

Extract Text

↓

Split by Headings

↓

Recursive Chunking

↓

Chunk Size = 600 Tokens

↓

Overlap = 100 Tokens

↓

Generate Embeddings

↓

Store in pgvector
```

User asks

```
How many maternity leaves are allowed?
```

System

```
Question

↓

Embedding

↓

Similarity Search

↓

Retrieve HR Leave Chunk

↓

LLM

↓

Answer
```

Instead of searching the entire handbook,

only the relevant chunk is used.

---

# Common Interview Questions

## What is Chunking?

Chunking is the process of splitting a large document into smaller meaningful pieces before generating embeddings.

---

## Why is Chunking Needed?

Because LLMs and embedding models have token limits, and smaller chunks improve retrieval accuracy and reduce cost.

---

## Which Chunking Strategy is Most Common?

Recursive Chunking is one of the most commonly used production strategies because it preserves natural document boundaries.

---

## What is Semantic Chunking?

Semantic Chunking splits documents based on topic changes rather than fixed size.

---

## What is Chunk Overlap?

Chunk overlap means repeating a small portion of text between adjacent chunks to preserve context.

---

## What Happens if Chunk Size is Too Large?

The embedding becomes less focused, retrieval quality decreases, and token costs increase.

---

## What Happens if Chunk Size is Too Small?

Important context may be lost, resulting in incomplete retrieval and weaker LLM responses.

---

## Why Store Metadata?

Metadata enables filtering, versioning, access control, and better retrieval.

---

# Whiteboard Architecture

```
Document

↓

Extract Text

↓

Clean

↓

Chunking

↓

Chunk Metadata

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

Final Response
```

---

# ⚡ 30-Second Interview Answer

> Chunking is the process of splitting large documents into smaller meaningful sections before generating embeddings. This improves semantic retrieval, reduces token usage, lowers cost, and helps the LLM receive only the most relevant context. Common strategies include Fixed Size, Recursive, Semantic, Document Aware, Parent-Child, and Sliding Window Chunking. In production systems, Recursive Chunking with appropriate chunk overlap is a popular choice because it preserves document structure while maintaining retrieval quality.

---

# ⭐ Senior Engineer Tips

In interviews, explain chunking using this flow:

```
Document

↓

Text Extraction

↓

Cleaning

↓

Chunking

↓

Metadata

↓

Embeddings

↓

Vector Database

↓

Similarity Search

↓

LLM
```

Then explain:

1. Why chunking is necessary.
2. Why one embedding for an entire document is a bad idea.
3. Different chunking strategies.
4. Why overlap improves context.
5. How metadata improves retrieval.
6. Which strategy you would choose for production and why.

---

# 📌 Production Best Practices

✅ Prefer Recursive Chunking for most document-based RAG systems.

✅ Use Semantic Chunking when topic boundaries are important.

✅ Add chunk overlap (commonly 50–150 tokens) to preserve context.

✅ Remove headers, footers, and repeated page numbers before chunking.

✅ Store rich metadata with every chunk.

✅ Keep document versions synchronized with embeddings.

✅ Test different chunk sizes using retrieval metrics rather than guessing.

---

# 🎯 Key Takeaways

- Chunking splits large documents into smaller meaningful sections.
- It improves retrieval accuracy and reduces LLM cost.
- Fixed Size Chunking is simple but may break context.
- Recursive Chunking preserves natural boundaries and is widely used.
- Semantic Chunking groups information by meaning.
- Parent-Child Chunking provides both precision and context.
- Sliding Window Chunking uses overlap to avoid losing information at boundaries.
- Metadata is essential for filtering and enterprise-scale RAG.
- The best chunking strategy depends on the document type and use case.

---

# 📚 Next Chapter

## Question 12 – What are Vector Databases?

Topics Covered:

- What is a Vector Database?
- Why Not Use SQL?
- How Vectors Are Stored
- Indexing (HNSW, IVF, Flat)
- Similarity Search
- Metadata Filtering
- pgvector vs Pinecone vs Qdrant vs Milvus vs Azure AI Search
- Production Architecture
- Scaling Vector Databases
- Enterprise Best Practices
