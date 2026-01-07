# legal-rag-court-judgments

This project explores a **retrieval-augmented generation (RAG)** pipeline built over **Indian court judgments** to study how semantic retrieval behaves on legal text corpus.

The goal of the project is **not** to build a general legal assistant, but to understand:
- what types of legal questions court-judgment corpora can answer well
- where retrieval breaks down
- when a system should **refuse to answer** instead of hallucinating

---

## Project Scope

### What this project covers
- Criminal law judgments
- Property and land-related disputes
- Procedural and evidentiary issues
- Judicial reasoning from Supreme Court and High Courts

### What this project does NOT cover
- Tax filing or compliance obligations
- Family law (divorce, maintenance, custody)
- Regulatory or advisory law
- Statutory guidance not litigated in courts

NOTE: The dataset reflects **post-facto legal disputes**, not pre-facto legal advice.

---

## System Overview

The pipeline consists of two main stages:

1. **Indexing**
   - Court judgments are cleaned, chunked, and embedded using sentence-transformer models
   - Embeddings are stored and indexed using FAISS for semantic similarity search
   - Metadata is preserved to trace retrieved chunks back to their sources

2. **Retrieval and Answering**
   - User questions are embedded directly (without forced rewriting)
   - Relevant document chunks are retrieved using FAISS
   - Answers are generated strictly from retrieved text
   - If documents do not address the legal issue, the system explicitly refuses to answer

---

## Key Design Decisions

### No query rewriting for retrieval
LLM-based query rewriting was tested and found to **reduce retrieval quality** when using general-purpose sentence embeddings over court judgments.
No matter the prompt given for rewriting, if it worked for certain kind of queries, it failed for certain others.

Raw user questions consistently produced higher similarity scores and more relevant results.  
As a result, **query rewriting was intentionally removed from the retrieval path**.

### Refusal over hallucination
If retrieved documents do not directly answer the legal question, the system refuses instead of guessing.  
This is a deliberate safety and correctness choice.

### FAISS index handling
FAISS indexes are rebuilt from stored embeddings rather than serialized with pickle, as FAISS contains native C++ state that is not reliably pickle-safe in Colab environments.

---

## Repository Structure

