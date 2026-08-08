# GenAI Engineer – Machine Learning Interview Preparation

## 📌 Overview

This repository contains **Machine Learning interview questions for a 6+ years experienced GenAI Engineer**.

The focus is not on becoming a traditional Machine Learning Researcher. Instead, the questions are designed around the ML concepts that are most relevant to modern **Generative AI, LLM, RAG, Embeddings, Fine-Tuning, Retrieval, Evaluation, and Production AI systems**.

The goal is to prepare for interviews for roles such as:

* Senior GenAI Engineer
* GenAI Developer
* AI Engineer
* Senior AI Engineer
* GenAI Architect
* LLM Engineer
* Applied AI Engineer

---

# 🎯 Target Experience

**6+ Years Software Engineering / GenAI Experience**

The preparation focuses on the level expected from a senior engineer who can:

* Understand ML fundamentals
* Build LLM applications
* Design production RAG systems
* Understand embeddings and vector search
* Evaluate AI systems
* Understand fine-tuning
* Debug retrieval and generation problems
* Make ML/GenAI architecture decisions
* Explain technical decisions during interviews

---

# 📚 Table of Contents

1. [Machine Learning Fundamentals](#1-machine-learning-fundamentals)
2. [ML Algorithms](#2-ml-algorithms)
3. [ML Evaluation](#3-ml-evaluation)
4. [Deep Learning](#4-deep-learning)
5. [NLP Fundamentals](#5-nlp-fundamentals)
6. [Transformers](#6-transformers)
7. [LLM Fundamentals](#7-llm-fundamentals)
8. [RAG and Retrieval](#8-rag-and-retrieval)
9. [Fine-Tuning](#9-fine-tuning)
10. [Production GenAI and ML](#10-production-genai-and-ml)
11. [Scenario-Based Questions](#11-scenario-based-questions)
12. [Interview Priority](#12-interview-priority)
13. [Preparation Strategy](#13-preparation-strategy)

---

# 1. Machine Learning Fundamentals

## Questions

1. What is Machine Learning?
2. What is the difference between supervised, unsupervised, and reinforcement learning?
3. What is the difference between classification and regression?
4. What is overfitting?
5. How do you prevent overfitting?
6. What is underfitting?
7. What is the bias-variance tradeoff?
8. What is training data?
9. What is validation data?
10. What is test data?
11. Why do we need a validation set?
12. What is cross-validation?
13. What is data leakage?
14. What is feature engineering?
15. What is feature selection?
16. Normalization vs standardization?
17. What is an outlier?
18. What is dimensionality reduction?
19. What is PCA?
20. What is regularization?
21. L1 vs L2 regularization?
22. What is a loss function?
23. What is gradient descent?

---

# 2. ML Algorithms

## Questions

24. How does Linear Regression work?
25. How does Logistic Regression work?
26. Linear Regression vs Logistic Regression?
27. How does a Decision Tree work?
28. What is Random Forest?
29. What is ensemble learning?
30. What is Bagging?
31. What is Boosting?
32. Random Forest vs Gradient Boosting?
33. What is XGBoost?
34. What is SVM?
35. What is K-Means clustering?
36. What is hierarchical clustering?
37. What is DBSCAN?
38. What is Naive Bayes?
39. When would you choose a traditional ML model?
40. How do you select an ML algorithm?
41. How do you handle imbalanced datasets?
42. What is SMOTE?
43. What is class weighting?

---

# 3. ML Evaluation

## Questions

44. What is accuracy?
45. What is precision?
46. What is recall?
47. What is F1-score?
48. Precision vs recall?
49. What is a confusion matrix?
50. What is ROC-AUC?
51. What is PR-AUC?
52. What is MSE?
53. What is MAE?
54. How do you choose an evaluation metric?
55. Why can accuracy be misleading?
56. How do you evaluate an ML model?
57. What is model drift?
58. What is data drift?
59. What is concept drift?
60. How do you monitor an ML model in production?

---

# 4. Deep Learning

## Questions

61. What is Deep Learning?
62. What is a neural network?
63. What is a neuron?
64. What are weights and biases?
65. What is an activation function?
66. ReLU vs Sigmoid vs Tanh?
67. What is forward propagation?
68. What is backpropagation?
69. What is a gradient?
70. What is vanishing gradient?
71. What is exploding gradient?
72. What is batch size?
73. What is an epoch?
74. What is learning rate?
75. What happens if learning rate is too high?
76. What happens if learning rate is too low?
77. What is an optimizer?
78. SGD vs Adam?
79. What is dropout?
80. What is batch normalization?
81. What is transfer learning?
82. What is fine-tuning?
83. What is inference?

---

# 5. NLP Fundamentals

## Questions

84. What is NLP?
85. What is tokenization?
86. What is stemming?
87. What is lemmatization?
88. What are stop words?
89. What is TF-IDF?
90. What are word embeddings?
91. Word2Vec vs GloVe?
92. What is semantic similarity?
93. What is cosine similarity?
94. Why are embeddings useful in GenAI?
95. What is an embedding model?
96. What determines embedding dimensionality?
97. What is an embedding space?
98. Sparse vs dense vectors?
99. What is the curse of dimensionality?
100. How do you evaluate an embedding model?

---

# 6. Transformers

> ⭐ **Highest Priority**

Transformers are one of the most important ML concepts for a modern GenAI interview.

## Questions

101. What is a Transformer?
102. Why were Transformers introduced?
103. Transformers vs RNNs?
104. Explain Transformer architecture.
105. What is self-attention?
106. What are Query, Key, and Value?
107. How is attention calculated?
108. What is scaled dot-product attention?
109. Why do we divide attention by √dₖ?
110. What is multi-head attention?
111. Why do we need multiple attention heads?
112. What is positional encoding?
113. Why is positional information required?
114. Learned vs sinusoidal positional embeddings?
115. What is causal attention?
116. What is masked attention?
117. Encoder vs Decoder?
118. Encoder-only vs Decoder-only vs Encoder-Decoder?
119. BERT vs GPT?
120. Why is GPT decoder-only?
121. What is a Transformer block?
122. What is LayerNorm?
123. What is a residual connection?
124. What is the feed-forward network?
125. What is attention complexity?
126. Why does attention become expensive for long contexts?
127. How can long-context problems be addressed?
128. What is KV Cache?
129. Why does KV caching improve inference?
130. What is a context window?

---

# 7. LLM Fundamentals

## Questions

131. What is an LLM?
132. How is an LLM trained?
133. What is pretraining?
134. What objective is used during LLM pretraining?
135. What is next-token prediction?
136. What is causal language modeling?
137. What is masked language modeling?
138. What is instruction tuning?
139. What is supervised fine-tuning?
140. What is RLHF?
141. What is DPO?
142. RLHF vs DPO?
143. What is alignment?
144. What is hallucination?
145. Why do LLMs hallucinate?
146. How can hallucinations be reduced?
147. What is temperature?
148. What is top-k sampling?
149. What is top-p sampling?
150. Temperature vs top-p?
151. What is greedy decoding?
152. What is beam search?
153. Deterministic vs stochastic generation?
154. What is quantization?
155. What is pruning?
156. What is knowledge distillation?
157. What is LoRA?
158. What is QLoRA?
159. Fine-tuning vs RAG?
160. When should you use RAG instead of fine-tuning?

---

# 8. RAG and Retrieval

> ⭐ **Critical for GenAI Engineers**

## Questions

161. What is RAG?
162. Why do we need RAG?
163. Explain the complete RAG pipeline.
164. What is document chunking?
165. Why does chunk size matter?
166. Fixed-size vs semantic chunking?
167. What is chunk overlap?
168. What happens when chunks are too large?
169. What happens when chunks are too small?
170. What are embeddings?
171. How does semantic search work?
172. What is vector similarity?
173. Cosine similarity vs Euclidean distance?
174. What is vector indexing?
175. What is HNSW?
176. What is IVF?
177. HNSW vs IVF?
178. What is Approximate Nearest Neighbor search?
179. Why use ANN instead of exact search?
180. What is hybrid search?
181. BM25 vs vector search?
182. Why combine keyword and vector search?
183. What is reranking?
184. Why is reranking required?
185. Cross-encoder vs bi-encoder?
186. What is retrieval precision?
187. What is retrieval recall?
188. What is Recall@K?
189. What is Precision@K?
190. What is MRR?
191. What is NDCG?
192. How do you evaluate a RAG system?
193. How do you detect poor retrieval?
194. How do you improve retrieval quality?
195. What if the correct document exists but is not retrieved?
196. How do you debug hallucinations in RAG?
197. How do you choose an embedding model?
198. How do you choose K?
199. How do metadata filters improve retrieval?
200. How would you build a production RAG evaluation framework?

---

# 9. Fine-Tuning

## Questions

201. When should you fine-tune an LLM?
202. When should you NOT fine-tune?
203. RAG vs fine-tuning?
204. Prompt engineering vs fine-tuning?
205. What is supervised fine-tuning?
206. What is LoRA?
207. Why is LoRA parameter efficient?
208. What is QLoRA?
209. What are adapters?
210. What is catastrophic forgetting?
211. How do you prepare a fine-tuning dataset?
212. How do you evaluate a fine-tuned model?
213. What causes overfitting during fine-tuning?
214. How do you prevent it?
215. How do you select a learning rate?
216. What is PEFT?
217. Full fine-tuning vs PEFT?
218. LoRA vs full fine-tuning?
219. What is quantization-aware training?
220. What is inference quantization?

---

# 10. Production GenAI and ML

## Questions

221. How do you evaluate an LLM application?
222. How do you measure hallucination?
223. How do you measure retrieval quality?
224. How do you create a golden dataset?
225. What is offline evaluation?
226. What is online evaluation?
227. What is LLM-as-a-Judge?
228. What are the limitations of LLM-as-a-Judge?
229. How do you perform human evaluation?
230. What is A/B testing for LLM applications?
231. How do you monitor an LLM application?
232. What production metrics would you monitor?
233. How do you reduce LLM latency?
234. How do you reduce LLM cost?
235. How do you handle model failures?
236. How do you implement model fallback?
237. How do you choose between LLM providers/models?
238. How do you handle model version changes?
239. What is model drift in an LLM application?
240. How do you detect degradation after changing an embedding model?

---

# 11. Scenario-Based Questions

> ⭐ **Very Important for 6+ Years Experience**

At senior level, interviewers often move from theoretical questions to architecture and troubleshooting scenarios.

### Scenario 1 — Poor Retrieval

**Your RAG system retrieves irrelevant documents. How would you debug it?**

Consider:

```text
Query
  ↓
Query preprocessing
  ↓
Embedding model
  ↓
Vector search
  ↓
Metadata filtering
  ↓
Hybrid search
  ↓
Reranking
  ↓
Top-K
```

---

### Scenario 2 — Good Retrieval, Bad Answer

**Your retrieval is good but the LLM still gives incorrect answers. What could be wrong?**

Investigate:

* Prompt construction
* Context ordering
* Context length
* Conflicting documents
* LLM behavior
* Temperature
* Prompt injection
* Missing instructions
* Hallucination
* Poor grounding

---

### Scenario 3 — High Recall, Poor Answer

**Your system has high Recall@10 but poor answer quality. What would you investigate?**

Potential areas:

* Precision
* Reranking
* Context quality
* Chunk size
* Duplicate chunks
* Context ordering
* Prompt design
* LLM capability

---

### Scenario 4 — Correct Document Not Retrieved

**The correct document exists in the vector database but isn't retrieved. Why?**

Investigate:

* Poor embedding
* Poor chunking
* Query mismatch
* Wrong metadata filters
* Incorrect similarity metric
* Poor index configuration
* Insufficient K
* Domain-specific vocabulary

---

### Scenario 5 — Multilingual Retrieval

**Your embedding model works well for English but poorly for Hindi. What would you do?**

Consider:

* Multilingual embeddings
* Domain-specific evaluation dataset
* Query translation
* Hybrid search
* Language-aware retrieval
* Reranking

---

### Scenario 6 — Hallucination

**Your LLM produces hallucinations even when the correct context is provided. How would you handle it?**

Consider:

```text
Better Retrieval
      ↓
Better Context
      ↓
Grounded Prompt
      ↓
Lower Temperature
      ↓
Structured Output
      ↓
Validation
      ↓
Citation / Evidence Check
```

---

### Scenario 7 — Reranking Latency

**Latency increases significantly after adding a reranker. How would you optimize it?**

Consider:

* Reduce candidate K
* Use a smaller reranker
* Batch inference
* Cache results
* Parallelize retrieval
* Optimize model inference
* Use approximate retrieval before reranking

---

### Scenario 8 — Large Dataset

**You have 10 million documents. How would you design the retrieval system?**

Discuss:

* Document ingestion
* Chunking
* Embeddings
* Vector database
* ANN indexing
* HNSW/IVF
* Metadata filtering
* Hybrid search
* Reranking
* Distributed architecture
* Monitoring
* Evaluation

---

### Scenario 9 — Embedding Model Migration

**You replace your embedding model. How do you evaluate whether the new model is better?**

Consider:

1. Build a benchmark dataset.
2. Generate embeddings using both models.
3. Run retrieval.
4. Compare Recall@K.
5. Compare Precision@K.
6. Compare MRR/NDCG.
7. Evaluate downstream answer quality.
8. Compare latency and cost.
9. Perform A/B testing.

---

### Scenario 10 — LLM Selection

**How would you compare two LLMs for a production application?**

Evaluate:

* Accuracy
* Grounding
* Reasoning
* Latency
* Token cost
* Context window
* Reliability
* Structured output
* Tool calling
* Safety
* Throughput

---

# 12. Interview Priority

## 🔴 Highest Priority

Master these first:

```text
Transformers
      ↓
Attention
      ↓
Embeddings
      ↓
Vector Search
      ↓
RAG
      ↓
Retrieval Evaluation
      ↓
Reranking
      ↓
LLM Evaluation
      ↓
Fine-Tuning
      ↓
Production GenAI
```

## 🟠 Medium Priority

* Deep Learning fundamentals
* NLP fundamentals
* ML evaluation
* Traditional ML algorithms
* Classification
* Clustering
* Optimization

## 🟡 Lower Priority for GenAI

For a pure GenAI Engineer role, don't spend disproportionate time on:

* Advanced mathematical proofs
* Complex statistical derivations
* Advanced classical ML algorithms
* Research-level optimization
* Highly theoretical ML topics

Know the concepts and be able to explain **when and why you would use them**.

---

# 13. Preparation Strategy

## Phase 1 — ML Fundamentals

Study:

```text
Supervised Learning
Unsupervised Learning
Overfitting
Underfitting
Bias-Variance
Regularization
Loss Functions
Gradient Descent
Evaluation Metrics
```

---

## Phase 2 — Deep Learning

Study:

```text
Neural Networks
Activation Functions
Forward Propagation
Backpropagation
Optimizers
Learning Rate
Batch Size
Dropout
Normalization
Transfer Learning
```

---

## Phase 3 — NLP

Study:

```text
Tokenization
TF-IDF
Word Embeddings
Word2Vec
Semantic Similarity
Cosine Similarity
Dense Vectors
Embedding Models
```

---

## Phase 4 — Transformers

Study deeply:

```text
Transformer Architecture
Self-Attention
Query / Key / Value
Multi-Head Attention
Positional Encoding
Causal Attention
Masked Attention
Encoder
Decoder
LayerNorm
Residual Connections
KV Cache
Context Window
```

---

## Phase 5 — LLMs

Study:

```text
Pretraining
Next Token Prediction
Instruction Tuning
SFT
RLHF
DPO
Temperature
Top-K
Top-P
Hallucination
Quantization
LoRA
QLoRA
Fine-Tuning
```

---

## Phase 6 — RAG

Master:

```text
Document Ingestion
      ↓
Chunking
      ↓
Embedding
      ↓
Vector Database
      ↓
Similarity Search
      ↓
Hybrid Search
      ↓
Reranking
      ↓
Top-K
      ↓
Prompt Construction
      ↓
LLM
      ↓
Evaluation
```

---

## Phase 7 — Production

Understand:

```text
Latency
Cost
Caching
Scaling
Monitoring
Observability
Evaluation
Model Versioning
Fallback Models
A/B Testing
Data Drift
Model Drift
Security
Guardrails
```

---

# 🧠 Senior Interview Mindset

For every question, don't stop at:

> **"What is it?"**

Also prepare:

### 1. What is it?

Definition.

### 2. Why do we need it?

Business/engineering reason.

### 3. How does it work?

Technical explanation.

### 4. When would you use it?

Practical decision-making.

### 5. What are the alternatives?

Trade-offs.

### 6. What are the problems?

Limitations.

### 7. How did you use it in a project?

Real-world example.

---

# 🎯 Example of a Senior-Level Answer

### Interviewer:

**Why would you use RAG instead of fine-tuning?**

### Weak Answer:

> RAG retrieves documents and gives them to the LLM.

### Strong 6-Year Answer:

> I would prefer RAG when the model needs access to frequently changing, private, or domain-specific knowledge. Instead of modifying the model weights, I retrieve relevant information from an external knowledge base and provide it as context to the LLM.
>
> This gives us easier knowledge updates, better traceability, and usually lower maintenance cost compared with repeatedly fine-tuning the model.
>
> I would consider fine-tuning when the primary requirement is changing the model's behavior, style, output format, or task-specific capabilities rather than simply adding factual knowledge.
>
> In production, I would also evaluate retrieval quality independently using metrics such as Recall@K, MRR, or NDCG and then evaluate the final grounded answer quality.

---

# 🏆 Final Preparation Target

For a **6-year GenAI Engineer interview**, aim to be able to confidently explain:

```text
                    GENAI ML
                       │
        ┌──────────────┼──────────────┐
        │              │              │
   ML Fundamentals  Deep Learning    NLP
        │              │              │
        └──────────────┼──────────────┘
                       │
                  Transformers
                       │
                  Attention
                       │
                     LLMs
                       │
          ┌────────────┴────────────┐
          │                         │
         RAG                    Fine-Tuning
          │                         │
   Embeddings                  LoRA / QLoRA
   Vector Search                    │
   Hybrid Search                    │
   Reranking                        │
          │                         │
          └────────────┬────────────┘
                       │
                 Evaluation
                       │
              Production GenAI
```

## ⭐ Most Important Questions to Master

If you have limited preparation time, prioritize:

1. What is a Transformer?
2. How does self-attention work?
3. Explain Query, Key, and Value.
4. Why do we need positional encoding?
5. Encoder vs decoder?
6. How does an LLM generate text?
7. What are embeddings?
8. How does semantic search work?
9. What is cosine similarity?
10. HNSW vs IVF?
11. What is RAG?
12. How do you improve RAG retrieval?
13. What is hybrid search?
14. What is reranking?
15. Cross-encoder vs bi-encoder?
16. How do you evaluate RAG?
17. Recall@K vs Precision@K?
18. MRR vs NDCG?
19. RAG vs fine-tuning?
20. What is LoRA?
21. What is QLoRA?
22. What is hallucination?
23. How do you reduce hallucinations?
24. How do you evaluate an LLM?
25. How do you build a production-grade GenAI evaluation system?
26. How do you reduce LLM latency?
27. How do you reduce LLM cost?
28. How do you choose an embedding model?
29. How do you choose an LLM?
30. How would you debug a production RAG system?

---

# 🚀 Recommended Repository Structure

```text
genai-ml-interview-preparation/
│
├── README.md
│
├── 01-ml-fundamentals/
│   └── questions.md
│
├── 02-ml-algorithms/
│   └── questions.md
│
├── 03-ml-evaluation/
│   └── questions.md
│
├── 04-deep-learning/
│   └── questions.md
│
├── 05-nlp/
│   └── questions.md
│
├── 06-transformers/
│   └── questions.md
│
├── 07-llm/
│   └── questions.md
│
├── 08-rag/
│   └── questions.md
│
├── 09-fine-tuning/
│   └── questions.md
│
├── 10-production-genai/
│   └── questions.md
│
└── 11-scenario-based/
    └── questions.md
```

---

# 📌 Goal

The ultimate goal is **not memorizing ML definitions**.

The goal is to confidently answer:

> **"Why did you choose this approach, how does it work, what are the alternatives, what are the trade-offs, and how would you implement and evaluate it in production?"**

That is the level expected from a **6+ year Senior GenAI Engineer**.
