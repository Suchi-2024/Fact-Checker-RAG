# Methodology

## Project Overview

This project implements a Hybrid Retrieval-Augmented Generation (RAG) pipeline for automated fact verification. The system retrieves relevant evidence from a Wikipedia knowledge base using hybrid retrieval techniques and verifies factual claims using a transformer-based Natural Language Inference (NLI) model.

The implementation focuses on efficient evidence retrieval, reranking, and claim verification while remaining scalable within the computational constraints of the Kaggle environment.

---

## Workflow

The complete pipeline consists of the following stages:

```
Input Claim
      │
      ▼
Claim Embedding
      │
      ▼
Dense Retrieval (FAISS)
      │
      ├─────────────┐
      ▼             │
Sparse Retrieval    │
(BM25)             │
      │             │
      └──────┬──────┘
             ▼
Hybrid Candidate Merge
             ▼
Cross-Encoder Reranking
             ▼
Top Evidence Selection
             ▼
DeBERTa Natural Language Inference
             ▼
Final Prediction
```

---

# 1. Dataset

The project uses publicly available datasets:

### FEVER Dataset

The FEVER (Fact Extraction and VERification) dataset provides:

- Claims
- Ground-truth labels
- Supporting evidence references

The dataset contains three verification labels:

- SUPPORTS
- REFUTES
- NOT ENOUGH INFO

### Wikipedia Corpus

Initially, the project attempted to use the complete Wikipedia corpus. However, embedding millions of pages exceeded the available memory and execution limits on Kaggle.

To address this limitation, the project uses the **Cohere Wikipedia Simple Embeddings** dataset, which provides:

- Pre-computed dense embeddings
- Pre-chunked passages
- Article titles
- Passage text
- Metadata

This significantly reduces preprocessing time while enabling efficient semantic retrieval. :contentReference[oaicite:1]{index=1}

---

# 2. Data Preparation

The retrieved Wikipedia passages are already preprocessed and embedded.

For the FEVER dataset:

- Claims are extracted
- Labels are preserved
- Evidence identifiers are retained for evaluation

No additional large-scale embedding generation is required.

---

# 3. Dense Retrieval

Semantic retrieval is performed using:

- BGE sentence embeddings
- FAISS vector index

Given an input claim:

1. Generate the claim embedding.
2. Search the FAISS index.
3. Retrieve the Top-K semantically similar passages.

Dense retrieval enables semantic matching beyond exact keyword overlap.

---

# 4. Sparse Retrieval

In addition to dense retrieval, BM25 lexical retrieval is used to capture exact keyword matches.

This improves retrieval quality for claims containing:

- Named entities
- Rare terms
- Specific phrases

---

# 5. Hybrid Retrieval

Results from FAISS and BM25 are merged into a unified candidate set.

Hybrid retrieval combines:

- semantic similarity
- lexical similarity

to improve overall evidence recall.

---

# 6. Cross-Encoder Reranking

Candidate passages are reranked using a Cross-Encoder model.

Unlike bi-encoder retrieval, the Cross-Encoder jointly encodes:

- Claim
- Evidence

This produces more accurate relevance scores, allowing the most informative evidence to be selected before verification.

---

# 7. Claim Verification

The highest-ranked evidence is paired with the original claim and passed to a DeBERTa-based Natural Language Inference model.

The model predicts one of three classes:

- SUPPORTS
- REFUTES
- NOT ENOUGH INFO

The final output consists of:

- predicted label
- confidence score
- retrieved supporting evidence

---

# 8. Evaluation

The notebook evaluates both retrieval and verification performance using:

- Accuracy
- Precision
- Recall
- F1 Score
- Error Analysis

Detailed evaluation results are available in the notebook.

---

# 9. Challenges

During development, several practical challenges were encountered:

- Memory limitations when processing large Wikipedia datasets
- Long embedding generation times
- Efficient nearest-neighbor search for large corpora
- Selecting the most relevant evidence before claim verification

Using precomputed Wikipedia embeddings and FAISS indexing significantly reduced both memory usage and retrieval time. :contentReference[oaicite:2]{index=2}

---

# 10. Future Work

Planned improvements include:

- Media bias analysis across multiple news sources
- Real-time news article verification
- Live news ingestion through APIs
- Multilingual fact verification
- Explainable AI for evidence interpretation
- FastAPI and Streamlit deployment
- LLM-based evidence summarization