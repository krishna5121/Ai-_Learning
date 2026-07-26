# 🚀 GenAI Interview Bible 2026
## Volume 2 – LLM Fundamentals

# Question 6 (Part 3)

# Advanced LLM Concepts
## Context Window • KV Cache • Temperature • Top-k • Top-p • Hallucinations • Memory • RAG

> **Difficulty:** ⭐⭐⭐⭐⭐
>
> **Experience Level:** 6+ Years
>
> **Interview Frequency:** ⭐⭐⭐⭐⭐
>
> **Expected Interview Time:** 25–35 Minutes

---

# 📖 Table of Contents

1. Why Interviewers Ask This Question
2. Interview Answer (3–5 Minutes)
3. Context Window
4. KV Cache
5. Temperature
6. Top-k Sampling
7. Top-p Sampling
8. Greedy Decoding
9. Beam Search
10. Hallucinations
11. Why Hallucinations Happen
12. How to Reduce Hallucinations
13. Why LLMs Forget
14. AI Memory
15. Why RAG is Needed
16. Enterprise RAG Pipeline
17. Common Follow-up Questions
18. Common Mistakes
19. Whiteboard Diagram
20. 30-Second Interview Answer
21. Senior Engineer Tips
22. Key Takeaways

---

# 🎯 Why Interviewers Ask This Question

Once you understand Transformer architecture, interviewers move to real-world production topics.

Typical questions include:

- What is a Context Window?
- Why does ChatGPT forget previous messages?
- What is Temperature?
- What is Top-k?
- What is Top-p?
- What is KV Cache?
- Why do LLMs hallucinate?
- How do we reduce hallucinations?
- What is AI Memory?
- Why is RAG required?

These questions test whether you understand how enterprise-grade AI systems behave in production.

---

# ✅ Interview Answer (3–5 Minutes)

> After receiving a prompt, an LLM processes only the tokens available inside its context window. During response generation, it predicts one token at a time based on probability distributions. Parameters such as Temperature, Top-k, and Top-p influence how those tokens are selected. Since the model predicts text rather than verifying facts, it may hallucinate when information is missing or ambiguous. Enterprise applications reduce hallucinations using Retrieval-Augmented Generation (RAG), prompt engineering, guardrails, and high-quality retrieval so that responses are grounded in trusted company data.

---

# 📚 What is a Context Window?

A Context Window is the maximum number of tokens that an LLM can process at one time.

Think of it as the model's temporary working memory.

```
Conversation

↓

Token Count

↓

Fits Inside Context Window?

↓

Yes → Model Uses It

No → Older Tokens Are Removed
```

---

# 👶 Beginner Analogy

Imagine taking an exam.

You are allowed only one notebook.

Everything written inside the notebook is available during the exam.

Anything outside the notebook cannot be used.

The notebook represents the Context Window.

---

# Example

Conversation

```
User:
My name is Krishna.

User:
I live in Delhi.

User:
I work as a GenAI Engineer.

User:
What's my name?
```

If all previous messages are still inside the Context Window:

LLM:

> Krishna

If the first message has already moved outside the Context Window:

LLM:

> I don't know your name.

The model did not permanently forget—it simply cannot access information outside the current context.

---

# Why Context Window Matters

Long conversations create more tokens.

```
Long Conversation

↓

More Tokens

↓

Higher Cost

↓

Higher Latency

↓

Older Messages Removed
```

Enterprise systems therefore summarize conversation history instead of sending every previous message.

---

# Enterprise Solution

Instead of sending hundreds of previous messages:

```
Conversation Summary

+

Recent Messages

↓

LLM
```

Benefits:

- Lower token cost
- Faster responses
- Better context utilization
- Improved scalability

---

# 🚀 What is KV Cache?

KV Cache stands for **Key-Value Cache**.

It stores previously computed attention information during text generation.

---

## Without KV Cache

Imagine generating:

```
Hello
```

Next:

```
Hello World
```

Without caching, the model recomputes attention for **Hello** every time a new token is generated.

```
Hello

↓

Recalculate

↓

Hello World

↓

Recalculate Again
```

This wastes computation.

---

## With KV Cache

```
Hello

↓

Compute Once

↓

Store Key & Value

↓

Generate Next Token

↓

Reuse Previous Computation
```

Benefits:

- Faster inference
- Lower latency
- Reduced GPU usage
- Better streaming performance

---

# 🌡 What is Temperature?

Temperature controls the randomness of generated responses.

It does **NOT** change the model's knowledge.

It changes how confidently the model selects the next token.

---

## Example

Prompt:

```
The sky is
```

Possible probabilities:

```
Blue → 92%

Green → 5%

Purple → 2%

Pizza → 1%
```

---

## Temperature = 0

Always chooses:

```
Blue
```

Characteristics:

- Deterministic
- Stable
- Predictable

---

## Temperature = 0.3

Almost always chooses:

```
Blue
```

Small amount of variation.

---

## Temperature = 0.7

Usually chooses:

```
Blue
```

Occasionally selects another reasonable option.

---

## Temperature = 1.2

Much more randomness.

Useful for:

- Stories
- Creative writing
- Brainstorming

Less suitable for factual applications.

---

# Recommended Temperature

## Low Temperature (0–0.3)

Best for:

- Banking
- Healthcare
- Customer Support
- Legal
- Enterprise Search

Need:

- Consistency
- Accuracy
- Predictability

---

## High Temperature (0.8–1.2)

Best for:

- Story Writing
- Marketing
- Poetry
- Brainstorming
- Entertainment

Need:

- Creativity
- Diversity

---

# Common Misunderstanding

Temperature does NOT:

- Make the model smarter
- Improve reasoning
- Add knowledge

It only changes randomness during token selection.

---

# 🔝 What is Top-k Sampling?

The model predicts many possible next tokens.

Example:

```
Blue → 50%

Red → 20%

Green → 10%

Yellow → 8%

White → 7%

Black → 5%
```

If:

```
Top-k = 3
```

Only these tokens are considered:

```
Blue

Red

Green
```

Everything else is discarded.

---

# 🌊 What is Top-p Sampling?

Instead of selecting a fixed number of tokens,

Top-p selects enough tokens whose cumulative probability reaches **p**.

Example:

```
Blue → 50%

Red → 25%

Green → 15%

Yellow → 5%

Black → 5%
```

If:

```
Top-p = 0.8
```

Selected tokens:

```
Blue

Red

Green
```

Because together they exceed 80%.

---

# Top-k vs Top-p

| Top-k | Top-p |
|--------|--------|
| Fixed number of tokens | Dynamic number of tokens |
| Simpler | More adaptive |
| Always selects K tokens | Selects tokens until probability threshold is reached |
| Less flexible | Preferred in modern LLM APIs |

---

# 🎯 What is Greedy Decoding?

Greedy Decoding always chooses the token with the highest probability.

Example:

```
Blue → 90%

Green → 5%

Red → 5%
```

Output:

```
Blue
```

Advantages:

- Fast
- Deterministic

Disadvantages:

- Repetitive
- Less creative

---

# 🌉 What is Beam Search?

Beam Search explores multiple candidate sentences simultaneously.

Instead of only:

```
The sky is blue.
```

It also evaluates:

```
The sky looks blue.

The sky appears blue.

The sky seems blue.
```

Finally, it selects the highest-scoring complete sentence.

Used in:

- Translation
- Summarization
- Speech Recognition

---

# 🤔 What is Hallucination?

Hallucination occurs when an LLM confidently generates information that is incorrect or unsupported.

Example:

User:

```
What is the warranty period?
```

Available documents:

```
No warranty information available.
```

LLM:

```
The warranty period is five years.
```

The answer sounds convincing but is completely fabricated.

---

# Why Do Hallucinations Happen?

### 1. Missing Context

The required information is unavailable.

---

### 2. Ambiguous Prompt

The question is unclear.

---

### 3. Outdated Knowledge

The model was trained before newer information existed.

---

### 4. Poor Retrieval

The RAG system retrieved irrelevant documents.

---

### 5. Probability-Based Generation

LLMs predict the most likely next token.

They do not verify facts.

---

# 🛡 How Do We Reduce Hallucinations?

Enterprise systems combine multiple techniques.

---

## Retrieval-Augmented Generation (RAG)

Retrieve trusted company documents before asking the LLM to answer.

---

## Better Prompt Engineering

Example:

```
Answer only using the provided context.

If the answer is unavailable,

reply:

"I don't know."
```

---

## Guardrails

Validate responses before returning them.

Examples:

- Sensitive data detection
- Policy enforcement
- Unsupported claim detection
- Compliance checks

---

## Better Retrieval

Improve:

- Chunking
- Metadata
- Hybrid Search
- Re-ranking
- Embeddings

---

## Human Review

Critical domains often require:

```
LLM

↓

Human Approval

↓

Final Response
```

---

# Can Hallucinations Be Eliminated?

No.

They can be greatly reduced,

but never completely eliminated.

---

# 🧠 Why Do LLMs Forget?

Conversation:

```
Message 1

↓

Message 2

↓

...

↓

Message 300
```

Eventually,

older messages leave the Context Window.

The model cannot access them.

This is not permanent forgetting.

It is simply a Context Window limitation.

---

# 🧠 What is Memory in AI Agents?

Production AI systems usually implement multiple memory types.

---

## Short-Term Memory

Current conversation.

Stored inside the Context Window.

---

## Long-Term Memory

Stored externally.

Examples:

- PostgreSQL
- Redis
- Vector Database

Retrieved when needed.

---

## Episodic Memory

Stores previous user interactions.

Example:

```
User prefers vegetarian food.
```

Can be retrieved in future conversations.

---

## Semantic Memory

Stores domain knowledge.

Examples:

- Product Manuals
- Company Policies
- FAQs

Usually implemented through RAG.

---

# 📚 Why Do We Need RAG?

Suppose your company launches a new product yesterday.

The LLM was trained six months ago.

Without RAG:

```
User

↓

LLM

↓

Outdated Answer
```

With RAG:

```
User

↓

Embedding

↓

Vector Search

↓

Relevant Documents

↓

Prompt Builder

↓

LLM

↓

Grounded Response
```

The LLM answers using the latest company documents.

---

# 🏢 Enterprise RAG Pipeline

```
User Question

↓

Authentication

↓

Conversation History

↓

Query Rewriting

↓

Embedding Generation

↓

Hybrid Search

↓

Vector Search

↓

Keyword Search

↓

Re-ranking

↓

Top-k Selection

↓

Prompt Builder

↓

LLM

↓

Guardrails

↓

Streaming Response
```

This is the architecture commonly discussed in senior GenAI interviews.

---

# 💬 Common Follow-up Questions

### Does Temperature improve intelligence?

No.

It only changes randomness.

---

### Does Top-k improve accuracy?

Not directly.

It controls which candidate tokens are eligible for selection.

---

### Why do enterprise chatbots use low Temperature?

To generate consistent and reliable responses.

---

### Why do hallucinations happen?

Because LLMs predict likely text rather than verifying facts.

---

### Can RAG completely eliminate hallucinations?

No.

It reduces hallucinations significantly, but retrieval quality still matters.

---

### Why is KV Cache important?

It avoids recomputing attention for previously generated tokens, reducing latency during inference.

---

# ❌ Common Mistakes

❌ Temperature increases intelligence.

✔ Temperature only changes randomness.

---

❌ Hallucinations are software bugs.

✔ Hallucinations are an inherent limitation of probabilistic language models.

---

❌ RAG stores knowledge inside the LLM.

✔ RAG retrieves external knowledge at runtime.

---

# 🖊 Whiteboard Diagram

```
                User Prompt
                     │
                     ▼
             Context Window
                     │
                     ▼
       Temperature / Top-k / Top-p
                     │
                     ▼
          Next Token Prediction
                     │
                     ▼
            Generated Response
────────────────────────────────────
           Enterprise Layer
────────────────────────────────────
                     │
                     ▼
            Query Rewriting
                     │
                     ▼
          Embedding Generation
                     │
                     ▼
            Hybrid Retrieval
                     │
                     ▼
              Re-ranking
                     │
                     ▼
             Prompt Builder
                     │
                     ▼
                  LLM
                     │
                     ▼
              Guardrails
                     │
                     ▼
            Final Response
```

---

# ⚡ 30-Second Interview Answer

> An LLM generates responses using only the information available within its Context Window and predicts one token at a time. Parameters such as Temperature, Top-k, and Top-p influence how those tokens are selected. Since LLMs predict probabilities rather than verify facts, they can hallucinate. Enterprise applications reduce hallucinations using RAG, better retrieval, prompt engineering, and guardrails to ensure responses are grounded in trusted company data.

---

# ⭐ Senior Engineer Tips

Answer advanced LLM questions in this order:

```
Context Window

↓

KV Cache

↓

Temperature

↓

Top-k

↓

Top-p

↓

Greedy Decoding

↓

Beam Search

↓

Hallucinations

↓

Memory

↓

RAG

↓

Enterprise Architecture
```

This mirrors the actual lifecycle of production GenAI systems and demonstrates both theoretical understanding and practical engineering knowledge.

---

# 📌 Key Takeaways

- Context Window is the LLM's temporary working memory.
- KV Cache speeds up inference by reusing previous attention computations.
- Temperature controls randomness, not intelligence.
- Top-k selects a fixed number of candidate tokens.
- Top-p selects tokens based on cumulative probability.
- Greedy Decoding is deterministic, while Beam Search explores multiple sequences.
- Hallucinations occur because LLMs predict probabilities rather than verify facts.
- RAG grounds responses in external knowledge to reduce hallucinations.
- Enterprise AI systems combine RAG, guardrails, prompt engineering, and monitoring for reliable production deployments.

---

# 📚 Next Chapter

➡ **Question 6 (Part 4) – Enterprise LLM Architecture**

Topics Covered:

- Complete End-to-End LLM Request Lifecycle
- Streaming Responses
- Prompt Templates
- System vs User vs Assistant Prompts
- Function Calling / Tool Calling
- AI Agents vs LLMs
- Observability & Monitoring
- LLM Evaluation Metrics
- Cost Optimization
- Production Deployment
- Senior-Level Architecture Questions
- Whiteboard Interview Scenarios
```
