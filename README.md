# Real-Time Fact Checking using Hybrid Retrieval-Augmented Generation (RAG)

A Hybrid Retrieval-Augmented Generation (RAG) framework for automated fact verification that combines dense semantic retrieval, sparse lexical retrieval, cross-encoder reranking, and transformer-based Natural Language Inference (NLI). The system retrieves evidence from Wikipedia and verifies factual claims using a DeBERTa-based inference model.

---

## Overview

The rapid growth of digital news platforms and social media has accelerated the spread of misinformation, making it increasingly difficult to distinguish factual information from false or misleading claims. Traditional fact-checking approaches are largely manual, making them time-consuming, resource-intensive, and difficult to scale.

This project presents an end-to-end Hybrid Retrieval-Augmented Generation (RAG) system that automatically retrieves trustworthy evidence from Wikipedia and verifies factual claims using transformer-based Natural Language Inference. By combining dense semantic retrieval, sparse lexical retrieval, cross-encoder reranking, and DeBERTa-based claim verification, the system provides evidence-backed predictions for automated fact checking.

---

## Objectives

The project aims to:

- Detect misinformation in news articles, social media posts, and other online content.
- Retrieve relevant evidence from a trusted knowledge base using hybrid dense and sparse retrieval.
- Improve retrieval quality through Cross-Encoder reranking.
- Verify factual claims using a DeBERTa Natural Language Inference model.
- Build a scalable Retrieval-Augmented Generation pipeline for evidence-based fact verification.

---

## Key Features

- Hybrid Retrieval using Dense Retrieval (FAISS) and Sparse Retrieval (BM25)
- Semantic search using BGE embeddings
- Cross-Encoder reranking for evidence selection
- DeBERTa-based Natural Language Inference
- Wikipedia knowledge base for evidence retrieval
- End-to-end fact verification pipeline
- Retrieval and classification evaluation

---

## System Architecture

```text
Input Claim
      │
      ▼
Sentence Embedding (BGE)
      │
      ▼
Dense Retrieval (FAISS)
      │
      ├──────────────┐
      ▼              │
Sparse Retrieval     │
(BM25)              │
      │              │
      └──────┬───────┘
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

## Dataset

The project uses the following publicly available datasets:

| Dataset | Purpose |
|----------|---------|
| FEVER Dataset | Fact verification claims |
| Wikipedia Corpus | Evidence retrieval and knowledge base |

---

## Technology Stack

| Category | Technologies |
|-----------|--------------|
| Programming Language | Python |
| Deep Learning | PyTorch |
| Transformers | Hugging Face Transformers |
| Embeddings | BGE |
| Dense Retrieval | FAISS |
| Sparse Retrieval | BM25 |
| Reranking | Cross-Encoder |
| Fact Verification | DeBERTa |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn |
| Visualization | Matplotlib |

---

## Repository Structure

```text
Real-Time-Fact-Checking-RAG
│
├── README.md
├── requirements.txt
├── LICENSE
├── .gitignore
│
├── notebooks/
│   └── Real_Time_Fact_Checking_RAG.ipynb
│
├── results/
│   └── error_analysis.csv
│
├── data/
│   └── README.md
│
└── docs/
    └── methodology.md
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/Suchi-2024/Real-Time-Fact-Checking-RAG.git
cd Real-Time-Fact-Checking-RAG
```

Install the required packages:

```bash
pip install -r requirements.txt
```

---

## Running the Project

Open the notebook:

```
notebooks/Real_Time_Fact_Checking_RAG.ipynb
```

Run all notebook cells sequentially to reproduce the complete pipeline.

---

## Pipeline

The complete workflow consists of the following stages:

1. Input factual claim
2. Generate semantic embeddings using BGE
3. Retrieve candidate evidence using FAISS
4. Retrieve additional evidence using BM25
5. Merge dense and sparse retrieval results
6. Rerank evidence using a Cross-Encoder
7. Select the highest-ranked evidence passages
8. Verify the claim using DeBERTa Natural Language Inference
9. Produce the final prediction and confidence score

---

## Results

The system is evaluated using standard retrieval and classification metrics, including:

- Retrieval Recall
- Precision
- Accuracy
- Recall
- F1 Score
- Confusion Matrix

Evaluation outputs and visualizations are available in the `results/` directory.

---

## Future Work

The following enhancements are planned for future versions of the project:

- Media bias analysis across multiple news sources
- Real-time news article fact checking
- Streamlit-based web application
- FastAPI deployment
- Multilingual fact verification
- Explainable AI for evidence interpretation
- LLM-based evidence summarization and reasoning

---

## References

- FEVER: Fact Extraction and VERification Dataset
- Wikipedia
- Hugging Face Transformers
- Sentence Transformers
- FAISS
- BM25
- DeBERTa

---
